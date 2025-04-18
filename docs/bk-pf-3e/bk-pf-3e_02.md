## 第二章：PF 配置基础

![PF 配置基础](img/httpatomoreillycomsourcenostarchimages2127149.png.jpg)

在本章中，我们将创建一个非常简单的 PF 配置。我们将从最简单的配置开始：一台配置为与单一网络通信的机器。这个网络很可能就是互联网。

配置 PF 的两大工具是你最喜欢的文本编辑器和 `pfctl` 命令行管理工具。PF 配置文件通常存储在 */etc/pf.conf* 中，称为 *规则集*，因为配置文件中的每一行都是一个 *规则*，帮助确定数据包过滤子系统应该如何处理它看到的网络流量。在日常管理中，你编辑 */etc/pf*.*conf* 文件中的配置，然后使用 `pfctl` 加载更改。虽然有 Web 界面可用于 PF 管理任务，但它们并不是系统的基础部分。PF 的开发者对这些选项并不排斥，但他们至今尚未见到一个显著优于编辑 *pf.conf* 文件并使用 `pfctl` 命令的图形界面。

## 第一步：启用 PF

在你开始使用 PF 和相关工具进行网络配置的有趣部分之前，你需要确保 PF 可用并已启用。具体的操作细节取决于你使用的操作系统：OpenBSD、FreeBSD 或 NetBSD。根据你的操作系统，按照相应的说明检查设置，然后继续阅读 简单的 PF 规则集：单一独立机器。

`pfctl` 命令是一个需要比普通用户默认权限更高的程序。在本书的其余部分，你将看到需要额外权限的命令，这些命令前面会加上 `sudo`。如果你还没有开始使用 `sudo`，应该开始使用它。OpenBSD 系统中自带了 `sudo`。在 FreeBSD、DragonFly BSD 和 NetBSD 中，也可以通过端口系统或 pkgsrc 系统轻松获取，并作为 *security/sudo* 提供。

这里有一些关于使用 `pfctl` 的一般说明：

+   禁用 PF 的命令是 `pfctl -d`。输入该命令后，所有可能已启用的基于 PF 的过滤规则将被禁用，所有流量将被允许通过。

+   为了方便，`pfctl` 可以在单行命令中执行多个操作。要启用 PF 并加载规则集，可以输入以下命令：

    ```
    $ **sudo pfctl -ef /etc/pf.conf**
    ```

### 在 OpenBSD 上设置 PF

在 OpenBSD 4.6 及之后的版本中，你无需手动启用 PF，因为它默认启用并且已有基本配置。如果你在系统启动时密切关注系统控制台，可能会注意到在内核消息完成后不久，`pf enabled` 消息就会出现。

如果你在启动时没有在控制台看到 `pf enabled` 消息，你有几个选项可以检查 PF 是否已经启用。一种简单的方法是输入你通常用来从命令行启用 PF 的命令：

```
$ **sudo pfctl -e**
```

如果 PF 已经启用，系统会返回以下消息：

```
pfctl: pf already enabled
```

如果 PF 没有启用，`pfctl -e` 命令会启用 PF 并显示如下信息：

```
pf enabled
```

在 OpenBSD 4.6 版本之前，PF 默认并未启用。你可以通过编辑 */etc/rc.conf.local* 文件（如果该文件不存在，可以创建该文件）来覆盖默认设置。虽然在较新的 OpenBSD 版本中不再需要这么做，但在你的 */etc/rc.conf.local* 文件中添加这一行并不会有害：

```
pf=YES           # enable PF
```

如果你查看在全新 OpenBSD 安装中的 */etc/pf.conf* 文件，你会第一次接触到一个有效的规则集。

默认的 OpenBSD *pf.conf* 文件从 `set skip on lo` 规则开始，确保环回接口组上的流量不会受到任何过滤。接下来的有效行是一个简单的 `pass` 默认规则，允许网络流量默认通过。最后，一个显式的 `block` 规则阻止远程的 X11 流量访问你的机器。

正如你可能已经注意到的，默认的 *pf.conf* 文件中也包含了一些以井号（`#`）开头的注释行。在这些注释中，你会找到一些建议的规则，这些规则提示了有用的配置，比如通过 `ftp-proxy` 实现的 FTP 透传（见 第三章）和 OpenBSD 的垃圾邮件延迟守护进程 `spamd`（见 第六章）。这些项在各种实际场景中可能有用，但由于它们在所有配置中并不总是相关，因此默认情况下被注释掉了。

如果你查看 */etc/rc.conf* 文件中的与 PF 相关的设置，你会找到 `pf_rules=` 设置。原则上，这让你可以指定你的配置文件位于默认的 */etc/pf.conf* 之外。然而，改变这个设置可能不值得麻烦。使用默认设置可以让你利用一些自动化管理功能，比如将配置文件自动备份到 */var/backups*。

在 OpenBSD 中，*/etc/rc* 脚本内置了一种机制，如果你在没有 *pf.conf* 文件或文件中包含无效规则集的情况下重启，它可以帮助你。在启用任何网络接口之前，*rc* 脚本加载一个规则集，允许一些基本服务：从任何地方的 SSH 连接、基本的名称解析和 NFS 挂载。这使得你可以登录并修正规则集中的任何错误，加载修正后的规则集，然后继续工作。

### 在 FreeBSD 上设置 PF

好的代码传播得很快，FreeBSD 用户会告诉你，其他地方的好代码最终都会找到通向 FreeBSD 的路。PF 也不例外，从 FreeBSD 5.2.1 和 4.*x* 系列版本开始，PF 和相关工具成为了 FreeBSD 的一部分。

如果你阅读了关于在 OpenBSD 上设置 PF 的前一节，你会发现，在 OpenBSD 上 PF 默认是启用的。但在 FreeBSD 上情况不同，PF 是三种可能的包过滤选项之一。在这里，你需要采取明确的步骤来启用 PF，与 OpenBSD 相比，你似乎需要在*/etc/rc.conf*中做更多的配置。从*/etc/defaults/rc.conf*文件来看，FreeBSD 中 PF 相关设置的默认值如下：

```
pf_enable="NO"                 # Set to YES to enable packet filter (PF)
pf_rules="/etc/pf.conf"        # rules definition file for PF
pf_program="/sbin/pfctl"       # where pfctl lives
pf_flags=""                    # additional flags for pfctl
pflog_enable="NO"              # set to YES to enable packet filter logging
pflog_logfile="/var/log/pflog" # where pflogd should store the logfile
pflog_program="/sbin/pflogd"   # where pflogd lives
pflog_flags=""                 # additional flags for pflogd
pfsync_enable="NO"             # expose pf state to other hosts for syncing
pfsync_syncdev=""              # interface for pfsync to work through
pfsync_ifconfig=""             # additional options to ifconfig(8) for pfsync
```

幸运的是，你可以安全地忽略其中的大部分内容——至少目前是这样。以下是你需要添加到*/etc/rc.conf*配置中的唯一选项：

```
pf_enable="YES"       # Enable PF (load module if required)
pflog_enable="YES"    # start pflogd(8)
```

在 FreeBSD 的不同版本中，PF 有一些差异。请参阅*FreeBSD 手册*，该手册可从*[`www.freebsd.org/`](http://www.freebsd.org/)*获取——特别是“防火墙”章节中的 PF 部分——以查看哪些信息适用于你的情况。FreeBSD 9 和 10 中的 PF 代码与 OpenBSD 4.5 中的代码等效，只有一些 bug 修复。本书中的说明假设你正在运行 FreeBSD 9.0 或更新版本。

在 FreeBSD 上，PF 默认是作为内核可加载模块编译的。如果你的 FreeBSD 系统使用 GENERIC 内核，你应该能够使用以下命令启动 PF：

```
$ **sudo kldload pf**
$ **sudo pfctl -e**
```

假设你已经在*/etc/rc.conf*中添加了刚才提到的行，并创建了*/etc/pf.conf*文件，你也可以使用 PF 的*rc*脚本来运行 PF。以下命令启用 PF：

```
$ **sudo /etc/rc.d/pf start**
```

这将禁用包过滤：

```
$ **sudo /etc/rc.d/pf stop**
```

### 注意

*在 FreeBSD 上，* /etc/rc.d/pf *脚本至少需要在* /etc/rc.conf *中有一行`pf_enable="YES"`，并且需要一个有效的* /etc/pf.conf *文件。如果这两个要求中的任何一个没有满足，脚本将会退出并显示错误信息。在默认的 FreeBSD 安装中没有* /etc/pf.conf *文件，因此你需要在启用 PF 后重新启动系统之前创建一个。为了我们的目的，使用`touch`创建一个空的* /etc/pf.conf *文件就足够了，但你也可以从系统提供的* /usr/share/examples/pf/pf.conf *文件的副本开始。

提供的示例文件* /usr/share/examples/pf/pf.conf *没有任何活动的设置。它只有以`#`字符开头的注释行和被注释掉的规则，但它确实给你展示了一个工作规则集的预览。例如，如果你删除位于`set skip on lo`前面的`#`符号来取消注释该行，然后将文件保存为你的*/etc/pf.conf*，一旦启用 PF 并加载规则集，你的回环接口组将不会被过滤。然而，即使 PF 在你的 FreeBSD 系统上被启用，由于我们还没有编写实际的规则集，PF 也没有做什么，所有数据包都会通过。

截至本文撰写时（2014 年 8 月），FreeBSD 的*rc*脚本未设置默认规则集作为回退选项，如果从*/etc/pf.conf*读取的配置无法加载。这意味着，如果启用 PF 时没有规则集，或者*pf.conf*文件的内容在语法上无效，PF 将启用并应用默认的`pass all`规则集。

### 在 NetBSD 上设置 PF

在 NetBSD 2.0 中，PF 作为一个可加载的内核模块提供，可以通过软件包（*security/pflkm*）安装，或者编译到静态内核配置中。在 NetBSD 3.0 及更高版本中，PF 是系统的基础部分。在 NetBSD 中，PF 是多种数据包过滤系统之一，你需要采取明确的措施来启用它。

一些 PF 配置的细节在 NetBSD 的不同版本之间发生了变化。本书假设你使用的是 NetBSD 6.0 或更高版本。^([10])

要在 NetBSD 上使用可加载的 PF 模块，请将以下行添加到*/etc/rc.conf*中，以分别启用可加载的内核模块、PF 和 PF 日志接口。

```
lkm="YES" # do load kernel modules
pf=YES
pflogd=YES
```

若要手动加载*pf*模块并启用 PF，请输入以下命令：

```
$ **sudo modload /usr/lkm/pf.o**
$ **sudo pfctl -e**
```

另外，你可以运行*rc.d*脚本来启用 PF 和日志记录，方法如下：

```
$ **sudo /etc/rc.d/pf start**
$ **sudo /etc/rc.d/pflogd start**
```

若要在启动时自动加载模块，请将以下行添加到*/etc/lkm.conf*文件中：

```
/usr/lkm/pf.o - - - - BEFORENET
```

如果你的*/usr*文件系统位于单独的分区上，请将以下行添加到*/etc/rc.conf*中：

```
critical_filesystems_local="${critical_filesystems_local} /usr"
```

如果此时没有错误，说明你已在系统上启用了 PF，并且可以继续创建完整的配置。

提供的*/etc/pf.conf*文件不包含任何活动设置；它只有以井号（`#`）开头的注释行和被注释掉的规则。不过，它确实给你提供了一个工作规则集的预览。例如，如果你去掉`set skip on lo`那一行前的井号以取消注释，并保存文件，那么在启用 PF 并加载规则集后，你的回环接口将不会被过滤。然而，即使在你的 NetBSD 系统上启用了 PF，我们还没有编写实际的规则集，所以 PF 实际上并没有做任何事情，只是传递数据包。

NetBSD 通过文件*/etc/defaults/pf.boot.conf*实现了默认或回退规则集。此规则集仅用于在*/etc/pf.conf*文件不存在或包含无效规则集时，帮助系统完成启动过程。你可以通过在*/etc/pf.boot.conf*中添加自定义规则来覆盖默认规则。

## 简单的 PF 规则集：单台独立机器

主要为了提供一个通用的、最小的基准，我们将从最简单的配置开始构建规则集。

### 最小规则集

最简单的 PF 设置是在一台不会运行任何服务、只与一个网络（可能是互联网）通信的单一计算机上。

我们将从一个类似下面的*/etc/pf.conf*文件开始：

```
block in all
pass out all keep state
```

该规则集拒绝所有进入流量，允许我们发送的流量，并保持我们连接的状态信息。PF 从上到下读取规则；规则集中与数据包或连接匹配的*最后*一条规则是被应用的规则。

在这里，来自任何其他地方进入我们系统的任何连接都会匹配`block in all`规则。即使有了这个初步结果，规则评估将继续进行到下一条规则（`pass out all keep state`），但流量不会匹配到这条规则中的第一个标准（即`out`方向）。由于没有更多的规则可以评估，状态不会发生变化，流量将被阻塞。以类似的方式，任何从具有此规则集的机器发起的连接都不会匹配第一条规则（再次是错误的方向），但会匹配第二条规则，这是一条`pass`规则，连接将被允许通过。

我们将在第三章中，结合一个稍长的规则集，更详细地探讨 PF 如何评估规则以及规则顺序的重要性。

对于任何包含`keep state`部分的规则，PF 会保持有关连接的信息，包括各种计数器和序列号，作为*状态表*中的一项条目。状态表是 PF 保存已匹配规则的现有连接的信息的地方，新的到达数据包会首先与现有的状态表条目进行比较以查找匹配。只有当数据包与任何现有状态不匹配时，PF 才会进行完整的*规则集评估*，检查数据包是否与加载的规则集中的某条规则匹配。我们还可以指示 PF 以各种方式处理状态信息，但在这种简单的情况下，我们的主要目标是允许我们发起的连接的返回流量返回给我们。

请注意，在 OpenBSD 4.1 及更高版本中，`pass`规则的默认行为是保持状态信息，^([11])，我们在这种简单情况下不再需要显式地指定`keep state`。这意味着规则集可以写成这样：

```
# minimal rule set, OpenBSD 4.1 onward keeps state by default
block in all
pass out all
```

实际上，如果你愿意，甚至可以省略这里的`all`关键字。

其他 BSD 系统现在大多数已经跟上了这个变化，接下来的部分我们将坚持使用较新的规则，如果你正在使用旧系统，偶尔会提醒你。

不言而喻，允许来自特定主机的所有流量通过意味着该主机是可信任的。只有在你确信可以信任该机器时，才会这么做。

当你准备好使用此规则集时，使用以下命令加载：

```
$ **sudo pfctl -ef /etc/pf.conf**
```

规则集应该能够加载而不显示任何错误消息或警告。在除最慢的系统外，应该会立即返回到`$`提示符。

### 测试规则集

测试规则集以确保它们按预期工作始终是一个好主意。当你转向更复杂的配置时，适当的测试变得至关重要。

要测试这个简单的规则集，看看它是否能够执行域名解析。例如，你可以检查`$ host nostarch.com`是否返回信息，如主机*nostarch.com*的 IP 地址和该域名邮件交换器的主机名。或者直接看看你是否能上网。如果你能够通过域名连接到外部网站，那么这个规则集就允许你的系统执行域名解析。基本上，你尝试从自己的系统访问的任何服务都应该能正常工作，而你尝试从另一台机器访问系统中的任何服务则应该产生`Connection refused`消息。

## 稍微严格一点：使用列表和宏来提高可读性

上一节中的规则集是一个极其简单的规则集——可能对于实际使用来说太过简化。但它是一个很好的起点，可以在此基础上构建出稍微更有结构和完整的配置。我们将从拒绝所有服务和协议开始，然后只允许我们知道需要的那些，^([12])，并使用列表和宏来提高可读性和控制性。

*列表*只是指两个或更多相同类型的对象，你可以在规则集中引用它们，如下所示：

```
pass proto tcp to port { 22 80 443 }
```

这里，`{ 22 80 443 }`就是一个列表。

*宏*是一个纯粹的可读性工具。如果你在配置中有多次引用的对象，例如一个重要主机的 IP 地址，那么定义一个宏可能会很有用。例如，你可以在规则集中早期定义这个宏：

```
external_mail = 192.0.2.12
```

然后，你可以在规则集中稍后引用这个主机，写成`$external_mail`：

```
pass proto tcp to $external_mail port 25
```

这两种技术在保持规则集的可读性方面具有巨大潜力，因此，它们是有助于实现保持对网络控制的总体目标的重要因素。

### 一个更严格的基础规则集

到目前为止，我们在处理我们自己生成的任何流量时相对宽松。宽松的规则集在检查基本连通性是否正常或检查过滤是否是我们遇到的问题的一部分时非常有用。一旦“我们有连通性吗？”的阶段结束，就该开始收紧规则，创建一个我们能够掌控的基础规则集。

首先，将以下规则添加到*/etc/pf.conf*：

```
block all
```

这个规则是完全限制性的，它将阻止所有方向的流量。这是我们将在接下来几章中使用的所有完整规则集的初始基础过滤规则。我们基本上是从零开始，配置一个*不允许*任何流量通过的规则。稍后，我们将添加一些规则，放宽流量限制，但我们会逐步进行，并确保始终保持对系统的控制。

接下来，我们将定义一些宏，以便在规则集中后续使用：

```
tcp_services = "{ ssh, smtp, domain, www, pop3, auth, https, pop3s }"
udp_services = "{ domain }"
```

在这里，你可以看到列表和宏的结合如何对我们有利。宏可以是列表，正如示例中所演示的，PF 理解使用服务名称和端口号的规则，这些服务名称和端口号列在你的 */etc/services* 文件中。我们将小心使用所有这些元素以及一些进一步提高可读性的技巧，来处理那些需要更复杂规则集的复杂情况。

定义了这些宏之后，我们可以在规则中使用它们，接下来我们将稍微编辑规则，使其如下所示：

```
block all
pass out proto tcp to port $tcp_services
pass proto udp to port $udp_services
```

字符串 `$tcp_services` 和 `$udp_services` 是宏引用。规则集中出现的宏会在规则集加载时展开，运行中的规则集会在引用宏的地方插入完整的列表。根据宏的具体性质，它们可能导致带有宏引用的单一规则展开为多个规则。即使在像这样的小规则集中，使用宏也使得规则更易于理解和维护。规则集中需要显示的信息量减少，且通过合理的宏名称，逻辑变得更清晰。在典型规则集的逻辑中，大多数时候我们不需要在每个宏引用的位置看到完整的 IP 地址或端口号列表。

从实际的规则集维护角度来看，重要的是要记住允许哪些服务使用哪些协议，以保持一个适当的控制状态。根据协议将允许的服务分开列出，很可能有助于保持规则集既功能完备又易于阅读。

TCP 与 UDP

我们已经小心地将 UDP 服务与 TCP 服务分开。几个服务主要运行在 TCP 或 UDP 上的知名端口号上，一些服务则根据特定条件在 TCP 和 UDP 之间切换。

这两种协议在多个方面有所不同。TCP 是面向连接的，并且可靠，是进行有状态过滤的完美候选。而 UDP 是无状态的、无连接的，但 PF 会为 UDP 流量创建并维护等同于状态信息的数据，以确保如果返回的 UDP 流量与现有状态匹配，则允许其通过。

一个常见的 UDP 状态信息有用的例子是处理名称解析。当你请求一个名称服务器将域名解析为 IP 地址，或将 IP 地址解析回主机名时，合理的假设是你希望收到答案。保留 UDP 流量的状态信息，或其功能等效物，可以实现这一点。

### 重新加载规则集并查找错误

在我们修改了 *pf.conf* 文件之后，需要按如下方式加载新规则：

```
$ **sudo pfctl -f /etc/pf.conf**
```

如果没有语法错误，`pfctl` 在加载规则时不应显示任何消息。

如果你更喜欢显示详细输出，可以使用 `-v` 标志：

```
$ **sudo pfctl -vf /etc/pf.conf**
```

当你使用详细模式时，`pfctl` 应该会在返回命令行提示符之前，将你的宏展开为各自的规则，如下所示：

```
$ **sudo pfctl -vf /etc/pf.conf**
tcp_services = "{ ssh, smtp, domain, www, pop3, auth, https, pop3s }"
udp_services = "{ domain }"
block drop all
pass out proto tcp from any to any port = ssh flags S/SA keep state
pass out proto tcp from any to any port = smtp flags S/SA keep state
pass out proto tcp from any to any port = domain flags S/SA keep state
pass out proto tcp from any to any port = www flags S/SA keep state
pass out proto tcp from any to any port = pop3 flags S/SA keep state
pass out proto tcp from any to any port = auth flags S/SA keep state
pass out proto tcp from any to any port = https flags S/SA keep state
pass out proto tcp from any to any port = pop3s flags S/SA keep state
pass proto udp from any to any port = domain keep state
$ _
```

将此输出与您实际编写的*/etc/pf.conf*文件的内容进行比较。我们的单个 TCP 服务规则扩展为八个不同的规则：每个服务都有一个对应的规则。单个 UDP 规则只处理一个服务，并且它从我们写的内容扩展到包括默认选项。请注意，规则被完整地显示出来，默认值如`flags S/SA keep state`已应用到你未明确指定的任何选项。这就是实际加载的配置。

### 检查你的规则

如果你对规则集做了大量更改，在尝试加载规则集之前，使用以下命令检查它们：

```
$ pfctl -nf /etc/pf.conf
```

`-n`选项告诉 PF 仅解析规则，而不加载它们——这基本上是一次模拟运行，可以让你检查和纠正任何错误。如果`pfctl`在规则集中发现任何语法错误，它将退出并显示错误信息，指明错误发生的行号。

一些防火墙指南建议你确保旧的配置已被完全删除，否则你可能会遇到问题——你的防火墙可能处于某种中间状态，这种状态既不符合之前的状态，也不符合之后的状态。使用 PF 时，这种情况完全不成立。最后加载的有效规则集会一直处于活动状态，直到你禁用 PF 或加载新的规则集。`pfctl` 会检查语法，然后在切换到新规则集之前完全加载新的规则集。这通常被称为*原子规则集加载*，意味着一旦有效的规则集加载完毕，就不会有部分规则集或没有加载规则的中间状态。一个后果是，匹配旧规则集和新规则集中都有效的状态的流量不会被中断。

除非你真的按照一些旧指南的建议，*刷新*了现有的规则（这确实可以通过使用`pfctl -F all`或类似命令实现），然后再尝试从配置文件加载新的规则，否则最后有效的配置将继续保持加载。实际上，刷新规则集通常不是一个好主意，因为它实际上将你的数据包过滤器置于`pass all`模式，这样既会为任何流量打开大门，又可能在你准备加载新规则时中断有用的流量。

### 测试已更改的规则集

一旦你有了一个`pfctl`能加载且没有任何错误的规则集，就该检查你编写的规则是否按预期工作了。像我们之前做的那样，使用命令`$ host nostarch.com`测试名称解析应该仍然能正常工作。不过，最好选择一个你最近没有访问过的域名，比如你不会考虑投票给的某个政党，这样可以确保你没有从缓存中拉取 DNS 信息。

你应该能够浏览网页并使用几个与邮件相关的服务，但由于这个更新的规则集的性质，任何尝试访问除已定义的 TCP 服务（如 SSH、SMTP 等）以外的远程系统服务应该会失败。就像我们简单的规则集一样，系统应拒绝所有不匹配现有状态表条目的连接；只有由本机发起的连接的返回流量才会被允许进入。

## 显示有关系统的信息

你对规则集进行的测试应该已经显示 PF 正在运行，并且规则行为符合预期。有几种方法可以跟踪运行中的系统中发生的事情。提取 PF 信息的其中一种更直接的方式是使用已经熟悉的`pfctl`程序。

一旦 PF 启用并运行，系统会根据网络活动更新各种计数器和统计信息。要确认 PF 是否正在运行并查看其活动的统计信息，可以使用`pfctl -s`，后面跟上你想显示的信息类型。可以显示的信息类型有很多种（请参阅`man 8 pfctl`并查找`-s`选项）。我们将在第九章中回到这些显示选项，并在第十章中更详细地讨论它们提供的一些统计信息，我们将利用这些数据来优化我们正在构建的配置。

以下是`pfctl -s info`输出的一个例子（摘自我的家庭网关）。显示系统实际传输流量的高层信息可以在这部分找到。

```
**$ sudo pfctl -s info**
Status: Enabled for 24 days 12:11:27                Debug: err

Interface Stats for nfe0               IPv4               IPv6
  Bytes In                      43846385394                  0
  Bytes Out                     20023639992                 64
  Packets In
    Passed                          49380289                 0
    Blocked                            49530                 0
  Packets Out
    Passed                          45701100                 1
    Blocked                             1034                 0

State Table                            Total              Rate
  current entries                        319
  searches                         178598618            84.3/s
  inserts                            4965347             2.3/s
  removals                           4965028             2.3/s
```

`pfctl`输出的第一行表明 PF 已经启用，并且运行了稍多于三周的时间，这与我上次进行需要重启的系统升级的时间相等。

显示中的`Interface Stats`部分表明系统管理员选择了一个接口（此处为`nfe0`）作为系统的日志接口，并显示该接口处理的进出字节。如果没有选择日志接口，则显示会稍有不同。现在是检查系统输出的好时机。接下来的几项可能会更引人兴趣，在我们的上下文中，它们显示了每个方向上被阻止或通过的数据包数量。在这里，我们可以看到过滤规则是否有效的初步迹象。在这个例子中，规则集要么很好地匹配了预期的流量，要么我们有相当守规矩的用户和访客，在两个方向上，通过的数据包数量远大于被阻止的数据包数量。

接下来，系统处理流量的另一个重要指标是 `状态表` 统计信息。状态表的 `当前条目` 行显示有 319 个活动状态或连接，而状态表平均每秒搜索匹配现有状态的次数略多于 84 次，自计数器重置以来，总共进行了超过 1.78 亿次搜索。`插入` 和 `移除` 计数器显示了状态被创建和删除的次数。如预期所示，插入和移除的次数与当前活动状态的数量不同，速率计数器显示，自计数器最后重置以来，创建和删除状态的速率与此显示的分辨率完全一致。

这里的信息大致与配置为仅支持 IPv4 的小型网络网关上你应当看到的统计数据一致。IPv6 列中的数据包传递不必惊慌。OpenBSD 内置了 IPv6。在网络接口配置期间，默认情况下，TCP/IP 堆栈会发送 IPv6 邻居发现请求，用于链路本地地址。在一个正常的仅 IPv4 配置中，只有前几个数据包实际上会通过，等到来自*/etc/pf.conf*的 PF 规则集完全加载时，IPv6 数据包会被默认的“阻止所有”规则拦截。（在这个示例中，它们不会出现在 `nfe0` 的统计信息中，因为 IPv6 是通过不同的接口进行隧道传输的。）

## 展望未来

现在你应该有一台能够与其他联网机器通信的机器，使用一个非常基本的规则集，它作为控制网络流量的起点。随着你阅读本书，你将学习如何添加执行各种有用操作的规则。在第三章中，我们将扩展配置，使其充当一个小型网络的网关。为几台计算机提供服务会有一些后果，我们将研究如何至少允许某些 ICMP 和 UDP 流量通过——如果没有别的，至少用于你自己的故障排除需求。

在第三章中，我们还将考虑对你的安全有影响的网络服务，如 FTP。智能使用数据包过滤来处理那些安全要求较高的服务，是本书中的一个反复出现的主题。

* * *

^([9]) 如果你在设置 OpenBSD 版本低于这个版本的第一个 PF 配置，最好的建议是升级到最新的稳定版本。如果由于某种原因你必须继续使用旧版本，查阅本书的第一版以及你使用的特定版本的 man 页和其他文档可能会有所帮助。

^([10]) 有关在早期版本中使用 PF 的说明，请参阅你所使用版本的文档，并查阅本书附录 A 中列出的相关资料。

^([11]) 事实上，新的默认设置对应于`保持状态标志 S/SA`，确保只有在连接建立过程中初始的 SYN 数据包会创建状态，从而消除了某些令人困惑的错误场景。为了无状态地过滤，你可以为那些不想记录或保留状态信息的规则指定`no state`。在 FreeBSD 中，OpenBSD 4.1 等效的 PF 代码已被合并到 7.0 版本中。如果你正在使用一个较旧的 PF 版本，且它没有这个默认设置，这强烈表明你应该尽快考虑升级操作系统。

^([12]) 为什么要将规则集设置为默认拒绝？简短的答案是，这样能让你更好地控制。数据包过滤的目的是掌控局面，而不是在坏人行动之后再做补救。Marcus Ranum 写过一篇非常有趣且富有启发性的文章，名为《计算机安全中的六大愚蠢想法》(*[`www.ranum.com/security/computer_security/editorials/dumb/index.html`](http://www.ranum.com/security/computer_security/editorials/dumb/index.html)*)。
