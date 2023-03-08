---
title: "教程"
subtitle: "概述"
---

Tokio 是 Rust 编程语言的异步运行时。 
它提供了编写网络应用程序所需的构建块。
它提供了针对各种系统的灵活性，
从具有数十个内核的大型服务器到小型嵌入式设备。

在高层次上，Tokio 提供了几个主要组件：

 - 用于执行异步代码的多线程运行时。
 - 标准库的异步版本。
 - 一个庞大的图书馆生态系统。

# Tokio 在您的项目中的角色

以异步方式编写应用程序时，
可以通过降低同时执行许多操作的成本来使其更好地扩展。
但是，异步 Rust 代码不会自行运行，
因此您必须选择一个运行时来执行它。
Tokio 库是使用最广泛的运行时，
超过了所有其他运行时的总和。

此外，Tokio 还提供了许多有用的实用程序。
在编写异步代码时，
你不能使用 Rust 标准库提供的普通阻塞 API，
而必须使用它们的异步版本。
这些替代版本由 Tokio 提供，反映了 Rust 标准库的 API。

# Tokio 的优势

本节将概述 Tokio 的一些优点。

## 快

Tokio 很 _快_，建立在 Rust 编程语言之上，
它本身就很快。这是本着 Rust 的精神完成的，
目标是你不应该能够通过手动编写等效的代码来提高性能。

Tokio 是 _可扩展的_ ，建立在 async/await 语言功能之上，
该功能本身是可扩展的。在处理网络时，由于延迟，
处理连接的速度是有限的，
因此扩展的唯一方法是一次处理多个连接。
使用 async/await 语言功能，
增加并发操作的数量变得非常便宜，
允许您扩展到大量并发任务。

## 可靠

Tokio 是使用 Rust 构建的，
Rust 是一种使每个人都能够构建可靠和高效软件的语言。
[许多][microsoft][研究][chrome]发现，大约 70% 的高严重性安全漏洞是内存不安全的结果。 
使用 Rust 消除了在你的应用程序中的这一整类错误。

Tokio 还非常注重提供一致的行为，没有意外。
Tokio的主要目标是允许用户部署可预测的软件，
这些软件将以可靠的响应时间和不可预测的延迟峰值日复一日地执行。

[microsoft]: https://www.zdnet.com/article/microsoft-70-percent-of-all-security-bugs-are-memory-safety-issues/
[chrome]: https://www.chromium.org/Home/chromium-security/memory-safety

## 容易

借助 Rust 的 async/await 功能，
编写异步应用程序的复杂性大大降低。
结合 Tokio 的实用程序和充满活力的生态系统，编写应用程序轻而易举。

Tokio 在有意义时遵循标准库的命名约定。
这可以轻松地将仅使用标准库编写的代码转换为使用Tokio编写的代码。
借助 Rust 的强大类型系统，轻松交付正确代码的能力是无与伦比的。

## 灵活

Tokio 提供了运行时的多种变体。 
从多线程、[工作窃取]运行时到轻量级、单线程运行时的一切。 
这些运行时中的每一个都带有许多旋钮，
允许用户根据自己的需要调整它们。

[work-stealing]: https://en.wikipedia.org/wiki/Work_stealing

# 何时不使用Tokio

虽然Tokio对于许多需要同时做很多事情的项目很有用，但也有一些用例Tokio不太合适。

 - 通过在多个线程上并行运行它们来加速 CPU 密集型计算。 
   Tokio 专为 IO 密集型应用程序而设计，
   其中每个单独的任务都将大部分时间花在等待 IO 上。 
   如果您的应用程序唯一要做的就是并行运行计算，
   那么您应该使用[rayon]。 也就是说，如果您需要两者兼顾，仍然可以“混合搭配”。
 - 读取大量文件。尽管看起来 Tokio 对于
   只需要读取大量文件的项目很有用，
   但与普通线程池相比，Tokio 在这里没有任何优势。
   这是因为操作系统通常不提供异步文件 API。
 - 发送单个 Web 请求。 
   Tokio 给你带来优势的地方是当你需要同时做很多事情的时候。 
   如果您需要使用用于异步 Rust 的库，例如 [reqwest]，
   但您不需要一次做很多事情，您应该更喜欢该库的阻塞版本， 
   因为它会使您的项目更简单。 
   当然，使用 Tokio 仍然有效，
   但与阻塞 API 相比并没有真正的优势。 
   如果库不提供阻塞 API，请参阅[桥接同步代码一章][bridging]。

[rayon]: https://docs.rs/rayon/
[reqwest]: https://docs.rs/reqwest/
[bridging]: /tokio/topics/bridging

# 获取帮助

在任何时候，如果你遇到困难，你总是可以在[Discord]或[Discord] or [GitHub
discussions][disc]上获得帮助。不要担心问“初学者”问题。我们都从某个地方开始，并乐于提供帮助。

[discord]: https://discord.gg/tokio
[disc]: https://github.com/tokio-rs/tokio/discussions
