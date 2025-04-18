## 第八章 有用的正则表达式

在本章中，我们将讨论各种正则表达式，以及如何在一些方便的单行代码中使用它们。正则表达式包括匹配 IP 地址、HTTP 头和电子邮件地址；匹配数字和数字范围；提取和修改匹配项。我还将分享一些正则表达式难题和最佳实践。本章与前几章略有不同，因为我将从一个正则表达式开始，然后编写一个使用它的单行代码。

## 8.1 匹配看起来像 IP 地址的东西

```
/^\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}$/
```

这个正则表达式实际上并不能保证匹配的东西真的是一个有效的 IP 地址；它仅仅匹配看起来像 IP 地址的东西。例如，它可以匹配一个有效的 IP 地址，如 `81.198.240.140`，也可以匹配一个无效的 IP 地址，如 `936.345.643.21`。

这是它的工作原理。正则表达式开头的 `^` 是一个锚点，用来匹配字符串的开头。接下来，`\d{1,3}` 匹配一位、两位或三位连续的数字。`\.` 匹配一个点。结尾的 `$` 是一个锚点，用来匹配字符串的结尾。（你使用 `^` 和 `$` 锚点来防止像 `foo213.3.1.2bar` 这样的字符串匹配。）

你可以通过将前三个重复的 `\d{1,3}\.` 表达式分组来简化这个正则表达式：

```
/^(\d{1,3}\.){3}\d{1,3}$/
```

假设你有一个文件，内容如下，并且你想提取看起来像 IP 地址的行：

```
81.198.240.140
1.2.3.4
5.5
444.444.444.444
90.9000.90000.90000
127.0.0.1
```

要提取仅匹配的行，可以写成这样：

```
perl -ne 'print if /^\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}$/'
```

这应该会输出：

```
81.198.240.140
1.2.3.4
444.444.444.444
127.0.0.1
```

单行代码 8.3 解释了如何精确匹配一个 IP，而不仅仅是看起来像 IP 的东西。

## 8.2 测试一个数字是否在 0 到 255 的范围内

```
/^([0-9]|[0-9][0-9]|1[0-9][0-9]|2[0-4][0-9]|25[0-5])$/
```

我喜欢用难题来挑战人们。我最喜欢的一个问题是让某人编写一个匹配数字范围的正则表达式。如果你以前从未做过的话，写出一个其实是相当棘手的。

这是它的工作原理。一个数字可以有一位、两位或三位。如果数字是一位，你可以让它是任何 `[0-9]`。如果它有两位，你也允许它是 `[0-9][0-9]` 的任意组合。但是如果数字有三位，它必须是 100 到 199 之间的某个数字，或者是 200 到 249 之间的数字。如果数字是 100 到 199 之间的，那么 `1[0-9][0-9]` 匹配它。如果数字是 200 到 249 之间的，那么这个数字要么是 200 到 249（由 `2[0-4][0-9]` 匹配），要么是 250 到 255（由 `25[0-5]` 匹配）。

让我们确认这个正则表达式真的能匹配从 0 到 255 的所有数字，并编写一个单行代码来实现它：

```
perl -le '
  map { $n++ if /^([0-9]|[0-9][0-9]|1[0-9][0-9]|2[0-4][0-9]|25[0-5])$/ } 0..255;
  END { print $n }
'
```

这个单行代码输出 256，这是 0 到 255 范围内的总数字。它会遍历 0 到 255 的范围，并在每个匹配的数字上增加 `$n` 变量。如果输出值小于 256，你就知道有些数字没有匹配。

让我们还确保这个单行代码不会匹配超过 255 的数字：

```
perl -le '
  map { $n++ if /^([0-9]|[0-9][0-9]|1[0-9][0-9]|2[0-4][0-9]|25[0-5])$/ } 0..1000;
  END { print $n }
'
```

尽管有 1001 次迭代，从 0 到 1000，最终`$n`的值和输出应该仍然是 256，因为大于 255 的数字不应该匹配。如果值大于 256，你就会知道匹配的数字太多，正则表达式是错误的。

## 8.3 匹配一个 IP 地址

```
my $ip_part = qr/[0-9]|[0-9][0-9]|1[0-9][0-9]|2[0-4][0-9]|25[0-5]/;
if ($ip =~ /^$ip_part\.$ip_part\.$ip_part\.$ip_part$/) {
  print "valid ip\n";
}
```

这个正则表达式结合了前两个正则表达式（8.1 和 8.2）的思想，并引入了`qr/.../`操作符，它允许你构造一个正则表达式并将其保存在变量中。在这里，我将匹配 0 到 255 范围内所有数字的正则表达式保存在`$ip_part`变量中。接下来，`$ip_part`匹配 IP 地址的四个部分。

你可以通过将前三个 IP 部分分组来简化这一点：

```
if ($ip =~ /^($ip_part\.){3}$ip_part$/) {
  print "valid ip\n";
}
```

让我们在与一行代码 8.1 相同的文件上运行这个。如果你的输入文件是：

```
81.198.240.140
1.2.3.4
5.5
444.444.444.444
90.9000.90000.90000
127.0.0.1
```

你的一行代码是

```
perl -ne '
  $ip_part = qr{([0-9]|[0-9][0-9]|1[0-9][0-9]|2[0-4][0-9]|25[0-5])};
  print if /^($ip_part\.){3}$ip_part$/
'
```

然后输出是

```
81.198.240.140
1.2.3.4
127.0.0.1
```

如你所见，只有有效的 IP 地址会被打印出来。

## 8.4 检查字符串是否像一个电子邮件地址

```
/\S+@\S+\.\S+/
```

这个正则表达式确保字符串看起来像一个电子邮件地址；然而，它并不保证字符串就是一个电子邮件地址。首先，它匹配不是空白的内容（`\S+`）直到`@`符号；然后它尽可能多地匹配，直到找到一个点；接着它再匹配一些内容。

如果匹配成功，你知道该字符串至少看起来像是一个带有`@`符号和点的电子邮件地址。例如，`cats@catonmat.net`匹配，但`cats@catonmat`不匹配，因为正则表达式无法找到一个完全合格的域名所需的点。

这是一个更加健壮的方法来判断一个字符串是否是有效的电子邮件地址，使用`Email::Valid`模块：

```
use Email::Valid;
print Email::Valid->address('cats@catonmat.net') ? 'valid email' : 'invalid email';
```

在这里，你使用了三元运算符`cond ? true : false`。如果`cond`为真，则执行`true`部分；否则执行`false`部分。如果电子邮件有效，它将打印`valid email`；如果无效，则打印`invalid email`。

所以一行代码可以像这样：

```
perl -MEmail::Valid -ne 'print if Email::Valid->address($_)'
```

在这里，如果电子邮件地址有效，你只需打印它。

## 8.5 检查字符串是否是数字

使用正则表达式来判断一个字符串是否是数字很困难。这是一个匹配十进制数字的正则表达式的衍生形式。

我从 Perl 的`\d`正则表达式开始，它匹配数字 0 到 9：

```
/^\d+$/
```

这个正则表达式从字符串的开始`^`到结束`$`匹配一个或多个数字`\d`。但它不匹配像`+3`和`-3`这样的数字。让我们修改正则表达式以匹配它们：

```
/^[+-]?\d+$/
```

在这里，`[+-]?`表示“匹配数字前的可选加号或减号。”这个正则表达式现在匹配`+3`和`-3`，但不匹配`-0.3`。让我们添加这个：

```
/^[+-]?\d+\.?\d*$/
```

我通过添加`\.?\d*`扩展了之前的正则表达式，这匹配一个可选的点后跟零个或多个数字。现在我们可以开始了。这个正则表达式也匹配像`-0.3`和`0.3`这样的数字，但不会匹配像`123,456`或`.5`这样的数字。

匹配十进制数字的一个更好的方法是使用`Regexp::Common`模块。例如，要匹配一个十进制数字，你可以使用`Regexp::Common`中的`$RE{num}{real}`。以下是一行代码，它过滤输入并只打印十进制数字：

```
perl -MRegexp::Common -ne 'print if /$RE{num}{real}/'
```

这个一行代码也匹配并打印类似`123,456`和`.5`这样的数字。

那么，如何匹配正十六进制数字呢？方法如下：

```
/⁰x[0-9a-f]+$/i
```

这个一行代码匹配十六进制前缀`0x`，后面跟着十六进制数字本身。末尾的`/i`标志确保匹配时不区分大小写。例如，`0x5af`匹配，`0X5Fa`匹配，但`97`不匹配，因为`97`没有十六进制前缀。

更好的做法是使用`$RE{num}{hex}`，因为它支持负数、十进制数和数字分组。

那么，如何匹配八进制数字呢？

```
/⁰[0-7]+$/
```

八进制数字以 0 为前缀，后跟八进制数字`0-7`。例如，`013`是有效的，而`09`不是，因为它不是一个有效的八进制数字。使用`$RE{num}{oct}`更好，因为它支持负数八进制数、小数点八进制数以及数字分组。

最后，我们来到了二进制匹配：

```
/^[01]+$/
```

二进制基数只由 0 和 1 组成，因此`010101`匹配，但`210101`不匹配，因为`2`不是一个有效的二进制数字。

`Regexp::Common`还提供了一个更好的正则表达式来匹配二进制数字：`$RE{num}{bin}`。

## 8.6 检查一个单词是否在字符串中出现两次

```
/(*word*).*\1/
```

这个正则表达式匹配一个单词，后面跟着其他字符或什么都没有，再跟着同样的单词。这里，`(word)`将单词捕获到组 1 中，`\1`指代组 1 的内容，等同于写`/(word).*word/`。例如，`silly things are silly`匹配`/(silly).*\1/`，但`silly things are boring`不匹配，因为`silly`在字符串中没有重复。

## 8.7 将字符串中的所有整数增加 1

```
$str =~ s/(\d+)/$1+1/ge
```

在这里，你使用替换操作符`s`来匹配所有整数`(\d+)`，将它们放入捕获组 1，然后将它们替换为其值加一：`$1+1`。`g`标志表示查找字符串中的所有数字，`e`标志表示将`$1+1`作为 Perl 表达式求值。例如，`this 1234 is awesome 444`会变成`this 1235 is awesome 445`。

请注意，这个正则表达式不会增加浮点数，因为它使用`\d+`来匹配整数。要增加浮点数，请使用一行代码 8.5 中的`$RE{num}{real}`正则表达式。这里有一个使用`$RE{num}{real}`的一行代码示例：

```
perl -MRegexp::Common -pe 's/($RE{num}{real})/$1+1/ge'
```

如果你传入这个一行代码的输入`weird 44.5 line -1.25`，它会打印`weird 45.5 line -0.25`。

## 8.8 从 HTTP 头提取 HTTP 用户代理字符串

```
/^User-Agent: (.+)$/
```

HTTP 头部的格式是`Key: Value`对。你可以通过指示正则表达式引擎将`Value`部分保存在`$1`组变量中来轻松解析这样的字符串。例如，如果 HTTP 头包含以下内容：

```
Host: www.catonmat.net
Connection: keep-alive
User-Agent: Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10_0_0; en-US)
Accept: application/xml,application/xhtml+xml,text/html
Accept-Encoding: gzip,deflate,sdch
Accept-Language: en-US,en;q=0.8
Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.3
```

那么，正则表达式将提取字符串`Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10_0_0; en-US)`。

## 8.9 匹配可打印的 ASCII 字符

```
/[ -~]/
```

这个正则表达式既巧妙又复杂。要理解它，可以查看`man ascii`，你会看到空格的值是`0x20`，而`~`字符的值是`0x7e`。表达式`[ -~]`定义了一个从空格到`~`的字符范围。因为所有在空格和`~`之间的字符都是可打印的，所以这个正则表达式匹配所有可打印字符。这是我最喜欢的正则表达式，因为当你第一次看到它时，它让人感到困惑。它匹配什么？一个空格，一个破折号和一个波浪线？不，它匹配的是从空格到波浪线之间的所有字符！

要反转匹配，可以将`^`放在分组的第一个字符位置：

```
/[^ -~]/
```

这个正则表达式匹配的是与`[ -~]`相反的内容，也就是说，匹配所有不可打印字符。

## 8.10 提取两个 HTML 标签之间的文本

```
m|<strong>([^<]*)</strong>|
```

在我解释这个正则表达式之前，我想说的是，只有在快速处理并需要完成任务时，使用正则表达式匹配 HTML 是可以的。你*绝不*应该在正式的应用程序中使用正则表达式来匹配和解析 HTML，因为 HTML 实际上是一个复杂的语言，通常无法通过正则表达式来解析。相反，应该使用像`HTML::TreeBuilder`这样的模块来更清晰地完成任务！

这个正则表达式将`<strong>...</strong>`HTML 标签之间的文本保存到`$1`特殊变量中。这个单行代码中最棘手的部分是`([^<]*)`，它匹配直到`<`字符之前的所有内容。这是一个正则表达式惯用法。

例如，如果你试图匹配的 HTML 是`<strong>hello</strong>`，那么这个正则表达式会在`$1`变量中捕获`hello`。然而，如果你试图匹配的 HTML 是`<strong><em>hello</em> </strong>`，那么这个正则表达式就不会匹配，因为在`<strong>`和`</strong>`之间还有另一个 HTML 标签。

要提取两个 HTML 标签之间的所有内容，包括其他 HTML 标签，你可以写：

```
m|<strong>(.*?)</strong>|
```

这个正则表达式将`<strong>...</strong>`之间的所有内容保存到`$1`变量中。例如，如果 HTML 是`<strong><em>hello</em> </strong>`，那么这个正则表达式将`$1`设置为`<em>hello</em>`。正则表达式中的`(.*?)`部分匹配两个最接近的`<strong>`和`</strong>`标签之间的所有内容。正则表达式中的问号`?`控制其贪婪度。

如果你想成为一个好公民并使用`HTML::TreeBuilder`，那么一个执行相同操作的 Perl 程序应该是这样的：

```
use warnings;
use strict;
use HTML::TreeBuilder;
my $tree = HTML::TreeBuilder->new_from_content(
  "<strong><em>hello</em></strong>"
);
my $strong = $tree->look_down(_tag => 'strong');
if ($strong) {
  print $_->as_HTML for $strong->content_list;
}
$tree->delete;
```

在这里，我从给定的字符串创建了一个新的`HTML::TreeBuilder`实例；然后我找到了`<strong>`标签，并将所有`<strong>`标签的子元素以 HTML 格式输出。正如你所看到的，虽然像这样的程序不适合作为单行代码来写，但它是一个更加健壮的解决方案。

## 8.11 将所有`<b>`标签替换为`<strong>`

```
$html =~ s|<(/)?b>|<$1strong>|g
```

这里，我假设 HTML 内容存储在变量`$html`中。表达式`<(/)?b>`匹配开闭的`<b>`标签，捕获可选的闭合标签斜杠到组`$1`，然后根据是否找到开闭标签，将匹配到的标签替换为`<strong>`或`</strong>`。

请记住，正确的做法是使用`HTML::TreeBuilder`并编写一个合适的程序。你应该仅在快速解决问题时使用这个正则表达式。下面是一个使用`HTML::TreeBuilder`的程序示例：

```
use warnings;
use strict;
use HTML::TreeBuilder;
my $tree = HTML::TreeBuilder->new_from_content("
  <div><p><b>section 1</b></p><p><b>section 2</b></p></div>
");
my @bs = $tree->look_down(_tag => 'b');
$_->tag('strong') for @bs;
print $tree->as_HTML;
$tree->delete;
```

在这里，我从给定的字符串中创建了`HTML::TreeBuilder`对象；接下来，我找到了所有的`<b>`标签，并将它们存储在`@bs`数组中，然后遍历`@bs`并将它们的标签名称更改为`<strong>`。

## 8.12 从正则表达式中提取所有匹配项

```
my @matches = $text =~ /*regex*/g;
```

这里，正则表达式匹配的结果在列表上下文中进行评估，这使得它返回所有匹配项。匹配项被放入`@matches`变量中。

例如，下面的正则表达式从字符串中提取所有整数：

```
my $t = "10 hello 25 moo 30 foo";
my @nums = $text =~ /\d+/g;
```

执行这段代码后，`@nums`包含了`(10, 25, 30)`。你还可以使用括号仅捕获字符串的一部分。例如，下面是如何捕获只包含多个键值对（如`key=value`）并用分号分隔的行中的值：

```
my @vals = $text =~ /[^=]+=([^;]+)/g;
```

这个正则表达式首先通过`[^=]+`匹配键，然后匹配分隔键和值的`=`字符，接着匹配值部分`([^;]+)`。如你所见，正则表达式中的值部分被括在了括号中，因此这些值会被捕获。

这里有一个示例。假设你有一个文件，内容如下：

```
access=all; users=peter,alastair,bill; languages=awk,sed,perl
```

然后你写下了这个一行代码：

```
perl -nle 'my @vals = $_ =~ /[^=]+=([^;]+)/g; print "@vals"'
```

运行后输出如下：

```
all peter,alastair,bill awk,sed,perl
```

这些是`access`、`users`和`languages`键的值！
