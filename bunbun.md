# 文文新闻报社

大家好，我们是 PLCT 实验室里负责编程语言和类型系统的理论与实现研究的社团。

+ 本文作为社团广告，将简要介绍本社的起源、工作内容、现状和我们的招募标准，并将不定期更新。
+ 本文将会假设读者具有社团所涉及的领域的相关知识，所以会有一定的阅读门槛。

### 动机

这个社团主要开发的项目是一个叫做 Aya 的编程语言和定理证明器（目前有一个[简单的官网](https://www.aya-prover.org)）。我们认为，近年编程语言的学术界的前沿研究已经达到了一个理论半饱和、需要和实践结合的状态（即，有很多存在于理论里的事物缺乏实际的实现）。其次，如果一个编程语言方面的工作仅存在于理论中，我们是很难发现它潜在的问题和全部的潜力的。如果我们能把一些功能实现出来，或许能从中发现更多的美妙的事实。我们并不是唯一持有这样观点的人，[这个幻灯片](https://www.jonmsterling.com/slides/sterling:2022:wits.pdf)的第 17 页也表达了这样的观点。

~~于是，我们以「为将来从事编程语言的研究做准备」为动机、「实现学术型（即能进行定理证明的）编程语言」为载体，社团成员的编程语言愿景为抓手、「类型论的范畴模型」引导方法论，打出一套定理证明的组合拳。~~

把学术研究实现在实际的编程语言里有以下好处：

- 实现出一个特性并且自己去用它写代码，我们才能对这个东西「有冇用」建立直观感受。
  - 我们可能会在论文中犯错，实现是很好的测试手段。实现出这些东西之后，我们才能真实可靠地进行测试和实验。如果我们有新的发现，这些发现都可以写成论文，比如[这种](https://arxiv.org/abs/1911.08174)。
- 实现编程语言本身就是一件很浪漫的事情（知乎用户 vczh 钦点的计算机三大浪漫之一）。
- 我们有 [@lazyparser](https://github.com/lazyparser) 和 PLCT 实验室的支持，所以我们把 PL（编程语言理论）知识给 CT（编译器技术）化很符合公司的主题。
- 数量不菲的理论工作者并没有较好的编程基础和足够的软件工程功底（不是所有人都有魔理沙或者胡渊鸣那种理论实践双修的素质）来开发用户友好的学术研究型编程语言（看看 Agda 有多难安装，就可以知道）。我们希望自己试一试，能不能在这方面做的更好。Lean 在这方面做了一些榜样。
- 高维类型论目前没有特别好用的实现。由于 Cubical Agda 使用了奇怪的约束系统编码立方类型论的「边界条件」导致目前 cooltt 成了全村的希望。但是 cooltt 的基础类型论 CCTT 过于复杂（这个理论需要的限制面语法太复杂了，等价于外延相等类型）。
- 类型论社区有严重的「准入门槛」（accessibility barrier）（例如立方类型论中把限制面称为「上纤维化」，但实际上在编程语言的角度理解这个概念完全不需要理解模型范畴），我们希望能为广大编程爱好者提供友好的学习资源。

在这些思考下，Aya 这个项目诞生了。此处我们提供一些历史资料：

1. 初始的项目提案是一个[腾讯文档](https://docs.qq.com/doc/DZGNTcnViekRJTmp3)（包含技术选型、愿景、时间安排计划等内容）
2. 在进行了 8 个月的开发后存在一次[开发总结](https://docs.google.com/document/d/1P4UnVW3C4n_vIyYfozSXBYs9SOzwGrnJD7QmmWcITp8/edit)（包含被诅咒的传说、永远的勿忘草、神明的造物、罪与罚）
3. 部分计划也被放进了一次演讲的 [slides](https://docs.google.com/presentation/d/1FIZnRzFUJK1AwMGMAil1wt7k1bbDRIdNeMb62FiB4QE/edit) 里
4. 后来在 Idris Developer's Meeting 上进行过一次分享，这里是 [slides](https://docs.google.com/presentation/d/1OnxX2WE3CV_EuBmHOKJwiKRxKytZ6Z7hNTKGiXq2h9E/edit)
5. 红黑树 [showcase](https://docs.google.com/presentation/d/1st0TeiIIe_voZ1mx52N4BqnPuxYALaEMHMjCg6Y40vY/edit)
6. TyDe workshop 上关于索引类型族的分享 [slides](https://docs.google.com/presentation/d/1Gv-2CymnE_9DLuMYbEtyfoNOPpggyMhm3feN1qR2LeU/edit)

### 近况和技术栈

我们已经实现了一个有如下证明能力的定理证明器：

+ 定义立方类型论里的内涵等号类型，背后是「扩展类型」（命名来自于[这篇论文](https://arxiv.org/abs/1705.07442)）
+ 定义自然数和整数以及这两个类型的一些交换律、结合律、分配律等基本性质
+ 定义带索引的红黑树，使用类型确保子节点黑高相同

并且为它搭载了一个文学编程模式和一个简易的语言服务器（language server）和配套的 [VSCode 插件](https://github.com/aya-prover/aya-vscode)。下一步的计划是实现包管理等工具链方面的功能，然后开始标准库（初具雏形）、元编程模式和 JIT 编译器的开发。

[这里](https://cha.fan/articles/3d9u3PXL2BMURmST2y8Q)有一篇文章介绍 Aya 编程语言截止 2021 年 8 月已经实现的一些比较有特色的功能。我们希望进一步吸取欧系编程语言理论研究中的成果。我们在 2022 年决定抛弃原本的类型论、转而实现完整的立方类型论，这次迁移花费了巨量的时间，截止 2022 年 9 月也没有完成。

我们始终使用最新版本的 Java 工具链（包含接近最新版本的 Gradle、ANTLR4、IntelliJ IDEA）、VSCode（用于开发编辑器插件）和 Git/GitHub 进行开发。截止本文发布，最新的版本是 Java 18。选择 Java 的原因已经[写在这里](https://cha.fan/articles/4RFySaAW8b7hEHXBknkz)了，这里不再赘述。

+ 我们广泛地使用新版本的 Java 语言特性（对于 C# 等竞争对手而言都是很古老的特性了），包括但不限于密封类、局部类型推导、结构体（record）、模式匹配等功能。
+ 由于 Java 标准库对于集合的抽象缺乏对可变性的控制，我们采用了第三方的集合框架 [kala](https://github.com/Glavo/kala-common)，也是一位社团成员的个人项目。
+ 我们使用 jlink 工具打包我们的项目，使得安装 Aya 编译器时不需要单独安装 Java 运行时，卸载 Aya 也不需要单独去卸载 Java 运行时（会比 Minecraft 容易安装许多）。通过 jpackage 我们可以进一步实现无脑的安装，实现对非计算机专家的高友好度。

### 愿景

- 我们希望能在软件安装上做到像 VSCode 或者 CoqIDE 一样简便。
- 我们希望能设计出 Lean4 的元编程框架一样美好的元编程框架（tactic system），并开发一个类似 [mathlib](https://github.com/leanprover-community/mathlib) 的数学形式化库。
- 我们希望能实现 [Arend 标准宏](https://arend-lang.github.io/documentation/standard-tactics)、[Agsy](https://github.com/frelindb/agsyHOL)、[Isabelle sledgehammer](https://isabelle.in.tum.de/website-Isabelle2009-1/sledgehammer.html) 等软件一样强大的命题求解器，这样可以大幅缓解入门门槛。
- 我们希望我们的编程语言可以被 JIT 编译到 Java 字节码，然后被 Java 虚拟机进一步 JIT 编译成机器码，实现很好的计算性能的同时达到编译的效果。使用 GraalVM 可以进一步把编译出的 Java 字节码静态编译成可执行文件。
- 我们希望能设计出一个适合用于博客和论文编写的文学编程模式。现在这个功能有一个[介绍视频](https://www.bilibili.com/video/bv1K64y1q7f3)，但是以后可能会有所改动。
- 我们希望能拥有一个尽可能强大的类型系统，并且至少拥有同伦类型系统的全部能力（注意，这不同于同伦类型论，见[这个文档](https://www.math.ias.edu/vladimir/sites/math.ias.edu.vladimir/files/HTS.pdf)）。
  - 目前我们寄希望于 [OTT](https://hal.inria.fr/hal-03367052/document) 和 [CTT](https://staff.math.su.se/anders.mortberg/papers/cubicalagda2.pdf) 结合的 [2LTT](https://arxiv.org/abs/1705.03307)。
- 我们希望使用 Aya 编程这件事很简单。
- 我们希望 Aya 的工具链在中国大陆可以被轻松地访问到。为此，我们目前计划使用国内高校的镜像源技术，并官方推广某个镜像源。
- 我们希望社员身心都健康，从社团活动中获得足够的知识和乐趣。

## 社团招新

[实习岗位 JD](https://github.com/lazyparser/weloveinterns/blob/master/open-internships.md)

重点来了。本社秉持「更多的人不一定带来更高的生产力」的观点，实行**高门槛招募**。如果你想要加入我们，我们期望你拥有如下素质，不过如果你在某一个特定的方面**特别优秀**的话，可以无视这个标准。事实上，目前的成员其实基本全都不满足所有的标准，但是这些人都「在特定的方面特别优秀」。如果你能加入这个团队，你将和这样的一群人共事！

+ 满足 PLCT 评级标准中的「[LV4 - 大能力者](https://github.com/lazyparser/weloveinterns/blob/master/how-do-we-rank-interns.md#lv4-大能力者)」的大部分要求，以及 PLCT 的[入职要求](https://github.com/lazyparser/weloveinterns/blob/master/so-you-want-to-join-us.md#%E4%BD%A0%E9%9C%80%E8%A6%81%E6%BB%A1%E8%B6%B3%E7%9A%84%E6%9D%A1%E4%BB%B6%E6%8A%80%E6%9C%AF%E5%B2%97%E4%BD%8D)。我们不要求掌握对于 LLVM 那种规模的怪兽级项目的拿捏能力，但是我们要求对于十万行 Java 代码这个规模的项目的掌控能力。编程语言方面，我们仅要求掌握 Java，但是熟悉 Haskell 或任意一个定理证明器（Agda, Coq, Lean, Idris, Nuprl, Isabelle, HOL, Andromeda, Arend, Beluga, Epigram, Dedukti, Cedille, Twelf, [Matita](http://matita.cs.unibo.it/) 等）或者逻辑编程语言（Prolog, Datalog）将会是一个很大的加分点。
+ 拥有基础的软件工程素养。你需要对面向对象编程（子类型多态、继承与子类型）、Java 编程（抽象类、接口等）、函数式编程（组合、数据不可变、惰性数据结构等思想）和设计模式（访问者模式、单例模式、工厂模式等）有一定熟悉程度，因为我们使用这些思想进行编程。你需要拥有良好的编程习惯，不要做出不格式化代码、提交 `.DS_Store`、仅局部使用的变量写成成员变量、在循环里使用 `+=` 拼接字符串、不跑测试就声称功能已完成、使用数组而不是集合类型存取数据等涉嫌气死 PR reviewer 的行为。有维护万行级别的代码的经验者为佳。
+ 会用开发工具，包括但不限于浏览器、Git/GitHub、IntelliJ IDEA 等工具。能在开源社区里和人打交道。
+ 对「依值类型系统」、「类型论」、和「同伦类型论」有一定的了解。这里有一个[参考学习路线](https://cha.fan/articles/5u9DV2LWWcjgJ8c7ha7T)。
+ 对事不对人的讨论态度、和其他社员（尤其是社长）撕逼的勇气。我们保持一个自由的氛围，在这个团队里没有什么条条框框，想说什么就说什么。对什么事情有意见，要大胆地说出来。不过在提意见的时候，我们希望你能提供一个解决方案，或者一些思路。

唯一的强制要求：

+ 对编程语言、类型系统方面的技术或是数学理论的有**强烈的兴趣**或者**个人利益上的关系**（例如：相关领域博士在读），**有强烈的求知欲**，能**接受失败**。本社的工作是学术研究，探索的是**全人类**在某一个小领域里的**最前沿**的技术，所以我们可能会面临**被同行犯的错误坑**、**被迫阅读过度复杂的算法**、**自己或者队友的失败**，可能会做出**根本不 make sense** 的垃圾功能，这样的代码我们肯定是要干掉的。我们要为此做好准备。

### 社团能给你带来的好处

+ 潜在的科研机会——如果你有一些编程语言或者类型系统方面的想法，在社员的帮助下，可以比起自己一个人更快地实现。我们可以教你写论文。
+ 跟进前沿研究、和拥有相似兴趣的人研讨技术的机会。
+ 获得特殊能力者帮助的机会，比如范畴论学习、类型论学习、写论文、组织代码等。
+ 学术界有很多秘密知识和神秘的名词仅通过口口相传得知（比如类型系统风格中的瑞典 vs 法国、演讲风格中的美国 vs 苏联、某些发明行不通的原因、一些奇奇怪怪的八卦等）。如果你目前并不身处学术界，却想了解这样的知识，本社可以为你带来这个机会。
+ 社团是 PLCT 的一份子，所以你也可以获取 PLCT 的资源，比如实习证明和实习工资。但是如果你想入职 PLCT，你需要有学校的在读证明或者社保缴纳证明。如果不能提供这两者之一，就只能成为编制外成员参与开发和讨论。
+ [weloveinterns/so-you-want-to-join-us.md#实习之后可以得到什么 · lazyparser/weloveinterns (github.com)](https://github.com/lazyparser/weloveinterns/blob/master/so-you-want-to-join-us.md#实习之后可以得到什么)

### 不能给你带来的好处

+ 我们都是活跃科研工作者或者尚未成为科研工作者的人（而不是高校里的导师），所以你不会像读博一样免费得到 idea。
+ 我们不会教你过于基础的知识（比如上面列出的），请自行学习。
+ 我们不会为你未来的就业负责，入行科研请[谨慎考虑](https://www.zhihu.com/question/307580157)。

如果你认为你想要加入本社，请联系本文的作者（`ice1000kotlin at foxmail dot com`），并尽可能按照[官方规定](https://github.com/lazyparser/weloveinterns/blob/master/open-internships.md#%E5%A6%82%E4%BD%95%E6%AD%A3%E7%A1%AE%E7%9A%84%E6%8A%95%E9%80%92%E7%AE%80%E5%8E%86)撰写邮件。我们会先行对你的能力进行考察，然后你会被推荐给 PLCT。理论上符合本社要求的能力者都是符合 PLCT 入职要求的。

我们的 GitHub 组织是 <https://github.com/aya-prover>。
