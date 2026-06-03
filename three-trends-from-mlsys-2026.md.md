# MLSys 2026 的三大趋势

translated from: https://www.modular.com/blog/three-trends-from-mlsys-2026



MLSys 2026 大会全面概述了当前研究和产业界推理技术的发展现状。今年的 LLM 专题研讨会共设六场（是去年的两倍），涵盖了 Modular 近期工作的核心机遇与挑战。Modular 很荣幸赞助此次大会，我们的团队注意到，在演讲、海报和主题演讲中，有三个趋势尤为突出。这些正是 Modular 一直以来从根本上着手解决的问题，而我们独特的技术栈正是解决这些问题的关键所在。

## 趋势一：智能体正在编写从内核到系统的一切内容。

周一的主题演讲奠定了基调。Mark Saroufim 的演讲“[*当人工智能开始编写系统代码”*](https://mlsys.org/virtual/2026/invited-talk/3655)展示了一些新手内核开发者使用人工智能代理编写内核的案例，这些案例足以让他们在竞争激烈的黑客马拉松比赛中名列前茅。随后，他以一种幽默的方式讽刺了这些代理的成就，演示了代理如何作弊通过基准测试，并优化那些永远无法在给定测试用例之外推广的结果。Saroufim 指出，与其等待一代始终遵守规则的代理出现，不如通过创建足够全面的基准测试来实现“零信任”验证，从而避免依赖于善意的提交。

周立东周二发表的主题演讲“[*系统的下一个阶段：从MLSys到系统智能”*](https://mlsys.org/virtual/2026/invited-talk/3665)指出，系统社区需要将人工智能代理视为底层代码的主要编写者。周立东展示了一个Rust微内核（Nanvix），该内核逐模块验证人工智能生成的规范和证明，在一个包含150个任务的证明生成基准测试中，其通过率从2%（GPT-4o，基于提示）提升至91.3%（经过微调并具有自调试功能的LLaMA-3.1 8B）。演讲还记录了模型在无法完成证明时采取的捷径：将代码封装起来`external_body`绕过验证器、植入错误的后置条件以及将证明负担转移给调用者。

这些讨论的共同结论是，智能工程在规范、设计和验证方面需要更加严格。

随后的演讲展示了智能体工程在内核和系统中的具体应用。AccelOpt [*：用于人工智能加速器内核优化的自改进LLM智能体系统，*](https://mlsys.org/virtual/2026/poster/10168)描述了一个闭环系统，其中LLM提出加速器内核变体，对其进行分析，并将结果反馈给自身。FlashInfer [*-Bench：在“机器学习在系统中的应用”环节中，构建人工智能驱动的LLM系统的良性循环，*](https://mlsys.org/virtual/2026/oral/3832)将此描述为一个反馈回路：基准测试的存在是为了给智能体提供优化目标。

这一切背后的内核作者痛点也直接显现出来。FlashAttention [*-4：面向非对称硬件扩展的算法与内核流水线协同设计，*](https://mlsys.org/virtual/2026/poster/3536)将其实现从 CUDA C++ 模板转移到嵌入 Python 的 CuTe-DSL，其明确目标是让下游开发者无需修改核心框架即可扩展内核。HipKittens [*：快速而强大的 AMD 内核*](https://mlsys.org/virtual/2026/poster/3512)和[*ParallelKittens：多 GPU AI 内核的系统化和实用化简化，*](https://mlsys.org/virtual/2026/oral/3845)都主张采用一套更简单的内核工程抽象。它们的共同假设是，人类内核作者不会为每一代加速器都编写一个新的模板森林，并且抽象对智能体的益处至少与对人类开发者的益处一样大。

### 模块化解决方案

模块化工程师和社区已经开始使用 Mojo 智能体编写代码，并探索其众多特性如何优化智能体工程。Mojo 强大的类型系统、高效的编译和清晰的错误信息，支持智能体开发与人工验证之间紧密的反馈循环。我们关于“[通过 AI 智能体将代码转换为 Mojo”](https://www.modular.com/blog/translating-to-mojo-via-ai-agents)的博文为此工作流程提供了实用指南。官方[`modular/skills`](https://github.com/modular/skills)软件包可与 Claude Code、Cursor 和其他编码智能体集成，并纠正模型可能产生的任何错误概念和过时模式。在博文中，Brad Larson 演示了如何将一个智能体从 CUDA softmax 内核（[Szymon Ożóg 的 FastSoftmax](https://github.com/SzymonOzog/FastSoftmax)）转换为可在 NVIDIA、AMD 和 Apple 芯片上运行的便携式 Mojo 版本，整个过程仅需一次会话。[Automatika Robotics](https://forum.modular.com/t/project-mojo-for-robotics-porting-gpu-navigation-kernels-jetson-strix-halo/2952)对其 EMOS/kompass-core 工作负载的自主导航内核进行了同样的优化，结果显示，在代理首次运行且未进行 Mojo 端优化的情况下，其运行时间为 15.973 毫秒，而 SYCL/CUDA 基线运行时间为 16.358 毫秒。Ehsan [Kermani 的另一篇博文](https://www.modular.com/blog/how-i-built-a-pure-mojo-app-and-10-libraries-with-ai-agents)也展示了如何通过有效的代理工程来创建经过全面测试并满足社区实际需求的 Mojo 库。

第二个联系点在内核端。模块化内核团队创建的可组合抽象已记录在我们的[“结构化 Mojo 内核”系列博客文章](https://www.modular.com/structured-mojo-kernels)中。这种模式将生产内核拆分为三个组件（TileIO、TilePipeline 和 TileOp），并使用上下文管理器来避免出现错误的同步情况。重写 B200 矩阵乘法器后，代码量从 14,683 行减少到 7,634 行，同时保持了 1770 TFLOPS 的稳定性能。“结构化 Mojo 内核”模式适用于 NVIDIA 和 AMD 平台，并且在[模块化代码库](https://github.com/modular/modular)中开源。这正是对 FlashAttention-4 维护问题的直接回应：一个足够简洁、便于人（或智能体）理解的内核层，其抽象层能够在硬件变更的情况下保持稳定，且性能不受影响。

## 趋势二：KV缓存成为主导子系统

KV缓存是本次大会上讨论最多的主题。周三下午的LLM Serving 3分会场实际上完全变成了KV缓存分会场，连续六篇论文都围绕这个主题展开。

刘宇涵在题为[*《LMCache：面向企业级LLM推理的高效键值缓存层》*](https://arxiv.org/abs/2510.09665)的演讲中直接阐述了其架构论证。该论文将键值缓存视为一等数据结构，而非推理的内部副产品，并指出实际部署中键值缓存的使用量已超过GPU内存：在超过五周的遥测数据中，绝大多数存储的键值缓存已无法容纳在GPU上，而每个用户的令牌重用率增长超过19%。该系统目前支持八种存储后端（NFS、WEKA、GPU-Direct Storage、Mooncake Store、NIXL、S3、InfiniStore、Valkey），涵盖四种处理器类型（NVIDIA、AMD、Ascend、TPU）和两种推理引擎（vLLM、SGLang）。如此广泛的覆盖范围至关重要。由于其底层存储和计算硬件并非同质，因此缓存层必须具备可移植性。

这些论文共同描述了同样的转变。键值缓存（KV缓存）日益分布式、异构化和复杂化，其放置、传输、驱逐和重用策略涵盖了GPU内存、主机DRAM、本地磁盘和分布式存储。这一趋势发展到如今，已经出现了专门用于缓存的定制芯片市场：[Netpreme](https://netpreme.com/)正在构建一款采用网络内存分层的内存处理单元（MPU），其卖点是将XPU内存扩展100倍。当一个子系统开始吸引自己的硬件供应商时，它就不再仅仅是实现细节了。

其他优化缓存的技术包括量化和稀疏性，它们结合使用可以直接控制内存需求。Kitty [：采用动态通道精度提升的精确高效的 2 位 KV 缓存量化技术，](https://openreview.net/forum?id=r3mQiuYKIN)在相同的内存预算下，通过支持 8 倍更大的批次来提高吞吐量。SGLang 团队的[HiSparse：利用分层内存增强稀疏注意力机制](https://www.lmsys.org/blog/2026-04-10-sglang-hisparse/)（Christos Kozyrakis 在周五关于推理效率的主题演讲中重点提到了这项技术）将稀疏注意力机制与分层内存层相结合：GPU 维护一个用于存储频繁访问的 KV 区域的热设备缓冲区，而将不活跃的条目卸载到主机内存中。其结果是，在 GLM-5.1-FP8 的长上下文工作负载下，吞吐量最高可提升 5 倍。量化减少了缓存的存储成本，稀疏性减少了引擎需要关注的数据量，而将二者结合使用则是解决长上下文推理问题的实用方案。

共同点是，缓存从引擎中分离出来，变成了一个独立的分布式系统，拥有自己的调度、自己的存储分层和自己的重用语义。

### 模块化解决方案

[Brian Zhang 在他的博文《KVCache 的五个时代](https://www.modular.com/blog/the-five-eras-of-kvcache)》中描述了这一趋势。该博文追溯了缓存的演进历程：从 2023 年的本地引擎内优化，到 PagedAttention、前缀缓存和卸载，最终发展到缓存统一、分布式且可在异构基础设施上组合的时代。MLSys 2026 的论文共同记录了这一持续进行的工作。

要了解分布式键值缓存如何在集群层面工作，请查看 Modular 博客上的推理路由系列文章。其中一篇题为[*《为什么 LLM 推理需要一种新型路由器》的文章*](https://www.modular.com/blog/why-llm-inference-needs-a-new-kind-of-router-part-1)论证了路由决策和键值缓存状态密不可分，路由器必须具备缓存感知能力，而累积链接和位图索引正是实现大规模应用的关键。从更宏观的角度来看，Kyle Caverly 对[MAX Serve 从提示到响应的详细讲解](https://youtu.be/hewZwTwDBcM?si=gZX08UlKiPDRTE4r)，很好地阐释了键值缓存在整个推理平台中的作用。MLSys 的论文描述了多种高效的键值缓存管理方法。这些论文印证了 Modular 多年来致力于构建的方案的紧迫性。Modular Cloud 实现了一种可组合的大规模分布式推理方法，该方法可跨硬件运行，并能灵活应对不断变化的优化。

## 趋势三：推理工作负载正在利用异构硬件

在 MLSys 2026 大会上，异构性贯穿了所有六个 LLM 服务课程以及两个行业服务专题研讨会。Esha Choukse 在第一天的特邀演讲“[*超越模型服务：面向智能体的跨栈协同设计”*](https://mlsys.org/virtual/2026/invited-talk/3650)[ ](https://mlsys.org/virtual/2026/invited-talk/3650)奠定了框架：硬件多样性是高效服务于交互式、多模态和智能体的先决条件。

Meta 的行业论文[*《优化 LLM 推理的部署配置》*](https://mlsys.org/virtual/2026/oral/3780)展示了异构性的优势，即使在单模型部署中也是如此。该论文记录了通过在一种加速器上运行预填充、在另一种加速器上运行解码，可以降低 15% 到 25% 的总拥有成本 (TCO)，因为预填充受限于计算能力（倾向于高 FLOP/s），而解码受限于内存带宽（倾向于高 HBM 带宽）。NVIDIA 在同一会议中发表的《[*超越喧嚣：推理分离的务实之道》*](https://mlsys.org/virtual/2026/oral/3819)承认预填充-解码分离是真实且有价值的，但前提是速率匹配、键值传输、缓存路由和弹性扩展等问题能够同时得到解决。BOute[*的论文《通过多目标贝叶斯优化实现异构 LLM 和 GPU 的低成本 LLM 服务》*](https://mlsys.org/virtual/2026/oral/3795)将选择哪个模型运行在哪个加速器上视为一个搜索问题。 TriInfer：混合 EPD 分解，用于在多模态和生成模型会议中[*高效地进行多模态大型语言模型推理，将分解从两个阶段扩展到编码-预填充-解码，以用于多模态工作负载。*](https://mlsys.org/virtual/2026/oral/3756)

针对特定硬件的内核工作表明了这一点的重要性。SuperInfer [*：面向超级芯片的 LLM 推理的 SLO 感知旋转调度和内存管理，*](https://mlsys.org/virtual/2026/oral/3809)发现现有的卸载框架对 GH200 上的 NVLink-C2C 互连的利用率不足其 900 GB/s 容量的 5%，因为它们将其视为 PCIe 互连。该论文总结道，瓶颈在于软件栈。SHIP [*：用于快速 LLM 服务的基于 SRAM 的大型推理流水线，*](https://mlsys.org/virtual/2026/oral/3834)描述了 Groq 基于 LPU 的服务栈，其中整个模型都可放入 SRAM 中，编译器以周期粒度静态调度集体通信。TokenWeave [*：用于分布式 LLM 推理的高效计算通信重叠，*](https://mlsys.org/virtual/2026/oral/3744)依赖于 PyTorch 的 SymmetricMemory API 和 NVLink4 的 NVSHARP 引擎，这两者的存在正是因为厂商特定的集体通信路径不再符合内核作者的工作方式。

异构硬件在多模态推理和成本优化方面具有优势，但可能会受到供应商特定软件栈的限制。

### 模块化解决方案

MAX 从底层设计就充分考虑了硬件多样性。一个容器即可运行在 NVIDIA GPU、AMD GPU 和 CPU 上。内核层采用 Mojo 编写，它会针对每个硬件目标进行编译，而不是封装厂商特定的库。运行时环境能够感知硬件，但并非特定于某个硬件。

[在实际工作负载（例如Hippocratic AI](https://www.modular.com/blog/hippocratic-ai-partners-with-modular-to-power-flexible-high-quality-inference-for-real-time-patient-conversations) ）上运行时，MAX 的平均 TTFT 低于 500 毫秒，P99 端到端速度提升约 30%，在 NVIDIA B300 GPU 上处理 4000 亿以上参数模型时，平均端到端速度比 SGLang 快 22%。与 B200 上的 vLLM 相比，Modular 的堆栈在 Kimi-K2.5 上的 P50 TTFT 速度提升 5.5 倍，在 Gemma-4-31B-it 上的 P99 TTFT 速度提升 2.5 倍，两者的吞吐量均提升 1.5 倍。在相同的软件堆栈中，Flux.2-dev 图像生成工作负载在 B200 上的运行速度比 PyTorch Diffusers 快 6.9 倍，在 AMD MI355x 上快 3.8 倍。您可以在[Modular 的 MLSys 闪电演讲](https://mlsys.org/virtual/2026/sponsor-lightning-talk/10024)`torch.compile`中了解更多关于 MAX 卓越性能的信息。

高效的推理服务需要充分利用所有可用硬件的潜力，以满足不断变化的行业需求。MLSys 2026 会议将分别探讨推理栈的各个组成部分并进行独立优化，例如内核、键值缓存、服务等。模块化设计将整个栈重写为一个单一系统，使我们能够从内核到云端进行全面优化。这种方法使我们能够始终处于研究前沿，并实现覆盖整个栈的优化。

感谢各位莅临 Modular 展位，与我们探讨我们的技术栈和[招聘职位。](https://www.modular.com/company/careers)如果您有兴趣为我们的[开源项目](https://github.com/modular)做贡献或参与研究合作，欢迎访问[我们的论坛](https://forum.modular.com/)与我们联系。我们期待参加 MLSys 2027，届时我们将分享研究成果和正在进行的创新。明年见！