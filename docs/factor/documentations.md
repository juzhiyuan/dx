---
layout: default
title: 文档体验设计
parent: 开发者体验设计因子
nav_order: 1
---

# 开发者体验：文档体验设计
{: .no_toc }

## 目录
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 文档体验设计（TBD）

### 模式：

## 文档工程体验（面向文档工程师）

### 文档编写的痛点

在编写文档时，常见的一些痛点有：

* 文档代码不同步。即文档的 API 变化可能落后于代码，导致 API 与文档出现不一致。
* 频繁的 API 变更。API 变更时，文档需要手动进行更新，不能自动化同步。
* 概念不统一。对于同一个概念，文档的不同地方描述不一致。
* 重复的文档块。文档需要重复引用某一部分的文档，不能像代码一样引用。
* 代码无法运行。按照文档的步骤下来编写的代码、复制的代码，是不能运行的。

还有一些问题，可能是难以通过自动化的方式来解决的，诸如于：

* 风格不一致。不同的人编写文档的风格不一致，可能需要类似于 code review 的 document review 的方式来解决。
* 语法不准确。使用的是不同形式的中文描述方式。（PS：难道是回去再上上语文课）

于是，我们可以尝试性地借用业内一些通用的方式来解决问题。

### 定义文档工程体验

再回到标题上，让我对标题做一些解释：

文档工程用于帮助我们指定、设计、和实施计算机技术相关的文档，如产品特定规格或详细说明，以及创建和使用它们的流程。它的特点是以“文档为中心”，以帮助我们构思和理解如何支撑其所在的商业模式。

而文档工程体验设计，则是围绕于构建和设计文档的过程进行的体验改善。即目标用户是**编写文档的工程师**，改善其编写文档的体验。并针对于文档的目标用户，改善他们在文档方面的体验（PS：这部分不是本文讨论的重点）。

文档体验是开发者体验的一个关键性因素，用于指导新手快速上手技术产品。在我们设计各类[开发者体验指标](https://www.phodal.com/blog/developer-experience/)时，一个非常重要的指标就是 TTFHW（Time to first hello world），即从零到第一个 Hello World 需要的时间，而这个指标是严重依赖于开发者文档。

因此，本文的意图是从文档开发者的体验出发，以重新塑造整体的开发者体验。

既然文档工程体验归属于开发者体验，它面向的是开发者提供更好体验，对于自身而言，更需要非凡的体验。只有以此为出发点，才能减小文档团队人员的流 动，毕竟不是程序员想写文档，也不是程序员都想看文档的。

## 卓越文档工程体验要素

作为一个程序员，我设计和参与过两个文档系统（Ledge 便是其中之一），它们之间有各自不同的思想。再结合我对于多个语言的文档体系的分析和设计，我觉得一个优秀的文档工程应该是满足这样的条件：

* 编辑-发布分离。架构设计上，编辑态和发布是完成分离的，各自可以使用不同的语言和技术来实现，诸如于使用 markdown 编写，但是输出可以是丰富多彩的形式。
* 过程自动化。特别好理解，它应该能实现快速的自动化发布，以代码开发保持一致和构建频繁。
* 文档形式化。XML 是上一个世代比较流行的文档形式化格式，从我的研究情况来看，定制化的 markdown  是这一个世代流行的方式。形式化的输入，它便意味着在输出上会有多种形式，如 markdown 结合 Pandoc 可以转换为 PDF、Word、HTML 等一系列的格式。
* 开放式协作。文档面向使用者开放修改，使用者可以通过 pull request 的形式来对文档进行改进，并可以针对文档提出建议。
* 版本化管理。在编辑态上，所有的历史修改都是可见的，可以回溯所有变更；在发布上，可以看到关键的历史版本，以适应不同人的需求。一种特别简单的示例，就是使用 git 来版本。
 
对于多数语言、框架的文档系统来说，它们都是面向特定领域定制的，以带来更好的编写体验和一致性。所以，从某种意义上来说，定制化开发也是非常重要的一点 —— 即我们往往难以获得一个通用的解决方案。

### 面向场景设计呈现

除了上述的要素之后，我们还需要提及一个非常重要的因素，即针对于不同的场景，应该要有不同的文档呈现形式。诸如于：

 - 一页文档。诸如于搭建指南，在项目初始化的时候，可以在一个网页内快速完成，而不需要进页面挑战。
 - 模块化文档。诸如于面向 API / SDK 场景下，以让每**部分** API 都可以独立访问，也能通过搜索引擎优化。
 - 可交互文档。诸如于编程语言 REPL、组件库场景下，让用户可以零成本学习和试用技术产品。
 - ……

尽管文档很重要，但是请不要忘了，我们的初衷是带来更好的用户体验。

## 文档编程模式

为了更方便于讨论，我尝试性对所接触的文章进行了模式上的分类，以及它们所适用的场景：

| 模式                | 场景                                         | 优点                         | 缺点                  | 一致性机制               | 原则                 | 
|---------------------|----------------------------------------------|------------------------------|-----------------------|--------------------------|----------------------|
| 文档代码化 | 需要协作的在线文档、侧重于开发指南编写       | 提升社区参与度、灵活扩展系统 | 实现成本略高          |                          | 以领域特定语言为核心 |
| 文档测试            | SDK、API 等功能性描述文档                    | 文档代码强一致性             | 实现成本略高          | 编译时保证               | 注释设计             |
| 可执行文档          | 文档为核心，代码为辅助、Demo 编写            | 轻量、文档一致性             | 大型工程比较难 handle | 编译时保证               | 文档优先             |
| 灵活代码块          | 代码为核心，文档为辅助、Demo 编写            | 动态响应代码变化             | 注释在 demo 代码中    | 代码正确编译，则文档正常 | 代码优先             |
| 测试即文档          | 业务系统开发，文档为核心，确保文档和代码一致 | 文档代码强一致性             | 实现成本略高          | 持续集成时保证           | 文档驱动开发         |
| 文档同构            | 文档驱动开发、业务系统开发                   | 文档代码强一致性             | 实现成本高            | 双向确保代码-文档一致    | 双向绑定             |

在文档工程这个上下文下，其详细的定义如下。

### 基础模式：文档代码化

定义：文档代码化是将文档以类代码的领域特定语言的方式编写，并借鉴软件开发的方式（如源码管理、部署）进行管理。 它可以借助于特定的工具进行编辑、预览、查看，又或者是通过专属的系统部署到服务器上。

示例：各类的开源软件文档、Rust、Julia 等编程语言的文档系统

文档代码化其中是现代化的文档工程里的基石。现有的开源软件文档体系，都是以 markdown + 开源的形式而展开的，所有的人都可以在这之上进行协作。除此，基于不同文档的需求，它们会在 DSL 的基础上进行扩展，如新一代的编程语言的文档系统。它们的方式是这样的：

1. 为扩展设计：文档 DSL
2. 为准确性设计：文档测试
3. 构建开放协作平台：开放协作

更详细可以参考：《[API 库的文档体系支持：主流编程语言的文档设计](https://www.phodal.com/blog/api-ducumentation-design-dsl-base/)》

### 文档测试：一致性

定义：文档测试的原始定义是，一种测试方式，用于确保系统的文档与系统的功能相匹配。在文档工程的上下文里， 我们定义为针对于文档中的代码验证其有效性，以及其结果的准确性。

示例：Rustdoc、DocumenterTools.jl

如在 Rustdoc 中**代码中的注释中的代码**会被提取出来，它会被独立编译，确保代码是可运行的。

```
  ```rust
assert_eq!(2 + 2, 4);
  ```
```

如下是 Rustdoc 中将上述的代码生成测试代码的测试用例：

```rust
fn main() {
   #[allow(non_snake_case)]
   fn _doctest_main__some_unique_name() {
       assert_eq!(2 + 2, 4);
   }
   _doctest_main__some_unique_name()
}
```

一旦上述的代码编译并运行通过，则说明文档中的注释是正确的。具体的步骤如下：

- 解析 markdown，寻找 Rust 语言的语法块（如果没有标注语言类型，默认是 Rust）
- 根据语法块，做一些简单的处理，生成可编译的代码
- 编译上述的测试代码 （如果编译失败，则说明测试失败）
- 运行这些测试 or 文档

详细见 Rustdoc 相关源码：[librustdoc](https://github.com/rust-lang/rust/tree/master/src/librustdoc)

### 可执行文档

定义：可执行文档是指文档本身已经是代码化的结果，它像代码一样可以执行， 并且可以将结果动态地与文档结合在一起。

示例：Julia 的 DocumenterTools、R Markdown、Exemd

在 R Markdown 里，它可以结合文档与 R 语言源码，可以进行动态的渲染。我们可以在 markdown 文件中，“随意”地调用 R 中的函数，并动态地嵌入数据、代码、计算结果、可视化图表等到输出的文档中。在结合了 Pandoc 之后，文档可以输出到所有主流的文档格式。如下的示例：

```markdown
    ```{r fig.show='animate', dev='jpeg', ffmpeg.format='gif'}
    for (i in 1:10) plot(runif(100), ylim = c(0, 1)) # for example
    ```
```

它将会运行并在文档中嵌入运行的结果。

### 灵活代码块

定义：灵活代码块是指文档可以通过 DSL 动态引用源码中的内容。

示例：DocumenterTools.jl、Forming 里的 Writing

以我设计的 Writing 为例，它可以动态解析 markdown 中设计的 Writing DSL，并从代码中读取对应的代码块。如下是 Writing 的示例：

```
// doc-code: file("src/lib.rs").line()[2, 5]
// 读取 "src/lib.rs" 文件的第 2 到第 5 行
// doc-section: file("src/lib.rs").section("section1")
// 读取 "src/lib.rs" 文件中的 section1 相关的代码块
```

通过简单的自定义函数，将文档与代码有机结合到一起。只要应用编译运行成功，那么文档本身也是正确的。

### 测试即文档

定义：测试即文档即指测试用例以文档的形式编写，文档本身就是测试用例。

示例：Cucumber 

相信大家都很“熟悉”了，主要是在自动化测试中使用非常广泛。Cucumber 示例如下：

```cucumber
# language: zh-CN
@math
功能: 加法
 加法计算器的验证用例

 @sanity
 场景: 两个数相加
   假如我已经在计算器里输入6
   而且我已经在计算器里输入7
   当我按"相加"按钮
   那么我应该在屏幕上看到的结果是13
```

测试是文档，文档即是测试。

### 文档同构（概念）

文档同构。[文档同构](https://www.phodal.com/blog/isomorphism-document/) 是一种将代码与文档保持一致的技术理念，它能读取格式化的文档，并将文档自动加入到代码中，如以注释的形式或者是只在 IDE 呈现；同时，还能将读取代码中的文档，自动更新到文档中，或是对文档进行测试和差异对比。