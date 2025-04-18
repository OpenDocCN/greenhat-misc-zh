## 第三章：生产力**

![图片](img/com.jpg)

在 1960 年代末期，显然仅仅培养更多的程序员并不能缓解软件危机。唯一的解决方案是提高程序员的生产力——也就是使现有的程序员能够编写更多的代码——这就是软件工程领域的起源。因此，研究软件工程的一个好的起点是理解生产力。

### 2.1 什么是生产力？

尽管“生产力”一词通常被描述为软件工程的基础，但令人惊讶的是，很多人对其有着扭曲的看法。问任何程序员关于生产力的定义，你一定会听到“代码行数”、“功能点”、“复杂性指标”等等。事实是，软件项目中的生产力概念并没有什么神秘的地方。我们可以将生产力定义为：

在单位时间内或以特定成本完成的单元任务数量。

这个定义的挑战在于如何定义一个*单元任务*。一个便捷的单元任务可能是一个项目；然而，项目在规模和复杂性上差异巨大。程序员 A 在给定时间内完成了三个项目，而程序员 B 仅在一个大项目的某个小部分上工作，这并不能告诉我们这两位程序员的相对生产力。因此，单元任务通常比整个项目要小得多。通常，它是像一个函数、一行代码，或者项目中的一个更小的组件。只要单元任务在不同项目之间保持一致，并且预期一个程序员在任何项目中完成单元任务所需的时间相同，那么具体的度量标准就无关紧要。一般来说，如果我们说程序员 A 的生产力是程序员 B 的*n*倍，那么程序员 A 在相同时间内可以完成*n*倍（等效的）项目，而程序员 B 完成一个项目所需的时间。

### 2.2 程序员生产力与团队生产力

1968 年，Sackman、Erikson 和 Grant 发表了一篇震撼人心的文章，声称程序员之间的生产力差异可达 10 到 20 倍。^(1) 后来的研究和文章将这一差距推得更高。这意味着某些程序员的代码产出是一些能力较弱的程序员的 20 倍（或更多）。一些公司甚至声称，在他们的组织中，不同软件团队之间的生产力差异可以达到两个数量级。这是一个惊人的差异！如果某些程序员的生产力是其他程序员的 20 倍（即所谓的“大师级程序员”[GMPs]），那么我们是否可以采用某些技术或方法，来提高普通（或低生产力）程序员的生产力呢？

因为无法训练每个程序员将其提升到 GMP（高效能程序员）水平，大多数软件工程方法论采用其他技术，如更好的管理流程，来提高大团队的生产力。本书系列采取另一种方法：不是尝试提高团队的生产力，而是教导个人程序员如何提高自己的生产力，并朝着成为 GMP 努力。

尽管单个程序员的生产力对项目交付进度的影响最大，但现实世界更关注项目成本——完成项目所需的时间和费用——而非程序员的生产力。除非是小型项目，*团队*的生产力优先于*团队成员*的生产力。

团队的生产力不仅仅是每个成员生产力的平均值；它基于团队成员之间的复杂互动。会议、沟通、个人互动和其他活动都会对团队成员的生产力产生负面影响，培训新成员或经验较少的成员、以及重构现有代码也会产生同样的影响。（这些活动带来的开销是程序员在小型项目中比在中型或大型项目中更具生产力的主要原因。）团队可以通过管理沟通和培训的开销、抵制重构现有代码的冲动（除非确实必要），以及管理项目使代码在第一次编写时就正确（减少重构的需要）来提高生产力。

### 2.3 人工工时与实际时间

前面给出的定义提供了两种生产力的衡量标准：一种基于时间（生产力是单位时间内完成的任务数量），另一种基于成本（生产力是给定成本下完成的任务数量）。有时成本比时间更重要，反之亦然。为了衡量成本和时间，我们可以分别使用人工工时和实际时间。

从公司的角度来看，项目成本中与程序员生产力相关的部分与其*人工工时*直接成正比，即每个团队成员在项目上花费的时间。一个*工人日*大约是 8 个人工工时，一个*工人月*大约是 176 个人工工时，一个*工人年*大约是 2,000 个人工工时。项目的总成本是项目上花费的人工工时总数乘以每个团队成员的平均时薪。

*实际时间*（也称为*日历时间*或*墙钟时间*）就是项目进行过程中时间的推移。项目计划和最终产品的交付通常基于实际时间。

工时是实际时间与同时在项目上工作的团队成员数量的乘积，但优化其中一个数量并不总是能优化另一个。例如，假设你正在开发一个市政选举需要的应用程序。在这种情况下，最关键的数量是实际时间；软件必须在选举日期之前完全功能化并部署，无论成本如何。相比之下，一个“地下程序员”正在开发世界上下一个杀手级应用，他可以花更多时间在项目上，从而延长交付日期，但无法雇佣额外人员以更快完成应用。

项目经理在大型项目中常犯的一个最大错误是将工时与实际时间混淆。如果两个程序员可以在 2,000 工时（和 1,000 实际小时）内完成一个项目，你可能会得出结论，四个程序员可以在 500 实际小时内完成该项目。换句话说，通过将项目团队扩充一倍，你可以在一半的时间内完成项目，并按计划完成。然而，现实中，这并不总是奏效（就像增加第二个烤箱也不会让蛋糕更快烤好一样）。

增加人员以提高每个日历小时的工时数，通常在大型项目中比在小型和中型项目中更成功。小型项目的范围足够有限，单个程序员可以跟踪项目相关的所有细节；程序员无需咨询、协调或培训其他人来参与项目。通常情况下，向小型项目添加程序员会消除这些优势，并在不显著影响交付计划的情况下，显著增加成本。在中型项目中，平衡较为微妙：两个程序员的生产力可能比三个程序员更高，^(2) 但增加更多的编程资源可以帮助加快一个人手不足的项目的完成（尽管可能会以更高的成本）。在大型软件项目中，增加团队规模会相应缩短项目的计划时间，但一旦团队超过一定规模，可能需要添加两三个人来完成通常由一个人完成的工作。

### 2.4 概念和范围复杂性

随着项目变得更加复杂，^(3) 程序员的生产力会下降，因为更复杂的项目需要更深刻（且更长时间）的思考才能理解发生了什么。此外，随着项目复杂性的增加，软件工程师引入错误的可能性也更大，系统中早期引入的缺陷可能要到后来才会被发现，这时修复它们的成本会更高。

复杂性有几种形式。考虑以下两个“复杂”的定义：

1.  拥有复杂、繁琐或错综复杂的部分排列，使得理解变得困难

1.  由许多互相关联的部分组成

我们可以称第一个定义为*概念复杂性*。例如，考虑一个高层语言（HLL）中的单个算术表达式，如 C/C++，它可能包含复杂的函数调用、几个具有不同优先级的奇怪算术/逻辑运算符，以及许多使表达式难以理解的括号。概念复杂性可能出现在任何软件项目中。

我们可以称第二个定义为*范围复杂性*，当信息量过大，人类的思维无法轻松消化时就会发生。即使项目的各个组件很简单，项目的庞大规模也使得一个人无法理解整个项目。范围复杂性出现在中型和大型项目中（事实上，正是这种复杂性将小项目与其他项目区分开来）。

概念复杂性通过两种方式影响程序员的生产力。首先，复杂的结构需要更多的思考（因此也需要更多的时间）来实现，而比简单的结构复杂得多。其次，复杂的结构更容易包含缺陷，必须在后期进行修复，从而导致生产力的相应损失。

范围复杂性引入了不同的问题。当项目达到一定规模时，项目中的程序员可能完全不了解项目其他部分的进展，甚至可能重复编写系统中已有的代码。显然，这会降低程序员的生产力，因为程序员浪费了时间在编写那部分代码上。^(4) 由于范围复杂性，也可能会导致系统资源使用效率低下。在工作系统的某一部分时，一个小团队的工程师可能只测试自己的部分，但他们看不到它与系统其他部分的交互（可能这些部分甚至还没有准备好）。因此，系统资源使用的问题（如 CPU 周期或内存）可能直到后期才被发现。

通过良好的软件工程实践，部分复杂性是可以缓解的。但总体结果是一样的：随着系统的复杂度增加，人们必须花更多的时间去思考它们，并且缺陷的机会大幅增加。最终结果是生产力下降。

### 2.5 预测生产力

生产力是一个可以衡量并尝试预测的项目属性。当项目完成时，假设团队在项目开发过程中保持了准确的任务记录，判断团队（及其成员）的生产力是相对简单的。尽管过去项目的成功或失败不能保证未来项目的成败，但过去的表现是预测软件团队未来表现的最佳指标。如果你想改进软件开发过程，你需要跟踪哪些技术方法有效，哪些无效，这样你就能知道未来项目中该做什么（或*不做什么*）。为了追踪这些信息，程序员及其支持人员必须记录所有软件开发活动。这是软件工程引入的*纯粹负担*的一个很好的例子：文档几乎对当前项目的完成或提高质量没有帮助，但它是对未来项目的投资，帮助预测（和提高）生产力。

Watts S. Humphrey 的*《软件工程的学科》（A Discipline for Software Engineering）*（Addison-Wesley Professional, 1994）是一本很棒的书，适合那些有兴趣了解如何追踪程序员生产力的人。Humphrey 教授了一种形式、指导方针和程序的系统，来开发他称之为*个人软件过程（PSP）*的方法。尽管 PSP 主要面向个人，但它提供了宝贵的洞察，帮助发现程序员在软件开发过程中的问题所在。反过来，这能极大帮助他们确定如何攻克下一个重大项目。

### 2.6 指标及其必要性

通过观察团队或个人在类似项目中的过去表现来预测其生产力的问题在于，这种方法*仅适用于类似的项目*。如果新项目与团队过去的项目有显著不同，过去的表现可能不是一个好的指标。由于项目在规模上有很大差异，跨整个项目衡量生产力可能无法提供足够的信息来预测未来的表现。因此，需要某种低于整个项目粒度级别的衡量系统（*指标*），以更好地评估团队和团队成员。理想的指标应该独立于项目（团队成员、所选编程语言、所用工具及其他相关活动和组件）；它必须能够跨多个项目使用，以便进行比较。虽然确实存在一些指标，但没有一个是完美的——甚至不是非常好的。尽管如此，一个不完美的指标总比没有指标好，因此软件工程师们会继续使用它们，直到出现更好的测量方法。在本节中，我将讨论几种较为常见的指标，以及每种指标的优缺点。

#### *2.6.1 可执行文件大小指标*

程序员用来指定软件系统复杂度的一个简单度量是最终系统中可执行文件的大小。^(5) 假设是复杂的项目产生大的可执行文件。

该度量的优点包括：

+   它的计算非常简单（通常只需要查看目录列表并计算一个或多个可执行文件的总和）。

+   它不需要访问原始源代码。

不幸的是，执行文件大小度量也存在一些缺陷，使其不适合大多数项目：

+   可执行文件通常包含未初始化的数据，这些数据对文件大小的贡献与系统复杂度几乎没有关系。

+   库函数增加了可执行文件的大小，但实际上它们减少了项目的复杂性。^(6)

+   执行文件大小度量不是与语言无关的。例如，汇编语言程序通常比高级语言（HLL）可执行文件更为紧凑，但大多数人认为汇编程序比等效的 HLL 程序更复杂。

+   执行文件大小度量不是与 CPU 无关的。例如，针对 80x86 CPU 的可执行文件通常比为 ARM（或其他 RISC）CPU 编译的同一程序要小。

#### *2.6.2 机器指令度量*

执行文件大小度量的一个主要缺陷是，某些可执行文件格式包括用于未初始化静态变量的空间，这意味着对输入源文件的微小更改可能会显著改变可执行文件的大小。解决这个问题的一种方法是仅计算源文件中的机器指令（要么是机器指令的大小，以字节为单位，要么是机器指令的总数）。尽管这种度量解决了未初始化静态数组的问题，但它仍然表现出执行文件大小度量的所有其他问题：它依赖于 CPU，它计算了程序员未编写的代码（如库代码），并且它与语言有关。

#### *2.6.3 代码行数度量*

代码行数（LOC，或者用于表示千行代码的 KLOC）度量是目前使用最广泛的软件度量方法。顾名思义，它是对项目中源代码行数的统计。该度量有一些优点，也有一些缺点。

单纯计算源代码行数似乎是使用 LOC 度量的最流行形式。编写一个行数统计程序相当简单，绝大多数操作系统（如 Linux）上可用的字数统计程序都可以为你计算行数。

以下是一些关于 LOC 度量的常见说法：

+   无论使用什么编程语言，编写一行源代码所需的时间大致相同。

+   LOC 度量不受项目中使用库例程（或其他代码重用）的影响（当然，前提是不计算预编写的库源代码中的行数）。

+   LOC 度量与 CPU 无关。

LOC 度量方法确实有一些缺点：

+   它无法很好地指示程序员完成了多少工作。100 行 VHLL 代码完成的工作比 100 行汇编代码要多。

+   它假设每行源代码的成本相同。然而，事实并非如此。空白行成本微乎其微，简单的数据声明具有较低的概念复杂度，而包含复杂布尔表达式的语句则具有非常高的概念复杂度。

#### *2.6.4 语句数度量*

语句数度量计算源文件中的语言语句数量。它不计算空白行或注释，也不将分布在多行上的单个语句视为独立的实体。因此，它在计算程序员的工作量方面，比 LOC 更有效。

尽管语句数度量比代码行数提供了更好的程序复杂度视图，但它也存在许多相同的问题。它度量的是工作量而非完成的工作，它不像我们希望的那样独立于语言，并且它假设程序中的每条语句需要相同的工作量来编写。

#### *2.6.5 功能点分析*

功能点分析（FPA）最初是为了预测一个项目在编写源代码之前需要多少工作量而设计的。基本想法是考虑程序所需的输入数量、产生的输出数量以及必须执行的基本计算，并利用这些信息来确定项目的进度。^(7)

FPA（功能点分析）相比于行数或语句数等简化的度量方法，具有几个优势。它真正独立于语言和系统。它依赖于软件的功能性，而不是实现方式。

然而，FPA 确实存在一些严重的缺点。首先，与行数或语句数不同，计算程序中的“功能点”数量并非简单直接。分析是主观的：分析人员必须决定每个功能的相对复杂性。此外，FPA 从未成功实现自动化。这样的程序如何决定一个计算何时结束，另一个计算何时开始？它如何将不同的复杂度值（同样是主观分配）应用于每个功能点？由于这种手动分析相当耗时且成本高昂，FPA 并不像其他度量方法那样流行。在很大程度上，FPA 是一个*事后分析*（项目结束时的工具），通常在项目完成后而非开发过程中使用。

#### *2.6.6 McCabe 的环形复杂度度量*

如前所述，LOC 和语句计数度量的一个根本问题是它们假设每个语句具有相同的复杂性。FPA 稍微好一些，但需要分析师为每个语句分配复杂性评分。不幸的是，这些度量无法准确反映为完成工作所付出的努力，因此无法记录程序员的生产力。

Thomas McCabe 开发了一种被称为*循环复杂度*的软件度量方法，通过计算程序中的路径数量来衡量源代码的复杂性。它从程序的流程图开始。流程图中的节点对应程序中的语句，节点之间的边对应程序中的非顺序控制流。通过计算节点数量、边数量和流程图中连接组件的数量，可以为代码提供一个单一的循环复杂度评分。考虑一个包含 1,000 行`printf`语句的程序（没有其他内容）；其循环复杂度为 1，因为程序中只有一条路径。现在考虑第二个例子，其中包含大量的控制结构和其他语句；它的循环复杂度评分将会更高。

循环复杂度度量是有用的，因为它是一个客观的衡量标准，而且可以编写程序来计算这个值。它的缺点是程序的体积大小无关紧要；也就是说，它把一个简单的`printf`语句和连续 1,000 个`printf`语句视为相同，尽管第二种情况显然需要更多的工作（即使这额外的工作只是大量的剪切和粘贴操作）。

#### *2.6.7 其他度量*

我们可以设计很多度量标准来衡量程序员生产力的某个方面。一个常见的度量是统计程序中的操作符数量。这个度量认识到并调整了某些语句（包括那些不涉及控制路径的语句）比其他语句更复杂，需要更多的时间来编写、测试和调试。另一个度量是统计程序中的标记数量（如标识符、保留字、操作符、常量和标点符号）。不过，无论是哪种度量，它们都会有缺陷。

许多人尝试使用多种度量标准的组合（例如，将行数与环形复杂度和操作符数相乘）来创建一个“多维度”的度量标准，以更好地衡量编写一段代码所涉及的工作量。不幸的是，随着度量标准复杂性的增加，它在给定项目上的使用变得更加困难。LOC（行数）之所以成功，是因为你可以使用 Unix 的`wc`（字数统计）工具，它也会统计行数，从而快速了解程序的大小。计算这些其他度量标准的值通常需要专门的、依赖语言的应用程序（假设该度量标准是可以自动化的）。因此，尽管人们提出了大量的度量标准，但很少有像 LOC 那样变得如此广泛应用。

#### *2.6.8 度量标准的问题*

大致衡量项目源代码量的度量标准，若假设每一行或每条语句的编写大致需要相同的时间，它们能很好地反映项目的工作量。然而，代码行数（或语句数）与实际完成的工作之间的关系是微弱的。不幸的是，度量标准衡量的是程序的一些物理属性，但很少衡量我们真正关心的内容：编写代码所需的智力劳动。

几乎所有度量标准的另一个失败之处在于，它们都假设更多的工作会产生更多（或更复杂）的代码。但这并不总是正确的。例如，一个优秀的程序员通常会花费时间重构代码，使其更简洁、更不复杂。在这种情况下，更多的工作反而会产生更少的代码（而且代码更简单）。

度量标准也未能考虑与代码相关的环境问题。例如，10 行代码写在裸机嵌入式设备上，是否等同于在 SQL 数据库应用程序中写的 10 行代码？

所有这些度量标准都未考虑某些项目的学习曲线。10 行 Windows 设备驱动程序代码是否等同于 10 行 Java 代码写在 Web 小程序中？这两个项目的 LOC 值是无法比较的。

最终，大多数度量标准都失败了，因为它们衡量的是*错误的内容*。它们衡量的是程序员所写的*代码量*，而不是程序员对完整项目的整体*贡献*（生产力）。例如，一个程序员可能用一条语句完成一个任务（比如标准库调用），而另一个程序员可能需要写几百行代码来完成同样的任务。大多数度量标准会认为第二个程序员的生产力更高。

正是由于这些原因，当前使用的最复杂的软件度量标准也存在根本性的缺陷，这些缺陷使得它们无法完全有效。因此，选择一个“更好的”度量标准往往得不到比使用“有缺陷”的度量标准更好的结果。这也是 LOC 度量标准继续流行的另一个原因（以及本书使用它的原因）。它是一个极其糟糕的度量标准，但它并不比许多其他现有的度量标准差多少，而且它非常容易计算，无需编写特别的软件。

### 2.7 我们如何突破每天 10 行代码？

早期的软件工程文献声称，一个参与重大产品的程序员每天平均写 10 行代码。在 1977 年的一篇文章中，Walston 和 Felix 报告了每位开发者每月约 274 行代码^(8)。这两个数字描述的是在该产品生命周期内（即从第一次发布到退役期间，所有程序员花费的时间总量）所产生的经过调试和文档化的代码，而不仅仅是每天编写代码所花费的时间。尽管如此，这些数字看起来还是偏低。为什么？

在项目开始时，程序员可能每天能迅速写出 1,000 行代码，然后为了研究项目某个部分的解决方案，测试代码，修复错误，重写一半代码，再进行文档编写，速度就会减慢。到产品的第一次发布时，生产力已经从最初的 1,000 行代码每天下降了十倍，变成了不到 100 行。产品第一次发布后，通常会开始进行第二次发布，然后是第三次，依此类推。在产品的生命周期中，可能会有几个不同的开发人员参与其中。到项目结束时，代码已经被重写了几次（这是生产力的巨大损失），并且几个程序员花费了宝贵的时间去学习代码的运行方式（这也在削弱他们的生产力）。因此，在产品的生命周期内，程序员的生产力降到了每天 10 行代码。

软件工程生产力研究的一个重要结果是，提高生产力的最佳方式并不是发明某种方案，让程序员在单位时间内写出两倍的代码行数，而是*减少浪费在调试、测试、文档编写、重写代码以及在第一版代码存在后对新程序员进行培训的时间*。为了减少这些损失，改进程序员在项目中使用的流程比训练他们在单位时间内写两倍代码要容易得多。软件工程一直认识到这个问题，并试图通过减少所有程序员花费的时间来解决它。个人软件工程的目标是减少个别程序员在项目中其部分工作的时间。

### 2.8 估算开发时间

如前所述，尽管生产力对管理层评定奖金、加薪或口头表扬等方面有意义，但跟踪生产力的真正目的是预测未来项目的开发时间。过去的结果并不能保证未来的表现，因此你还需要知道如何估算项目的时间表（或者至少是你在项目中的部分时间表）。作为一名独立的软件工程师，你通常没有足够的背景、教育和经验来确定时间表的内容，因此你应该与项目经理会面，让他们解释在时间表中需要考虑的因素（这不仅仅是编写代码所需的时间），然后以此为基础构建估算。尽管本书的范围超出了正确估算项目所需的所有细节（有关更多信息，请参见第 37 页中的“更多信息”部分），但简要描述一下开发时间估算如何因项目规模不同（无论是小型、中型、大型项目，还是仅仅是项目的一部分）而有所不同，仍然是有价值的。

#### *2.8.1 估算小型项目开发时间*

按照定义，小型项目是由一名工程师完成的。项目进度的主要影响因素将是该软件工程师的能力和生产力。

估算小型项目的开发时间比大型项目要容易得多且更为准确。小型项目不会涉及并行开发，时间表只需要考虑单个开发者的生产力。

毫无疑问，估算小型项目开发时间的第一步是识别并理解所有需要完成的工作。如果项目的某些部分在此时尚未定义，当这些未定义的部分不可避免地需要比你预想的更多时间时，时间表将会引入相当大的误差。

在估算项目完成时间时，设计文档是项目中最重要的部分。没有详细的设计，就无法知道项目由哪些子任务组成，也无法估算每个子任务需要多长时间。一旦你将项目分解为适当大小的子任务（适当的大小是指能清楚估计完成所需时间的子任务），你只需将所有子任务的时间加总，就能得到一个合理的初步估算。

然而，人们在估算小型项目时犯的最大错误之一是，他们将子任务的时间加在一起，并称其为自己的进度计划，却忘记考虑会议、电话、电子邮件和其他行政任务的时间。他们还忘记添加测试时间，以及在发现缺陷时纠正（并重新测试）软件的时间。由于很难估算软件中会有多少缺陷，以及解决这些缺陷需要多少时间，大多数经理会将进度计划的初步估算乘以 2 到 4 倍。假设程序员（团队）在项目中保持合理的生产力，这个公式可以为小型项目提供一个良好的估算。

#### *2.8.2 估算中型和大型项目的开发时间*

从概念上讲，中型和大型项目由许多小项目组成（分配给各个团队成员），这些小项目结合起来形成最终结果。因此，大型项目进度计划的初步估算是将其拆分为一堆较小的项目，为每个子项目开发估算，然后将这些估算加在一起。这实际上是小型项目估算的一个更大版本。不幸的是，在现实生活中，这种估算形式充满了错误。

第一个问题是，中型和大型项目引入了小型项目中不存在的问题。一个小型项目通常只有一名工程师，正如之前所提到的，进度完全依赖于该人的生产力和可用性。在较大的项目中，多个人员（包括许多非工程师）会影响估算的进度计划。一位掌握关键知识的软件工程师可能因度假或生病而缺席几天，导致另一名需要这些信息来推进工作的工程师被耽搁。较大项目中的工程师通常每周都有几次会议（在大多数进度计划中没有考虑到），这些会议使得他们不能进行编程工作—也就是说，他们需要脱离工作几个小时。大型项目的团队组成可能会发生变化；一些有经验的程序员离开，其他人必须接手并学习子任务，而新程序员加入项目时需要时间适应。有时，甚至为新员工提供一台计算机工作站也需要几周时间（例如，在一个有官僚主义的 IT 部门的大公司）。等待购买软件工具、开发硬件和获得组织其他部门的支持也会导致进度问题。这个问题清单不断延伸。很少有进度估算能够准确预测这些多种多样的方式会如何消耗时间。

最终，创建中型和大型项目的进度估算涉及四个任务：将项目拆分为较小的项目，对这些小项目进行估算，加入集成测试和调试的时间（即将小任务合并并使它们能正常协同工作），然后对这个总和应用一个乘数因子。它们并不精确，但目前的情况大致就是这样。

#### *2.8.3 估算开发时间的问题*

因为项目进度估算涉及预测开发团队未来的表现，几乎没有人相信预计的进度会完全准确。然而，典型的软件开发进度预测尤其不准确。以下是一些原因：

**它们是研发项目。** 研发项目涉及做一些你以前从未做过的事情。它们需要一个研究阶段，在此阶段，开发团队分析问题并尝试确定解决方案。通常，没有办法预测研究阶段将花费多少时间。

**管理层有预设的进度安排。** 通常，市场部门决定希望在某个日期推出一个可以销售的产品，管理层则通过倒推该日期来创建项目进度。在要求编程团队提供子任务的时间估算之前，管理层已经对每个任务的完成时间有了一些预设的看法。

**团队以前做过这件事。** 管理层通常假设，如果你以前做过某事，那么第二次会更容易（因此会节省时间）。在某些情况下，这个假设是有一定道理的：如果一个团队从事的是研发项目，第二次做会更容易，因为他们只需要进行开发，且可以跳过（至少大部分）研究。然而，假设一个项目第二次总是更容易的观点很少是正确的。

**时间或资金不足。** 在很多情况下，管理层会设定某种金钱或时间限制，要求项目必须在这个限制内完成，否则就会被取消。这对那些薪水依赖于项目推进的人来说是*错误*的说法。如果面临选择是说“是的，我们可以按时完成进度”，还是找新工作，大多数人——即使知道成功的几率不高——都会选择前者。

**程序员往往夸大自己的效率。** 有时当软件工程师被问及是否能在某个时间框架内完成一个项目时，他们并不是在谎报所需的时间，而是对自己的表现做出乐观估计——而这种估计在实际工作中很少成立。当被问及在*真正高压*的情况下能产出多少时，大多数软件工程师给出的数字代表了他们在短时间内最大产出的记录（例如，在“危机模式”下，每周工作 60 到 70 小时），而没有考虑到意外的障碍（比如突然出现的非常棘手的 bug）。

**进度依赖于额外工作时间。** 管理层（和工程师）常常认为程序员在进度开始延迟时，总能投入“额外的一些小时”。因此，进度计划往往比实际情况更为激进（忽视了让工程师加班的负面影响）。

**工程师就像积木一样。** 项目进度的一个常见问题是，管理层假设可以通过增加程序员来提前项目的发布日期。然而，正如之前提到的，这并不一定正确。你不能随意增减项目中的工程师，并期望项目进度会相应成比例地变化。

**子项目估算不准确。** 现实的项目进度是通过自上而下的方式制定的。整个项目被拆分为更小的子项目。然后，这些子项目再拆分为子子项目，依此类推，直到子项目的规模足够小，以便某人能够准确预测每个小部分所需的时间。然而，这种方法有三个挑战：

+   愿意为这种方式制定计划付出努力（即提供一个正确且准确的自上而下的项目分析）

+   获取准确的子项目估算（特别是来自那些可能没有适当管理培训的工程师，他们不理解在时间估算中需要考虑哪些内容）

+   接受进度预测的结果

### 2.9 危机模式项目管理

尽管所有相关人员都抱有最好的意图，但许多项目仍会大幅落后于计划，管理层不得不加速开发以达到某个重要的里程碑。为了赶上截止日期，工程师通常被要求每周投入更多的时间，以减少（实际时间）交付日期。当这种情况发生时，项目就进入了“危机模式”。

危机模式的工程工作可以有效应对（快速）临近的截止日期，但总体来说，危机模式从来都不是特别高效，反而会导致生产力下降，因为大多数人工作之外还有其他事务需要处理，并且需要时间休息、放松大脑，让自己整理一下长时间工作中积累下来的问题。在疲劳状态下工作容易犯错误，而这些错误往往需要花费更多的时间来修正。从长远来看，放弃危机模式并坚持 40 小时工作周会更高效。

处理危机模式安排的最佳方法是在整个项目中添加里程碑，生成一系列“小危机”，而不是在项目结束时发生一次大危机。每个月增加一天或几天的加班，远比在项目结束时拼命工作几个七天的周要好得多。为了赶上最后期限，工作一两天 16 小时并不会对你的生活质量造成负面影响，也不会让你感到疲惫不堪。

除了健康和生产力问题，处于危机模式下还可能引发调度、伦理和法律问题：

+   一个糟糕的工作安排也会影响到未来的项目。如果你每周工作 60 小时，管理层会认为未来的项目也可以在相同的（实际）时间内完成，并期望你未来以此节奏工作，而不支付额外的报酬。

+   长期处于危机模式下运营的项目，其技术人员流动率较高，进一步降低了团队的生产力。

+   还有一个法律问题，就是加班时间没有得到加班费的补偿。视频游戏行业中几起高调的诉讼案件表明，工程师有权获得加班费（他们并非*免薪的员工*）。即使你的公司能够挺过这些诉讼，时间报告、行政管理和工作时间的规定将变得更加严格，导致生产力下降。

再次强调，处于危机模式下如果管理得当，可以帮助你在某些时限内完成任务。但最好的解决方案是制定更合理的计划，避免完全进入危机模式。

### 2.10 如何提高生产力

本章花了相当多的时间定义生产力及衡量生产力的指标。但它并没有花费太多时间描述程序员如何提高自己的生产力，成为一名优秀的程序员。关于这个话题，整本书都可以写（并且确实有人写过）。本节提供了可以在个人和团队项目中提高生产力的技术概述。

#### *2.10.1 明智选择软件开发工具*

作为一名软件开发人员，你的大部分时间将花在使用软件开发工具上，工具的质量对你的生产力有着巨大的影响。遗憾的是，选择开发工具的主要标准似乎是对工具的熟悉度，而不是工具对当前项目的适用性。

在选择项目初期的工具时，请记住你可能需要在整个项目生命周期内（甚至可能是更长时间）使用它们。例如，一旦你开始使用缺陷跟踪系统，由于数据库文件格式不兼容，可能很难切换到另一个系统；源代码控制系统也是如此。幸运的是，如今软件开发工具（尤其是 IDE）相对成熟，而且很多工具之间能够互操作，所以很难做出错误的选择。尽管如此，在项目开始时仔细思考，可以避免将来出现许多问题。

对于软件开发项目来说，最重要的工具选择是选择哪种编程语言以及使用哪些编译器/解释器/翻译器。选择最佳语言是一个难题。选择一种编程语言往往很容易，因为你对它比较熟悉，不会因为学习它而失去生产力；然而，未来的新工程师可能会因为一边学习编程语言一边维护代码而大大降低生产力。此外，有些语言选择可以简化开发过程，显著提高生产力，足以弥补学习语言的时间。如前所述，选择错误的编程语言可能会导致浪费大量开发时间，直到你发现它不适合项目，不得不重新开始。

编译器性能（处理一个常见源文件所需的时间）对生产力有巨大影响。如果编译器编译一个普通源文件需要两秒钟，而不是两分钟，你可能会发现使用更快的编译器更能提高生产力（尽管更快的编译器可能缺少一些功能，这会在其他方面影响你的生产力）。工具处理代码的时间越少，你就能有更多的时间进行设计、测试、调试和优化代码。

同时，使用一组能很好协作的工具也非常重要。如今，我们理所当然地使用*集成开发环境（IDE）*，它将编辑器、编译器、调试器、源代码浏览器以及其他工具整合成一个程序。在同一窗口中，能够快速在编辑器中进行小的修改、重新编译源代码模块并在调试器中运行结果，这对提升生产力有着显著的帮助。

然而，你常常需要在 IDE 外部处理项目的某些部分。例如，一些 IDE 不直接支持源代码控制或缺陷跟踪（尽管许多 IDE 支持）。大多数 IDE 没有提供用于编写文档的文字处理器，也没有提供用于维护需求列表、设计文档或用户文档的简单数据库或电子表格功能。你很可能需要使用一些 IDE 外部的程序——如文字处理、电子表格、绘图/图形、网页设计和数据库程序等等——来完成项目所需的所有工作。

在 IDE 外部运行程序并不是问题。只需确保你选择的应用程序与你的开发过程以及 IDE 生成的文件（反之亦然）兼容。如果你在 IDE 和外部应用程序之间传输文件时必须不断运行转换程序，你的生产力将会下降。

我能为你推荐使用的工具吗？绝对不行。项目需求各不相同，这里不可能考虑所有的建议。我的建议是，从项目开始时就要意识到这些问题。

但我*能*给出的一个建议是，在选择开发工具时，避免采用“哇，为什么不试试这项新技术”这种方式。花费六个月时间使用一个开发工具后发现它根本无法完成任务（并且以它为基础编写了源代码）可能会造成灾难性的后果。在不涉及产品开发的情况下评估你的工具，只有在你确信它们能为你所用时才开始使用新工具。一个经典的例子就是苹果的 Swift 编程语言。直到 Swift v5.0 发布（大约是 Swift 首次推出四年后），使用 Swift 一直是一种令人沮丧的经历。每年苹果都会发布一个新版本，与早期版本的源代码不兼容，这迫使你回过头来修改旧程序。此外，早期版本的语言中缺少了许多功能，有些功能也还没准备好进入“黄金时间”。直到 5.0 版本（本书写作时发布），该语言才显得相对稳定。然而，那些早早加入 Swift 阵营的人，为语言的不成熟发展付出了代价。^(9)

可悲的是，许多项目中你并不能选择开发工具。这个决定通常是高层指令，或者你继承了早期产品的工具。抱怨无济于事，只会浪费时间和精力，降低你的生产力。相反，要善于利用现有工具集，并成为它的使用专家。

#### *2.10.2 管理开销*

在任何项目中，我们可以将工作分为两类：与项目直接相关的工作（例如编写代码或项目文档）和与项目间接相关的工作。间接活动包括会议、阅读和回复电子邮件、填写时间卡和更新进度。这些是*开销*活动：它们增加了项目的时间和成本，但并没有直接帮助完成工作。

通过遵循 Watts S. Humphrey 的*个人软件工程*指南，你可以追踪项目中的时间花费，并轻松看到自己在项目上的时间花费与在开销活动上的时间花费。如果你的开销时间超过了总时间的 10%，就应该重新考虑你的日常活动。尝试减少或合并这些活动，减少它们对生产力的影响。如果你不追踪项目外的时间，你就错过了通过管理开销来提高生产力的机会。

#### *2.10.3 设定明确的目标和里程碑*

人类有一种自然的倾向，在没有迫近的截止日期时会放松自己，然后在截止日期临近时进入“超高速模式”。如果没有目标，很少有有效的工作能够完成。如果没有截止日期，很少有人会有动力在及时的方式下达成目标。因此，为了提高生产力，确保自己设定清晰的目标和子目标，并为它们设定严格的*里程碑*。

从项目管理的角度来看，里程碑是项目中的一个标记，用来确定工作进展的程度。一个优秀的经理总是会在项目进度中设定目标和里程碑。然而，少有进度表能够为单个程序员提供有用的目标。这就是个人软件工程发挥作用的地方。要成为一个高效的程序员，就需要在你负责的（项目部分）中精细管理自己的目标和里程碑。简单的目标，比如“在午饭前完成这个函数”或者“在今天下班前找到这个错误的源头”能帮助你保持专注。更大的目标，比如“在下周二前完成这个模块的测试”或者“今天至少执行 20 个测试程序”能帮助你衡量生产力，并确定自己是否达成了预期的目标。

#### *2.10.4 自我激励的实践*

提高生产力全靠态度。尽管他人可以帮助你更好地管理时间并在你遇到困难时提供帮助，但关键在于你必须主动去提升自己。始终关注自己的节奏，并不断努力提高自己的表现。通过追踪目标、努力和进展，你将能够在需要时“激励自己”，更加努力地提高生产力。

缺乏动力可能是生产力的最大障碍之一。如果你的态度是“唉，我今天必须做*那个*”，那么你完成任务的时间可能会比你抱着“哦！这是最有趣的部分！这一定很有意思！”的态度要长。

当然，并不是每个任务都能让你感到有趣和好玩。这正是*个人*软件工程发挥作用的地方。如果你想保持高于平均水平的生产力，当一个项目让你感到“缺乏动力”时，你需要有相当强的自我激励。试着创造一些理由让工作变得更有吸引力。例如，给自己设定小挑战，并在达成目标后奖励自己。一位高效的软件工程师不断地进行自我激励：你对一个项目的动力保持得越久，你的生产力就越高。

#### *2.10.5 集中注意力并消除干扰*

保持专注并消除干扰是提升生产力的另一种方法。进入“心流状态”。以这种方式工作的软件工程师比那些在脑海中同时处理多任务的人更具生产力。为了提高生产力，尽可能长时间地集中精力处理一项任务。

集中注意力最容易在一个安静的环境中，且没有任何视觉刺激（除了你的显示屏）。有时候，工作环境并不利于极度专注。在这种情况下，戴上耳机并播放背景音乐可能有助于消除干扰。如果音乐太分散注意力，可以尝试听白噪音；网上有好几个白噪音应用可供下载使用。

每当你在任务进行中被打断时，重新进入专注状态需要时间。事实上，可能需要长达半小时才能完全重新聚焦于工作。当你需要集中精力完成一项任务时，可以挂上告示，表示只有紧急事项才可打扰你，或者在你的工作区附近标明“办公时间”——你可以被打扰的时间；例如，你可以允许每小时开始时打扰五分钟。为了节省同事 10 分钟的时间，回答一个他们自己能解决的问题，可能会让你损失半小时的生产力。你确实需要与团队合作并做一个好的队友；然而，确保过度的团队互动不会影响你（以及他人）的生产力同样重要。

在一个典型的工作日中，会有许多预定的干扰：餐休、休息时间、会议、行政事务（例如处理电子邮件和时间记录）等。如果可能的话，尽量将其他干扰安排在这些事件周围。例如，关闭所有电子邮件提醒；在几秒钟内回复邮件是*很少*是紧急的，如果有紧急情况，别人可以亲自来找你或者给你打电话。如果人们确实需要你快速回复，设定闹钟提醒你在固定时间检查电子邮件（短信和其他干扰也一样）。如果你能做到，可以考虑将手机静音，如果你接到很多非紧急的电话，可以在休息时每小时检查一次消息。适合你的方法取决于你个人和职业生活的情况。但你所经历的干扰越少，你的工作效率就会越高。

#### *2.10.6 如果感到无聊，做其他事情*

有时候，不管你多么自我激励，你都会感到对手头的工作厌倦，难以集中注意力；这时，你的生产力会大幅下降。如果你无法进入工作状态并专注于任务，休息一下，换做其他工作。不要用无聊作为借口，在任务间徘徊而没有取得实质性进展。但当你真的卡住了，无法继续前进时，换一个你能有效完成的任务。

#### *2.10.7 尽量保持自给自足*

尽可能自己处理分配给你的所有任务。这不会提升你的工作效率；然而，如果你不断寻求其他工程师的帮助，可能会影响他们的生产力（记住，他们也需要保持专注，避免干扰）。

如果你正在处理一个需要比你当前知识更多的任务，并且不想不断打扰其他工程师，你有几个选择：

+   花时间自学，尽量让自己能够完成任务。虽然这可能会影响你短期的生产力，但你获得的知识会帮助你完成未来的类似任务。

+   和你的经理见面，解释你遇到的问题。讨论是否可以将任务重新分配给更有经验的人，并给你分配一个你能更好处理的任务。

+   和你的经理安排一次会议，在不影响其他工程师工作效率的时间（例如工作日的开始）寻求他们的帮助。

#### *2.10.8 识别何时需要帮助*

你可能会把自我支持的态度推得有些过头。你可能会花费过多的时间解决一个队友只需要几分钟就能解决的问题。作为一个优秀的程序员的一个方面是认识到自己卡住了，需要帮助才能前进。当你遇到困难时，最好的方法是设置一个定时提醒。在被卡住一段时间（无论是几分钟、几小时，甚至几天）后，寻求帮助。如果你知道该向谁寻求帮助，就直接去找他们。如果不确定，找经理帮忙。大多数情况下，经理可以把你引导到正确的人那里，这样你就不会打扰那些无法帮助你的人。

团队会议（每日或每周）是向团队成员寻求帮助的好地方。如果你有几个任务，而其中一个任务让你陷入困境，先放一放，做其他任务（如果可能的话），并将你的问题留到团队会议上。如果在会议之前你已经没有任务了，可以请求经理让你忙碌，以免打扰到别人。此外，在做其他任务的过程中，解决方案可能会突然想到。

#### *2.10.9 克服低落士气*

没有什么比团队成员之间士气低落更能迅速摧毁一个项目了。以下是一些帮助你克服低落士气的建议：

+   了解项目的商业价值。通过学习或提醒自己项目在现实世界中的实际应用，你会更加投入和感兴趣。

+   对（你负责的部分）项目负责。当你拥有项目时，你的自豪感和声誉都在其中。无论发生什么，确保你始终能够谈论自己为项目做出的贡献。

+   避免对自己无法控制的项目组件产生过多情感投入。例如，如果管理层做出了一些影响项目进度或设计的错误决策，在这些限制条件下尽力工作。不要只是坐在那里对管理层心生不满，而是把精力投入到解决问题上。

+   如果你面临性格差异导致的士气问题，应该与经理和其他受影响的人员讨论这些问题。沟通是关键。允许问题继续下去只会导致未来更大的士气问题。

+   始终关注可能会破坏士气的情况和态度。一旦项目的士气开始下降，通常很难恢复失去的部分。越早处理士气问题，解决起来就越容易。

有时，财务、资源或人员问题会降低项目参与者的士气。作为一个优秀的程序员，你的工作是挺身而出，超越这些问题，继续编写优秀的代码，并鼓励项目中的其他人也这么做。这并不总是容易的，但没有人说成为一名优秀的程序员是轻松的。

### 2.11 更多信息

Bellinger, Gene. “项目系统。” 系统思维，2004 年。*[`systems-thinking.org/prjsys/prjsys.htm`](http://systems-thinking.org/prjsys/prjsys.htm)*。

Heller, Robert, 和 Tim Hindle. *基本经理：管理会议*. 纽约：DK Publishing，1998 年。

Humphrey, Watts S. *软件工程的一门学科*. 上塞德尔河，新泽西州：Addison-Wesley Professional，1994 年。

Kerzner, Harold. *项目管理：规划、调度与控制的系统方法*. 霍博肯，新泽西州：Wiley，2003 年。

Lencioni, Patrick. *会议致命：关于解决商业中最痛苦问题的领导寓言*. 旧金山：Jossey-Bass，2004 年。

Levasseur, Robert E. *突破性商务会议：共享领导力的实践*. 林肯，内布拉斯加州：[iUniverse.com](http://iUniverse.com)，Inc.，2000 年。

Lewis, James P. *项目规划、调度与控制*. 纽约：McGraw-Hill，2000 年。

McConnell, Steve. *软件项目生存指南*. 红蒙德，华盛顿州：Microsoft Press，1997 年。

Mochal, Tom. “在团队士气低迷时激励项目团队的创意方法。” TechRepublic，2001 年 9 月 21 日。*[`www.techrepublic.com/article/get-creative-to-motivate-project-teams-when-morale-is-low/`](http://www.techrepublic.com/article/get-creative-to-motivate-project-teams-when-morale-is-low/)*。

Wysocki, Robert K., 和 Rudd McGary. *有效项目管理*. 印第安纳波利斯：Wiley，2003 年。
