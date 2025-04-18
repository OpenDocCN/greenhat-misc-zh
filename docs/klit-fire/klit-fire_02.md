# 第二章：食人代码

如果技术是以周期形式发展的，你可能会认为最好的遗产现代化策略是等待十年或二十年，直到范式发生变化，再跳跃过去。要是能这样就好了！尽管大型主机和云计算在总体上可能有许多共同点，但它们在实施上有许多显著的差异，阻碍了它们之间的轻松过渡。尽管时间共享的架构理念已经重新流行，但技术的其他组成部分却在不同的节奏上进步。你可以将任何单一产品分解为无限多个元素：硬件、软件、接口、协议等。然后你可以在这些类别中添加特定的技术。不所有的周期都是同步的。现代技术与旧技术完美契合的几率，就像是找到两天每颗星星的确切位置完全相同一样。

因此，理解技术是以周期形式发展的要点不是升级等得越久就越容易，而是你应该避免仅仅因为技术是新的就去升级。

## 可对齐差异与用户界面

没有可对齐的差异，消费者无法判断他们被要求投资的技术的价值。完全创新的技术不是一个可行的解决方案，因为它没有参考点来帮助它找到市场。我们常常认为技术是简洁高效的，没有任何没有明确目的的冗余部分，但事实上，许多你依赖的技术形式都包含了遗留下来的特征，这些特征要么是从其他旧技术继承而来，要么是后来引入的，以制造功能相等的假象。

例如，大多数软件工程团队保持 80 列的代码行宽。短行代码比长行代码更容易阅读，这一点是事实。但为什么是 80 列呢？为什么不是 100 列呢？

奇妙的是，80 列宽度是旧时大型主机打孔卡的尺寸，这些卡片用于输入数据和程序到 20 世纪 50 年代和 60 年代建造的巨型计算机中。因此，现在，已经是 21 世纪，程序员们还在强制执行一个为他们大多数甚至未曾见过、何况是编程的机器而制定的标准。

那么，为什么主机打孔卡是 80 列宽的呢？最早计算机公司使用的打孔卡——当时它们是主要用于像人口普查这样的工作，还是机械“制表机”——是临时设计的，并且极其低效。它们被设计用来进行计数，而不是计算，因此它们的设计类似于铁路乘务员用来售票的卡片，而不是用于存储数据的卡片。^(1) 这些卡片需要批量输入机器，然后再进行排序和存储。为了避免重新发明一切，这些卡片本身的设计与当时美国纸币的尺寸大致相同：3¼英寸乘 7⅜英寸。这意味着公司可以重新利用现有的抽屉、箱子和盒子来获取所需的配件。

到了 1920 年代，客户开始要求 IBM 在一张卡片上获取更多的数据存储空间。IBM 的创新是改变了孔的形状，使其更接近矩形，这样它们可以更紧密地排列在卡片上。^(2) 这意味着可以在卡片上放置 80 列孔。

现在，我们更深入地探讨一下。那打孔卡本身呢？为什么第一代计算机设计要从带孔的硬卡片输入数据？键盘的出现几乎和打字机一样久远，第一台现代打字机由克里斯托弗·拉瑟姆·肖尔斯、卡洛斯·格里登和塞缪尔·W·索尔于 1868 年获得专利，几乎比一些主机的开发早了一个世纪。电报机甚至早于此就开始实验不同类型的键盘。那么，为什么人们宁愿在一张厚纸上打孔，而不是直接在键盘上输入信息呢？

键盘或类似的输入设备的问题在于，人类操作员很容易输入错误，尤其是当操作员没有任何视觉确认，无法确认他们认为输入的内容是否就是机器接收到的内容时。想象一下在一个隐藏输入内容的网页字段中输入密码。这样的密码隐藏字段的一个缺点是，如果你按错了键，可能直到系统拒绝你的输入时才会注意到。你有多少次输入错误密码？现在想象一下在没有看到自己输入内容的情况下输入一条完整的信息。操作员错误是电报系统中的一个大问题，尤其是当电报开始在全球传递重要信息时。

解决方案是使用键盘，但键盘并不是直接与电报接口，而是会生成一个可以在机器尝试发送信息之前检查错误的记录。基于这个概念，开发了许多不同的变体，最终被采用的是在纸带上打孔。

有趣的是，19 世纪末的打卡机时代和 20 世纪初期的早期计算机时代，它们以不同的方式达到了相同的解决方案。打卡机的穿孔卡片起源于铁路票，而电报的穿孔卡片则源于纺织行业。

一百多年前，法国的织布工通过在卡片上打印出一系列穿孔图案，并将这些卡片输入织布机，自动化复杂地毯的图案设计。这使得织布工能够更快速地生产高质量的产品，具有更高的艺术性和更大的准确性。

电报进一步改进了这一系统，引入了编码的概念。当目标是操作巨大的织布机中的线程，一行一行地创建复杂的图案时，过于复杂的设计就显得没有意义。每根提升的线对应一个孔，这就足够有效。

然而，当目标是发送远距离信息时，这种字面上的方式就显得低效。电报操作员已经习惯于使用代码来表示不同的字母，但这些代码是为了减少操作员的错误而优化的。例如，在摩尔斯电码中，最常见的字母具有较短的代码。这可以保持传输速度，并减少操作员的压力。一旦电报开始产生一份物理记录，操作员可以在发送信息之前进行二次或三次检查，那么在机器编码的优化方面，性能的最大提升便得以实现。在电码长度为 1 到 5 个单位之间的字母，机器处理起来并不容易。机器在每个字母的长度相等时表现得更好。现在最好的编码是那些稍微复杂一些的、长度固定的编码，最终能够存储更多的数据。

开发了几种不同的系统。第一个被广泛采用的是由埃米尔·博多（Emile Baudot）在 1870 年开发的。这个被称为博多码的系统，也叫国际电报字母表第 1 号，是一个 5 位二进制系统。

快速推进到早期计算机时代，人们开始开发巨大的房间大小的机器，这些机器也使用二进制系统。他们需要一种输入数据和指令的方式，但当时并没有可视界面。直到 1964 年，贝尔实验室才将第一款原始的可视界面融入到 Multics 时间共享系统中，计算机才开始与显示器配合使用。我们当时没有办法看到计算机接收的输入信息，因此我们借用了电报的接口，而电报的接口又借用了 18 世纪法国织布工的接口。

技术也是如此。它按照周期发展，但这些周期偶尔会碰撞、交叉或融合。我们不断借用我们在其他地方看到的想法，要么是为了改进我们的系统，要么是为了给用户一个参考点，使得他们采纳新技术变得更快、更容易。真正的新系统通常会吞并旧系统的接口，以创造可以对齐的差异。

这就是为什么长期维护技术如此困难的原因。虽然盲目追求新事物因为其新颖性而具有危险性，但不与时俱进也是危险的。随着技术的进步，它积累了越来越多的接口和模式。它从其他领域吸收这些元素，并保留了那些已经不再有意义的历史成分。它围绕最深藏的特性建立假设。如果你的系统保持不变太久，你就会陷入迁移数十年假设的困境。

## Unix 吃掉了世界

一个常见的建议是，构建成功软件时要保持简单。但究竟是什么让一个设计看起来简单，而另一个设计却显得复杂呢？为什么一行 80 个字符的代码看起来更简单、更易读？它很简短，但如果我告诉你，用户体验研究实际上把理想的字符数定在 50 到 60 个字符之间呢？这意味着 80 个字符比实际测试中效果最好的长度长了 50%。

人类的大脑对熟悉的事物有强烈的偏见。我们把已经知道的概念和构造看作更简单、更容易、更高效，仅仅因为它们对我们来说是已知且舒适的。我们不需要成为某个构造的专家，甚至不一定要喜欢它，熟悉感就会改变我们对它的认知。20 世纪 60 年代，心理学家罗伯特·扎扬茨进行了一系列实验，记录了即使是对某物的单次接触，也能增加我们在后续接触中的正面情绪。他在语言、单词和图像上都发现了这一效应。后来的研究者也观察到了类似的偏好，比如金融专业人士如何进行投资^(3)，学术研究人员如何评估期刊^(4)，以及我们在吃东西时喜欢什么味道^(5)。在心理学中，这个现象被称为*单纯接触效应*。仅仅接触某个概念，会让大脑更容易处理这个概念，因此，用户会觉得它更容易理解。

因此，开发新技术或振兴旧系统最有效的方式往往是建立在熟悉的概念之上。参考点创造了可以对齐的差异，帮助我们评估新事物的价值，但这些相同的参考点也使新技术显得简单易懂，降低了进入的门槛，提高了其被采纳的可能性以及采纳的速度。

考虑一下 Linux 操作系统。它很可能是目前最受欢迎的网络服务器操作系统之一，甚至在计算机领域也是如此。目前有数百个版本可以自由安装，而且还有许多专业版本。Linux 是在激烈的竞争中脱颖而出的无可争议的胜者，它的目标是开发一个既能在多种不同类型的计算机上运行，又不受限制许可证约束的操作系统。

Linux 常被描述为最受欢迎的 Unix 操作系统版本，尽管这两个操作系统在实现方面几乎没有任何相似之处。

Linux 的故事始于 1982 年贝尔系统的解体，距其诞生将近十年。1956 年对 AT&T 的一项同意判令禁止该电信巨头从事“任何除提供公共通信服务以外的业务”。这意味着，当贝尔实验室的计算机科学家 Dennis Ritchie、Ken Thompson 和 Rudd Canaday 在 1970 年代开始开发 Unix 时，没有人确定 AT&T 是否被允许出售它。AT&T 的律师们决定采取保守态度，允许将其源代码和软件一同出售给学术和研究机构。^(6)

拥有源代码使得将 Unix 移植到不同的机器上变得容易，也可以对其进行修改和调试。人们将其打印出来并附上自己的注释。Unix 成为教学中一种便捷的选择，帮助学生理解操作系统是如何工作的。它在各种不同的机构中迅速传播开来，包括大学、博物馆、政府组织，甚至早期还有一所全女子私立学校。

用户开始将他们修改过的 Unix 版本放在磁带上，并相互分发。这些本质上是“分叉”和“拉取请求”，远在这种基础设施出现之前。分享的主要动机是分发错误修复和补丁。

与此同时，AT&T 的律师们正在努力决定如何处理 Unix，并且他们在原始的决策和更为传统的知识产权限制方法之间摇摆不定。Unix 历史学家 Peter Salus 讲述了 AT&T 的开发者是如何积极参与盗版自己知识产权的故事。

> *大量的错误修复被收集起来，而不是一次性发布，每次修复都会由 Ken [Thompson] 汇总成一个修复带。一些修复非常重要……我怀疑相当一部分修复实际上是由非贝尔公司的人完成的。Ken 尝试发布，但律师们一直拖延，拖延，再拖延。*
> 
> *最终，出于完全的厌恶，有人“发现”了一盘在 Mountain Avenue [贝尔实验室的地址是 600 Mountain Avenue, Murray Hill, NJ] 上的磁带，其中包含了这些修复。*
> 
> *当律师们得知此事后，他们打电话给每一个许可证持有者，威胁如果不销毁录音带，他们将面临严重后果……并试图找出他们是如何得到这盘录音带的。我猜没有人会真正告诉他们是如何得到录音带的（我没有）。这是 AT&T 律师们为了证明自己存在价值并扼杀 UNIX 的第一次尝试。^(7)*

当那些在计算机科学课程中学习 UNIX 的大学生毕业并找到工作时，他们把 UNIX 带到了各自的工作岗位。随着每个新版本的推出，AT&T 的许可证变得越来越严格，公司试图弄清楚它在法律上能做些什么来利用这一意外形成的繁荣社区。

然后，在 1982 年，美国司法部解决了对电信行业的第二起反垄断案件，并拆分了“Ma Bell”。AT&T 突然摆脱了那项令其无法完全将 UNIX 视作产品的同意令，它毫不犹豫地开始严厉打压这个在十多年间逐渐壮大的社区。

如果你经历过类似的尝试来阻止分享其他形式的知识产权，比如音乐和电影，你就能理解一旦人们习惯了拥有一个免费且可修改的操作系统 UNIX 后，他们不愿放弃它，也不愿回到以前的状态。剥夺对 UNIX 源代码的访问迫使社区寻找一个开源的、理想情况下免费的替代品。

一个早期的竞争者是伯克利开发的 UNIX 变种，称为伯克利软件发行版（BSD）。BSD 拥有一个日益壮大的社区，但它的基础使用了 UNIX 的部分源代码，因此很快陷入了诉讼之中。UNIX 的继承者需要表现得像 UNIX，但又不包括 AT&T 的任何知识产权。

于是 Linux 诞生了，它是计算机科学学生 Linus Torvalds 作为个人项目开发的。Linux 从来没有意图成为一个完整的操作系统；它只打算成为针对特定芯片架构的内核，而 Torvalds 恰好有该架构的访问权限。因此，Linux 操作系统是由来自其他团队的各种软件拼凑而成的。它的大部分类 Unix 接口来自理查德·斯托尔曼的 GNU 项目，而 GNU 本身设计上并不包含任何 UNIX 代码。

所以在某种意义上，Linux 是 UNIX 的后代，但它没有直接使用 UNIX 的任何代码。但，为什么要坚持保持 UNIX 的外观和感觉呢？一旦决定开始编写一个完全新的系统，那么保持看起来像 UNIX 的形式有什么价值呢？对斯托尔曼来说，情况很明确：自由软件是一项道德使命。目标不是建立一个免费的 UNIX 替代品，而是建立一个免费的*替代品*，完全取代并淘汰 UNIX。他毫不犹豫地将 GNU 项目的策略描述为极端：

> *随着 GNU 项目声誉的增长，人们开始主动为该项目捐赠运行 Unix 的机器。这些机器非常有用，因为开发 GNU 组件最简单的方式就是在 Unix 系统上进行，然后逐个替换该系统的组件。但是它们也提出了一个伦理问题：我们是否应该拥有 Unix 的副本？*
> 
> *Unix 是（并且仍然是）专有软件，而 GNU 项目的哲学认为我们不应该使用专有软件。但是，运用与自卫中暴力行为正当化相同的推理，我得出结论，当使用专有软件对开发一个可以帮助他人停止使用该专有软件的自由替代品至关重要时，使用专有软件是合法的。*
> 
> *但是，即使这是一个可以辩解的邪恶，它仍然是一个邪恶。今天我们不再拥有任何 Unix 的副本，因为我们已经用免费的操作系统取而代之。如果我们无法用免费的操作系统替代一台机器的操作系统，我们就换掉了那台机器。^(8)*

Stallman 使用 Unix 的接口，因为他明白，如果 GNU 的接口与现有软件的接口匹配，专有软件的用户将有更大的动力去切换。^(9)

让我们再深入一层：为什么 Unix 最初有它现在这样的接口？大多数 Unix 命令是两个字母的缩写，代表那些似乎不需要缩写的词。《The UNIX-HATERS Handbook》的作者将这种接口归因于 Unix 创建者当时可用的硬件：

> *初学 Unix 的用户总是对 Unix 命令名称的选择感到惊讶。无论在 DOS 或 Mac 上接受多少培训，都无法为那些神秘而美丽的两个字母的命令名称如 cp、rm 和 ls 做好准备。*
> 
> *我们这些使用过 70 年代早期 I/O 设备的人怀疑，退化的根源在于 ASR-33 电传打字机的速度、可靠性，以及最重要的，它的键盘，ASR-33 是当时常见的输入输出设备。与今天的键盘不同，今天的键盘按键行程基于反馈原理，所需的力量仅仅是关闭微动开关的力量，而电传打字机上的按键（至少在记忆中）需要移动超过半英寸，并且需要足够的力量来驱动一个小型电动发电机，就像自行车上的发电机一样。你在这些怪物上打字时，手指关节可能会受伤。*
> 
> *如果 Dennis 和 Ken 使用的是 Selectric 而不是电传打字机，我们可能会打出“copy”和“remove”，而不是“cp”和“rm”。再次证明，技术往往限制我们的选择，而不仅仅是扩展它们。*
> 
> *经过二十多年，继续延续这一传统的理由是什么？历史的强大力量，也就是现有的代码和书籍。如果一个厂商用比如说 remove 替代了 rm，那么每一本描述 Unix 的书籍将不再适用于它的系统，而每个调用 rm 的 shell 脚本也将不再适用。这样的厂商不如直接停止实现 POSIX 标准。*
> 
> *一个世纪前，快速打字员正在使他们的键盘卡住，因此工程师设计了 QWERTY 键盘来减慢他们的速度。计算机键盘不会卡住，但我们今天仍然在使用 QWERTY。一个世纪后，世界依然会在使用 rm。^(10)*

就像程序员现在写的代码行适合打孔卡片一样，他们也使用那些接口设计上最适合电传打字机键盘的操作系统。利用熟悉的结构来促进技术的普及可能会创造出奇怪的传统。

## 继承路径

如果人们更快地接受遵循已知模式的技术，即使他们讨厌这些模式，也值得探讨人们最初是如何接触到这些模式的。从一开始，计算机行业就是一个跨功能的行业。围绕计算机的开发以及最可能使用计算机来做其他工作的职业，形成了人们的网络。在计算机的早期，这意味着计算机用户既是构建应用程序、开发语言和设计架构的计算机科学家，*也是*像科学家、数学家和银行家这样的专业人士。即使在今天，这些群体仍然倾向于将自己孤立起来，限制了他们接触为其他用例创建的接口。

请考虑以下情况：最早期的成功编程语言之一是 COBOL，然而现代编程语言几乎没有继承 COBOL 的设计模式。例如，我们不会将代码划分为不同的部分，也不会使用句点来结束代码行。很少有程序员会猜到 PIC 是一个可变字符字符串。COBOL 的一些特性出现在其他语言中，但它的语法和接口几乎没有保留下来。相反，COBOL 自己则采纳了许多后来的语言结构，试图清理它的设计。

另一方面，ALGOL60 深刻地影响了几乎所有现代语言的结构和语法，但今天你很难找到一个程序员曾经听说过它。^(11)

当我们审视各种编程语言的成就时，COBOL 显然是赢家。COBOL 程序至今仍然处理着数百万笔交易和数万亿美元的资金流动，从 A 点到 B 点。很难提到 ALGOL60 曾经实现过的任何具有重大意义的事物。与 ALGOL60 同样有影响力且不为人知的语言 BCPL，幸存下来并成为 C 语言的祖先。那么，早期计算机科学家们怎么会比第一种真正成功的跨平台高级编程语言的模式更熟悉那些失败语言的模式呢？

答案是，COBOL 是一种为那些不想理解计算机如何工作的人的需求而设计的语言；他们只是想完成工作。当数据系统语言委员会（CODASYL）在开发 COBOL 时，那些致力于计算机研究与开发的人认为，你应该学习适用于你特定机器的汇编语言。让编程更易于访问、让代码更具人类可读性被视为一种反模式，认为这种做法是在降低编程的美感，迎合不值得的观众。

然而，这些观众实际上是那些为了实际目的而使用计算机的人，他们中的许多人对每次升级机器时都必须重写程序的想法感到无聊。这个群体的人不在乎是否是“真正的程序员”。他们关心的是比竞争对手做得更好、更快。如果可能的话。技术正确性不重要，优雅不重要，执行才是关键，任何能降低使用计算机执行目标的门槛的东西，都比那些更强大但更难学习的工具更可取。

这一时期的计算机科学家们有着相反的动机。尽管 COBOL 用户根据他们通过计算机更快地完成非技术性任务的能力来评判和奖励，但 ALGOL60 用户则根据他们扩展机器原本能做的功能的能力来评判和奖励。通常，这一领域有两种成就类型：让机器做一些新的事情，或者让机器比以前更高效地完成某些事情。对于计算机科学家来说，编程语言*本身就是*输出。开发完成后，下一步不是编写程序，而是撰写关于该语言的论文，并与其他学者分享以获取反馈和进行研究。

大致上，从 1950 年代到 1970 年代之间，有三种人群在编程计算机：科学家和数学家、数据处理人员，以及学者或计算机研究人员。

**科学家和数学家**用计算机进行计算，他们更倾向于使用尽可能反映科学和数学符号的语言。这个群体使得 FORTRAN 广为人知。当达特茅斯的两位数学教授希望创建一种更容易让学生学习的编程语言时，他们大量借鉴了 FORTRAN II 的语法，开发出了 BASIC。BASIC 后来衍生出了数百种变种，其中许多至今仍在使用。

**数据处理人员**使用计算机从一个源读取数据，然后进行计算或以某种方式转换数据，再保存到另一个源。这些正是 COBOL 的用户，而这种语言证明了它的有效性，至今仍在使用。

如果你想证明采用决策受人们网络间共享知识而非严格凭借优点的影响，考虑这一点：今天那些试图替换旧的 COBOL 应用程序的组织，并没有将其迁移到现代编程语言中最适合数据处理的首选语言——Python，而是迁移到继承了 COBOL 作为企业通用语言市场的语言——Java。

语言的设计从来都不是最重要的，重要的是人群。那些原本会成为 COBOL 程序员的人，现在正成为 Java 程序员，这使得 Java 成为自然的选择，尽管它并不是为了处理 COBOL 所优化的用例而设计的。

也许这就是为什么 COBOL 仍然在许多地方存在，并且抵抗了所有试图淘汰它的努力。

**学者和计算机研究人员**专注于计算机的发展。当他们最终从汇编语言转移时，他们转向了专门用于文档化和实现算法的语言。ALGOL60 可能没有被用来构建很多应用程序，但它是计算机协会（ACM）用于在教科书和学术资源中描述算法的语言，超过了 30 年。这使得它对研究人员后续开发的语言产生了强大的影响。

剑桥大学基于 ALGOL60 开发了剑桥编程语言（CPL）。CPL 后来发展为 BCPL，BCPL 被简化以创建 B，进一步修改后又形成了 C。接着，C 成为了这一群体的首选编程语言，并促成了大量编程语言的开发，这些语言被各种各样的程序员使用：Java、Go、PHP（通过 Perl）、Ruby、Python 和 Swift。

对这一群体来说，Lisp 也很受欢迎。因为最初的 Lisp 只是一个理论设计文档，直到今天，不同的实现层出不穷，紧随其后的是无果的标准化尝试。在 1960 和 1970 年代，Lisp 与人工智能研究紧密相关，并且基本上被归类为这一领域的利基技术。具有讽刺意味的是，在我们的计算时代，人工智能取得了更多的进展，但 Lisp 几乎没有发挥关键作用。相反，今天的 Lisp 被看作是一类通用编程语言，偶尔将一些思想和结构注入到更主流的语言中。

所以，计算机科学历史上的这一关键时刻，出现了两类人群，他们编程是为了实现一些与计算机本身无关的实际目的，还有一类人群则与计算机合作，推动计算机本身能够做的事情的边界。现存的大多数编程语言保留了这些第三类程序员熟悉的构造，尽管 COBOL、FORTRAN 和 BASIC 拥有更广泛的用户群体。

总体而言，接口和理念通过人际网络传播，而不是基于优点或成功。接触到某种配置会产生一种认为它更容易且更直观的感知，从而使其传递给更多代的技术。这里要学到的教训是，那些对人们来说熟悉的系统，总是比那些有结构优雅但与预期相悖的系统提供更多价值。

## 在接近遗留系统时利用接口

当我在处理遗留系统时，我总是首先评估潜在用户。谁将长期维护这个系统？他们习惯使用哪些技术？谁将最常使用这个系统？他们期望系统如何工作？

这并不意味着不能改变事物或引入新概念。特别是如果系统已有几十年历史，接口可能与不再合理的过程和关联捆绑在一起，就像 80 字符的行源自打孔卡，两个字符的 Linux 命令源自电传打字机，桌面应用程序上的保存图标是软盘一样。有时候，改变接口以去除不再相关的需求是件好事。如果系统是全新的，那么定义今天一个最小可行产品（MVP）的需求是什么，是在制定攻击计划时进行思维实验的一个好方法。

然而，即使变化的结果是净正面的，改变接口也不是免费的。让人们思考会增加摩擦，增加失败的可能性，即使新的接口更好，更符合产品的整体愿景。

工程师往往高估了秩序和整洁的价值。计算机系统真正重要的，只有它在执行实际应用时的有效性。Linux 之所以能够主导操作系统世界，并不是因为它从零开始经过精心设计；它是从多个不同系统中收集了想法和实现，集中力量在一个关键地方——内核上，创造了价值。

即便是撰写学术论文的愿望已被撰写流行博客的愿望所取代，仍然存在奖励个人软件工程师独特性、创新能力，或以创新方式完成旧事物的激励机制。然而，当技术建立在共同的事物之上时，它更有可能取得成功。这两股力量在任何软件项目中总是相互冲突，但遗留系统尤其容易受到影响。

我们知道，例如，基于现有解决方案进行迭代更可能改善软件，而不是进行完全重写。完全重写的风险已经有许多文献记录。Fog Creek Software 和 Stack Overflow 的 Joel Spolsky 将其描述为“任何软件公司都可能犯下的最糟糕战略错误。”^(13) 微软初创企业部门总经理 Chad Fowler 是这样描述的：

> 几乎所有生产软件的状态都糟糕到几乎无法作为重新实现自身的指导。现在，拿这个已经糟糕的情况，只挑选出那些足够庞大、复杂且脆弱到需要大规模重写的产品，那么采用这种方法成功的概率就会显著降低。^(14)

Fred Brooks 在 1975 年创造了*第二系统综合症*这个术语，用以解释这种完全重写所产生的臃肿、低效且常常无法正常运行的软件现象。但他将这些问题归因于监督重写的架构师的经验，而不是重写本身。第二系统综合症中的“第二系统”并不是现有系统的第二个版本，而是架构师所制作的第二个系统。Brooks 的看法是，架构师在做第一个系统时因为没有做过软件，所以会更严格，但在做第二个系统时，他们过于自信，加入了各种华而不实的装饰和功能，最终使事情变得过于复杂。等到他们做第三个系统时，才会吸取教训。

不幸的是，当面临现有系统的问题时，工程团队往往会产生从零开始构建的最大动力。那些旨在逐步修复和恢复运营卓越性的举措，就像修缮一座老房子一样，通常在工程团队中很少有人愿意参与。这是因为 Zajonc 的单纯接触效应有一个上限。到了一定程度，熟悉感会导致轻蔑。

从经济学角度来看，风险和*模糊性*之间是有区别的。^(15) 风险是已知且可估算的威胁；而模糊性则是那些正负结果都未知的地方。传统的思维方式告诉我们，人类对模糊性有厌恶感，会尽可能避免它。然而，模糊性回避是那些在实验室中表现良好的决策模型，但当应用到现实世界时会出现问题，因为现实中的决策更复杂，概率定义也不那么清晰。特别是当决策涉及多个属性时，问题的积极框架可以让人们从回避模糊性转向寻求模糊性。^(16)

撇开个人赞誉的动机不谈，工程团队倾向于进行全面重写，因为他们错误地将旧系统视为规范。他们认为，既然旧系统能工作，那么所有技术挑战和潜在问题都已经解决。风险已经消除！他们可以为新系统添加更多功能，或在不担心的情况下改变底层架构。要么他们没有察觉到这些变化带来的模糊性，要么他们将这种模糊性视为积极因素，想象着性能的提升和更大创新潜力。

与此同时，现有系统的模糊性已所剩无几。它就是它，假设的潜力已被耗尽。我们知道，在超出仅仅接触的上限后，一旦人们发现了他们不喜欢的特性，他们往往会对之后发现的每个特性进行更负面的评判。^(17) 所以程序员更喜欢进行全面重写而不是迭代旧系统，因为重写保持了吸引人的模糊性，而现有系统已经非常熟悉，因此显得乏味。提出全面重写的提案通常会引入一些对工程团队来说新的语言、设计模式或技术，这并非偶然。很少有重写计划是以使用相同语言重新设计系统或仅仅解决一个明确定义的结构问题的形式出现的。全面重写的目标是恢复模糊性，从而恢复热情。而它们失败的原因在于，假设旧系统可以作为规范，并被信任为准确诊断并消除了所有风险，这个假设是错误的。

## 小心人为一致性

在下一章中，我将详细介绍如何平衡这些紧张关系，以便制定策略，决定何时重构和重写，何时利用现有的、熟悉的接口。但目前为止，从这次关于特征如何传递的探索中，我们应该得到的结论是，简洁的感知受到你在技术使用场景中所接触到的事物的影响。当事物变得熟悉时，它们看起来更容易。熟悉感是由你与技术互动的方式以及与你一起使用技术的人决定的。

但熟悉性也有其弊端。在处理遗留系统时，你会遇到许多提案，声称通过建立人为一致性来改善系统。*人为一致性*意味着将设计模式和解决方案限制在一个小范围内，可以在整个架构中标准化并反复使用，而这种做法并没有提供技术价值。理解人为一致性的重要点是，它关注的是形式和分类的一致性，而非功能的一致性。举个例子，Node.js 和 React.js 都是 JavaScript 的形式。这两种技术看起来一致，但它们做的事情不同，并且构建在不同的抽象层上。它们都是 JavaScript 的形式，并不能让 Node.js 在与 React.js 互动时比任何其他后端语言更具优势。一个工程师在其中一者上的技能，并不一定能转化到另一者上。

人为一致性可以为非技术过程带来价值。例如，标准化使用一种编程语言可以让招聘、雇佣和最终共享工程资源变得更加容易。但当现代化努力的主要目的是提供技术价值时，要小心不要被这种假设迷惑：即看起来相同，或者我们用相同的词来描述的东西，实际上并不一定能更好地集成。

另一个人为一致性发挥作用的地方是在数据库上。十年前数据库的首选不再是今天的首选，因此高层领导有时会要求将遗留数据库迁移到与新系统使用的数据库更一致的选项中。就像前面的例子一样，这样做有合理的非技术原因，比如不想承担同时支持两种基本相同数据库的费用，但当工程团队被要求移除用于缓存的键值存储，转而使用关系数据库时，问题很容易失控。

确定一致性何时能带来技术价值，何时只是人为的，是工程团队必须做出的最艰难决策之一。人类是模式匹配机器。发现熟悉的事物更容易的反面是，我们往往会过度优化，屈从于人为的一致性，尽管有更好的工具可以使用。
