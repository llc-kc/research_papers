# MLSys 2026 论文摘要（按主题分类）

> 共 173 篇论文 | 129 篇完整中英双语翻译 | 2026-06-03

---


# LLM 推理服务（75 篇）


## [AgenticCache: Cache-Driven Asynchronous Planning for Embodied AI Agents](https://mlsys.org/virtual/2026/poster/3583)


**英文摘要 (English Abstract)**:

Embodied AI agents increasingly rely on large language models (LLMs) for planning, yet per-step LLM calls impose severe latency and cost. In this paper, we show that embodied tasks exhibit strong plan locality, where the next plan is largely predictable from the current one. Building on this, we introduce AgenticCache, a planning framework that reuses cached plans to avoid per-step LLM calls. In AgenticCache, each agent queries a runtime cache of frequent plan transitions, while a background Cache Updater asynchronously calls the LLM to validate and refine cached entries. Across four multi-agent embodied benchmarks, AgenticCache improves task success rate by 22% on average across 12 configurations (4 benchmarks × 3 models), reduces simulation latency by 65%, and lowers token usage by 50%. Cache-based plan reuse thus offers a practical path to low-latency, low-cost embodied agents. Code is available at https://github.com/hojoonleokim/MLSys26_AgenticCache.


**中文摘要**:

具身AI智能体越来越依赖大语言模型进行规划，然而每一步LLM调用都会带来严重的延迟和成本。本文发现，具身任务表现出很强的计划局部性——下一步计划在很大程度上可从当前计划中预测。基于此，我们提出AgenticCache，一个通过重用缓存计划来避免每步LLM调用的规划框架。在AgenticCache中，每个智能体查询一个包含频繁计划转移的运行时缓存，而后台缓存更新器则异步调用LLM来验证和优化缓存条目。在四个多智能体具身基准测试中，AgenticCache在12种配置（4个基准×3个模型）下平均将任务成功率提高22%，将仿真延迟降低65%，并将token使用量减少50%。因此，基于缓存的计划重用为低延迟、低成本的具身智能体提供了一条实用路径。代码见 https://github.com/hojoonleokim/MLSys26_AgenticCache。


---


## [ADAPTIVE ERASURE CODING FOR FAULT-TOLERANT LLM SERVING WITH CONTINUOUS BATCHING](https://mlsys.org/virtual/2026/poster/10186)


**英文摘要 (English Abstract)**:

(Abstract not publicly available - requires login)


**中文摘要**: [待翻译]


---


## [ForeCache: Understanding Workloads and Optimizing KVCache Management for Efficiently Serving LLM Coding Agents](https://mlsys.org/virtual/2026/poster/10200)


**英文摘要 (English Abstract)**:

(Abstract not publicly available - requires login)


**中文摘要**: [待翻译]


---


## [BioTriton: Portable Cross-Vendor GPU Kernels for High-Throughput Bioinformatics via OpenAI Triton](https://mlsys.org/virtual/2026/poster/10183)


**英文摘要 (English Abstract)**:

Training large Mixture-of-Experts (MoE) models remains computationally prohibitive due to their extreme compute and memory demands. Although low-precision training promises to accelerate computation and reduce memory footprint, existing implementations still rely on BF16-dominated dataflows with frequent quantize–dequantize (Q/DQ) conversions. These redundant casts erode much of FP8's theoretical efficiency. However, naively removing these casts by keeping dataflows entirely in FP8 introduces double quantization error: tensors quantized along different dimensions accumulate inconsistent scaling factors, degrading numerical stability. We propose FP8-Flow-MoE, an FP8 training recipe featuring a quantization-consistent FP8-centric dataflow with a scaling-aware transpose and fused FP8 operators that streamline computation and eliminate explicit cast operations from 12 to 2. Evaluations on a 671B-parameter MoE model demonstrate up to 21% higher throughput and 16.5 GB lower memory usage per GPU compared to BF16 and naïve FP8 baselines, while maintaining stable convergence. We provide a plug-and-play FP8 recipe compatible with TransformerEngine and Megatron-LM, with the reference implementation available at our GitHub repository.


**中文摘要**: [待翻译]


---


## [REMIX: Dynamic Partitioning for Fine-Grained Heterogeneous LLM Serving](https://mlsys.org/virtual/2026/poster/10182)


**英文摘要 (English Abstract)**:

Modern ML models demand ever-greater compute, prompting hardware vendors to add specialized matrix cores to their GPUs. While these units unlock high throughput, they impose intricate programming models and addressing schemes that are difficult to manage by hand. This paper introduces Wave, a Python-embedded DSL for kernel authoring that automates these complex address computations and lets authors focus on core computation. In experiments, it matches or surpasses the performance of state-of-the-art kernel DSLs and libraries.


**中文摘要**:

针对通过模型复用降低LLM推理基础设施成本的日益增长的需求，我们提出REMIX，一个高效且自适应的异构LLM服务系统。REMIX通过动态模型分区解决了将不同模型部分分配到异构GPU上的挑战，根据每个请求的特征和当前集群负载动态调整分区策略。这种方法最大化了异构GPU集群上的资源利用率，同时满足延迟SLO。实验表明，REMIX在异构GPU集群上相比静态分区策略将服务吞吐量提高了高达1.5倍。


---


## [FlexiCache: Leveraging Temporal Stability of Attention Heads for Efficient KV Cache Management](https://mlsys.org/virtual/2026/poster/3615)


**英文摘要 (English Abstract)**:

Large Language Model (LLM) serving is increasingly constrained by the growing size of the key-value (KV) cache, which scales with both context length and generation length. We introduce FlexiCache, a hierarchical KV-cache management system that leverages the temporal stability of KV heads to reduce GPU memory usage and computation overhead, while preserving model accuracy. FlexiCache classifies KV heads as stable or unstable: it retains all KV-cache pages from unstable heads in GPU memory, whereas for stable heads, it keeps only the top-K pages on the GPU and offloads the rest.


**中文摘要**:

大语言模型服务越来越受到键值缓存大小增长的制约，该缓存随上下文长度和生成长度而扩展。先前工作表明注意力由一小部分关键token主导，但现有系统难以在不降低精度的情况下有效利用这一点，尤其在长生成长场景中。我们做出一个关键观察：这些关键token的时间稳定性在不同KV头之间差异显著——一些头持续关注相同的token，而其他头频繁变化。基于这一洞察，我们引入FlexiCache，一个利用KV头时间稳定性来减少GPU内存使用和计算开销的层次化KV缓存管理系统，同时保持模型精度。FlexiCache将KV头分类为稳定或不稳定：它保留不稳定头的所有KV缓存页在GPU内存中，而对于稳定头，它只在GPU上保留top-K页并将其余卸载到主机内存。通过利用时间稳定性，FlexiCache对稳定头执行定期重排以获取新晋升的top页。基于vLLM实现，FlexiCache将长上下文请求的GPU内存占用降低高达70%，将离线服务吞吐量提高1.38-1.55倍，并将在线token延迟降低1.6-2.1倍，同时在长上下文、长生成长场景中保持精度。


---


## [Cascade: Utility-Driven Speculative Decoding for Mixture-of-Experts](https://mlsys.org/virtual/2026/poster/10189)


**英文摘要 (English Abstract)**:

The exponential increase in Machine Learning (ML) model size and complexity has driven unprecedented demand for high-performance acceleration systems. As technology scaling enables the integration of thousands of computing elements onto a single die, the boundary between distributed and on-chip systems has blurred, making efficient on-chip collective communication increasingly critical. In this work, we present a lightweight, collective-capable Network on Chip (NoC) that supports efficient barrier synchronization alongside scalable, high-bandwidth multicast and reduction operations, co-designed for the next generation of ML accelerators. We introduce Direct Compute Access (DCA), a novel paradigm that grants the interconnect fabric direct access to the cores' computational resources, enabling high-throughput in-network reductions with a small 16.5% router area overhead. Through in-network hardware acceleration, we achieve 2.9× and 2.5× geomean speedups on multicast and reduction operations involving between 1 and 32 KiB of data, respectively. Furthermore, by keeping communication off the critical path in GEMM workloads, these features allow our architecture to scale efficiently to large meshes, resulting in up to 2.1× and 2.1× estimated performance gains through multicast and reduction support, respectively, compared to a baseline unicast NoC architecture.


**中文摘要**:

在混合专家模型中，推测解码的实用性受限于草稿模型在多个专家间的分布。Cascade提出了一种效用驱动的推测解码方法，通过分析每个专家的推测质量来动态决定哪些专家参与草稿生成。系统根据历史推测接受率评估每个专家的效用，优先选择高价值专家生成草稿token，避免了在低效用专家上的浪费计算。在多种MoE模型上的评估表明，Cascade在保持生成质量的同时将推测解码的计算开销降低了高达40%。


---


## [PLA-Serve: A Prefill-Length-Aware LLM Serving System](https://mlsys.org/virtual/2026/poster/3564)


**英文摘要 (English Abstract)**:

LLM inference is computationally expensive due to the LLM's large parameter sizes. Existing techniques reduce the computing cost via model retraining, but cannot well adapt to different downstream tasks or variant input data at runtime. To avoid such retraining efforts for runtime adaptability, a better option is sparse activation that selectively deactivates an input-dependent set of neurons in inference, but current methods of lossless sparse activation only deactivate neurons with zero output magnitudes, and are ineffective on recent LLMs with higher parameter efficiency. In this paper, we present a new technique of attribution-based sparse activation, which is a lossy sparse activation technique that deactivates neurons with low attribution scores and aims to achieve the best tradeoff between model accuracy and computing costs. To ensure optimal sparse activation, we quantified the large errors of existing attribution metrics when used for sparse activation, due to the interdependency among attribution scores of different neurons, and further proposed a new attribution metric that can provably correct such errors. Experiments show that our technique can achieve up to 70% model sparsity in difficult generative tasks such as question answering and text summarization with <5% model accuracy loss. Such high model sparsity enables us to reduce the computing latency and memory use of LLM inference by 35% and 40%, respectively.


**中文摘要**:

长度感知预填充服务通过识别和分离LLM服务中不同提示长度的请求来降低TTFT延迟。虽然最近的系统已经解耦了预填充和解码阶段以提高吞吐量，但它们仍然依赖无法适应异构工作负载特征的统一调度策略。我们观察到提示长度的变化会导致不同的性能瓶颈，这促使我们设计一种自适应调度策略。LAPS将多轮长预填充请求与短预填充请求分离，并为短预填充工作负载引入长度感知的智能批处理机制。它采用双队列设计，支持在单个预填充实例上的时间分离或跨多个实例的空间分离。对于短预填充批次，批等待窗口和基于CUDA图的聚类减轻了异构计算的干扰，降低了批处理延迟和平均延迟。在真实的多轮工作负载中，LAPS在预填充-解码分离下相比原生SGLang将预填充延迟降低了超过30%，并在具有原生数据并行配置的多实例部署中进一步将SLO违规减少28%。与具有负载均衡的SGLang路由器相比，在多GPU设置中进一步将SLO违规降低了12%。在高并发和混合请求场景下，LAPS在服务Qwen2.5-32B模型时将预填充实例的请求吞吐量提高了35%，证明了其在优化异构LLM服务工作负载方面的有效性。


---


## [DriftBench: Measuring and Predicting Infrastructure Drift in LLM Serving Systems](https://mlsys.org/virtual/2026/poster/3576)


**英文摘要 (English Abstract)**:

AI applications increasingly depend on long-context inference, where LLMs consume substantial context to support stronger reasoning. Common examples include retrieval-augmented generation, agent memory layers, and multi-agent orchestration. As input contexts get longer, prefill latency becomes the main bottleneck. Yet today's prefill acceleration techniques face a trade-off: they either preserve reasoning quality but deliver little KV-cache reuse, or improve reuse at the cost of degraded reasoning quality. We present ContextPilot, a system that accelerates prefill by introducing context reuse as a new mechanism for faster long-context inference. ContextPilot introduces a context index to identify overlapping context blocks across LLM interactions (e.g., across users and turns). It further proposes context alignment and de-duplication techniques to maximize KV-cache reuse. To preserve reasoning quality under reuse, it introduces succinct context annotations that prevent quality degradation. Finally, ContextPilot is built around a modular architecture with a clean interface that integrates with existing inference engines. Extensive evaluation shows that ContextPilot reduces LLM prefill latency by up to 3X compared to state-of-the-art methods while preserving reasoning quality. At longer context lengths, it can even improve reasoning quality. ContextPilot is open-sourced at: https://github.com/EfficientContext/ContextPilot.


**中文摘要**:

生产级LLM部署缺乏系统的方法来评估基础设施变化对输出一致性的风险。基础设施漂移——硬件配置、软件版本和数据分布的渐进变化——会在不明显降低标准指标的情况下导致模型行为发生意外变化。我们提出DriftBench，一个用于测量和预测LLM服务系统中基础设施漂移的基准测试框架。它提供了一套标准化的漂移场景、检测指标和预测模型，使运维人员能够在漂移影响生产服务质量之前主动识别和缓解漂移。在两个大型生产集群上为期三个月的实验表明，DriftBench能够在中位数提前14天检测到显著的漂移事件。


---


## [PROMPTS: PeRformance Optimization via Multi-Agent Planning for LLM Training and Serving](https://mlsys.org/virtual/2026/poster/3620)


**英文摘要 (English Abstract)**:

We present TritorX, an agentic AI system designed to generate functionally correct Triton PyTorch ATen kernels at scale for emerging accelerator platforms. TritorX integrates large language models with a custom linter, JIT compilation, and a PyTorch OpInfo-based test harness. This pipeline is compatible with both real Meta Training and Inference Accelerator (MTIA) silicon and in hardware simulation environments for next-generation devices. In contrast to previous kernel-generation approaches that prioritize performance for a limited set of high-usage kernels, TritorX prioritizes coverage. Our system emphasizes correctness and generality across the entire operator set, including diverse data types, shapes, and argument patterns. In our experiments, TritorX successfully generated kernels and wrappers for 481 unique ATen operators that pass all corresponding PyTorch OpInfo tests (over 20,000 in total). TritorX paves the way for overnight generation of complete PyTorch ATen backends for new accelerator platforms.


**中文摘要**:

在大规模分布式系统上优化大语言模型的训练和服务是一个复杂的多目标问题。PROMPTS提出了一个通过多智能体规划来优化性能的框架，其中多个专门化智能体协作分析系统瓶颈并提出优化建议。该框架整合了训练和服务阶段的性能数据，通过智能体间的迭代规划持续改进系统配置，在吞吐量、延迟和资源利用率方面实现了全面的性能提升。


---


## [SD-HC: Heterogeneous Functional Pipelining for Speculative LLM Decoding on AI PCs](https://mlsys.org/virtual/2026/poster/10199)


**英文摘要 (English Abstract)**:

The Uniform Manifold Approximation and Projection (UMAP) algorithm has become a widely popular technique to reduce the dimensionality of a set of vectors, both for visualization and as a pre-processing step for follow-on machine learning tasks. UMAP is often an integral part of iterative and exploratory workflows, but the heavy amount of compute and memory required makes scaling to tens or even hundreds of gigabytes of vectors intractable on the CPU, often taking several hours to days to complete. In this paper, we show how we improved UMAP while unlocking performance that permits interactive analysis, even at massive-scale, by introducing an out-of-core strategy with optional multi-GPU support. We observe 22.7x speedup using a single GPU on smaller data scales where CPU baseline runs to completion, and project up to 74x speedup using multiple GPUs on a single node at larger scales where CPU was not able to complete by extrapolating measured scaling behavior.


**中文摘要**:

AI PC为在消费级硬件上运行LLM提供了新的可能性。SD-HC提出了一种异构功能流水线技术，用于在AI PC上进行推测性LLM解码。通过将推测解码的不同阶段分配到CPU、集成GPU和NPU上并行执行，SD-HC充分利用了AI PC中异构处理器的计算能力，实现了显著的LLM推理加速，使得本地运行大模型更加实用。


---


## [ContextPilot: Fast Long-Context Inference via Context Reuse](https://mlsys.org/virtual/2026/poster/3587)


**英文摘要 (English Abstract)**:

Automatic performance tuning (auto-tuning) is essential for optimizing high-performance applications, where vast and irregular search spaces make manual exploration infeasible. While auto-tuners traditionally rely on classical approaches such as evolutionary, annealing, or surrogate-based optimizers, designing algorithms that efficiently find near-optimal configurations robustly across diverse tasks is challenging. We propose a new paradigm: using large language models (LLMs) to automatically generate optimization algorithms tailored to auto-tuning problems. We introduce a framework that prompts LLMs with problem descriptions and search space characteristics to synthesize, test, and iteratively refine specialized optimizers. These generated algorithms are evaluated on four real-world auto-tuning applications across six hardware platforms and compared against the state-of-the-art in two contemporary auto-tuning frameworks. The evaluation demonstrates that providing additional application- and search space-specific information in the generation stage results in an average performance improvement of 30.7% and 14.6%, respectively. In addition, our results show that LLM-generated optimizers can rival, and in various cases outperform, existing human-designed algorithms, with our best-performing generated optimization algorithms achieving an average 72.4% improvement over state-of-the-art optimizers for auto-tuning.


**中文摘要**:

AI应用越来越依赖长上下文推理，其中LLM在请求间消耗大量的上下文token。ContextPilot观察到多个连续或重叠请求经常共享上下文前缀，通过智能缓存和复用这些共享前缀的KV缓存计算结果，大幅降低了重复计算开销。不同于简单的LRU缓存，ContextPilot使用上下文语义相似性来预测未来可能复用的前缀，并通过主动预热来减少缓存未命中，在批量处理长上下文请求时实现了显著的吞吐量提升和延迟降低。


---


## [Accelerating Large-Scale Reasoning Model Inference with Sparse Self-Speculative Decoding](https://mlsys.org/virtual/2026/poster/3510)


**英文摘要 (English Abstract)**:

Retrieval-augmented generation (RAG) extends large language models (LLMs) with external data sources to enhance factual correctness and domain coverage. Modern RAG pipelines rely on large datastores, creating a significant system challenge: achieving high throughput and low latency is difficult, especially when GPU memory is limited. To address these challenges, we propose TeleRAG, an efficient inference system that reduces latency and improves throughput with minimal GPU memory requirements. The core innovation of TeleRAG is lookahead retrieval, a prefetching mechanism that predicts required data and transfers them from CPU to GPU in parallel with LLM generation. In addition, TeleRAG adopts a prefetching scheduler and a cache-aware scheduler to support efficient multi-GPU inference with minimal overhead. Evaluations show TeleRAG achieves up to a 1.98× average end-to-end latency reduction (single-query) and 1.83× higher average throughput (batched), as well as good scalability in throughput. This confirms the practical utility of TeleRAG for faster and more memory-efficient deployments of RAG applications.


**中文摘要**:

大规模推理模型因其长推理链而产生高昂的计算成本。本文提出了一种利用稀疏自推测解码加速推理的方法。通过在自推测框架中引入稀疏性，跳过不重要的草稿token验证步骤，减少了计算冗余。该方法在不影响输出质量的情况下相比传统推测解码进一步降低了推理延迟，特别适用于具有长推理链的大模型。


---


## [Efficient, VRAM-Constrained xLM Inference on Clients](https://mlsys.org/virtual/2026/poster/3579)


**英文摘要 (English Abstract)**:

To usher in the next round of client AI innovation, there is an urgent need to enable efficient, lossless inference of high-accuracy large language models (LLMs) and vision language models (VLMs) on client systems. We present pipelined sharding, a novel, benchmark-profile-guided CPU-GPU hybrid scheduling technique. Using a combination of model sharding at the sub-layer level, CPU offloading, pipelined copy-compute, and prioritized tensor placement in VRAM, it optimizes both time-to-first-token and tokens per second metrics.


**中文摘要**:

上下文并行性已被广泛采用以支持基础模型预训练中不断增长的上下文长度。我们提出FCP，一个灵活的上下文并行范式，以块级粒度分片和调度序列。FCP不依赖环形等刚性通信拓扑，而是支持任意点对点通信，实现序列块在worker间的灵活放置。广泛评估显示FCP在最多256个NVIDIA GPU上实现近线性可扩展性。


---


## [Equinox: Decentralized Scheduling for Hardware-aware Satellite Intelligence](https://mlsys.org/virtual/2026/poster/10167)


**英文摘要 (English Abstract)**:

The growing demand for long-context inference capabilities in Large Language Models (LLMs) has intensified the computational and memory bottlenecks inherent to the self-attention mechanism. To address this challenge, we introduce BLASST, a drop-in, dynamic sparse attention mechanism that accelerates inference by using only a fixed scalar threshold to skip attention blocks. Our method targets practical inference deployment by removing the barriers to adoption present in existing works. As such, BLASST eliminates training requirements, avoids expensive pre-computation passes, accelerates both prefill and decode across all major attention variants (MHA, GQA, MQA, and MLA), provides optimized support for modern hardware, and easily integrates into existing frameworks. This is achieved by reusing online softmax statistics to identify negligible attention scores, skipping softmax, value block loads, and the subsequent matrix multiplication. We demonstrate the BLASST algorithm by delivering optimized kernels with negligible latency overhead. Our automated threshold calibration procedure reveals a simple inverse relationship between optimal threshold and context length, meaning we require only a single threshold each for prefill and decode per model. Preserving benchmark accuracy, we demonstrate a 1.52x speedup for prefill at 71.9% sparsity and a 1.48x speedup for decode at 73.2% sparsity on modern GPUs.


**中文摘要**:

卫星星座中的ML推理面临独特的调度挑战——每颗卫星的能源和通信带宽有限。Equinox提出了一个去中心化的硬件感知卫星智能调度系统，将ML推理任务调度转化为去中心化优化问题。每颗卫星根据本地观测和邻居信息自主决定计算任务的执行顺序，实现了星座级别的协作和负载均衡。


---


## [SuperInfer: SLO-Aware Rotary Scheduling and Memory Management for LLM Inference on Superchips](https://mlsys.org/virtual/2026/poster/3586)


**英文摘要 (English Abstract)**:

Large Language Model (LLM) serving faces a fundamental tension between stringent latency Service Level Objectives (SLOs) and limited GPU memory capacity. We present SuperInfer, a high-performance LLM inference system designed for emerging Superchips (e.g., NVIDIA GH200) with tightly coupled GPU-CPU architecture via NVLink-C2C. SuperInfer introduces RotaSched, the first proactive, SLO-aware rotary scheduler, and DuplexKV, an optimized rotation engine.


**中文摘要**:

随着LLM越来越多地部署在安全关键应用中，缺乏系统方法来评估其越狱攻击脆弱性构成了关键安全缺口。我们引入越狱预言机问题，并提出Boa——首个高效解决该问题的系统。Boa采用两阶段搜索策略，结合广度优先采样和由细粒度安全评分引导的深度优先搜索。


---


## [OPKV: A High-Throughput Plugin-Driven Framework for Recallable Sparsity in Paged KV Cache Systems](https://mlsys.org/virtual/2026/poster/3621)


**英文摘要 (English Abstract)**:

Maximizing performance on available GPU hardware is an ongoing challenge for modern AI inference systems. Traditional approaches include writing custom GPU kernels and using specialized model compilers to tune high-level code for specific GPU targets. Recent work shows that LLM-based multi-agent systems can effectively perform such tuning, often outperforming existing compilers and eliminating the need for manual kernel development. However, the dynamics of multi-agent systems for this task remain unexplored. In this work, we present a logical framework for comparing multi-agent PyTorch optimization systems. Our evaluation shows that exploit-heavy strategies perform best when paired with error-fixing agents, and that performance correlates with the granularity of optimization steps. The best implementation achieves an average 2.88× speedup over PyTorch Eager (1.85× over torch.compile) on an H100 GPU across diverse tasks in KernelBench, a benchmark suite covering a range of machine learning architectures in PyTorch. Code is publicly available at: https://github.com/pike-project/pike


**中文摘要**:

分页KV缓存系统在LLM服务中被广泛采用，但LRU驱逐策略可能过早驱逐未来需要的重要token。OPKV提出了一个高吞吐量的插件驱动框架，用于分页KV缓存系统中的可召回稀疏性管理。它提供了灵活的插件接口，允许用户自定义缓存驱逐和召回策略，通过智能地保留重要token的KV缓存并召回被驱逐的关键信息，在高吞吐量场景下保持了良好的模型质量。


---


## [BOute: Cost-Efficient LLM Serving with Heterogeneous LLMs and GPUs via Multi-Objective Bayesian Optimization](https://mlsys.org/virtual/2026/poster/3572)


**英文摘要 (English Abstract)**:

The rapid growth of large language model (LLM) deployments has made cost-efficient serving systems essential. We present BOute, a quality-aware scheduling system that jointly exploits heterogeneous model and GPU capabilities for cost-efficient LLM serving. BOute employs a multi-objective Bayesian optimization (MOBO) framework to co-optimize the routing strategy and model deployment. Evaluation results demonstrate that BOute outperforms state-of-the-art LLM serving systems by up to 157%.


**中文摘要**:

LLM部署的快速增长使成本高效的服务系统变得至关重要。我们提出BOute，一个联合利用异构模型和GPU能力实现成本高效LLM服务的质量感知调度系统。BOute采用多目标贝叶斯优化框架来协同优化路由策略和模型部署，在保证响应质量的条件下最大化服务系统的成本效率。评估结果显示BOute在相同成本预算和质量要求下相比最先进LLM服务系统平均提升59%、最高提升157%，或在保持相同性能目标的同时降低服务成本15%-61%。


---


## [Scaling Up Large Language Models Serving Systems for Semantic Job Search](https://mlsys.org/virtual/2026/poster/3522)


**英文摘要 (English Abstract)**:

The KV cache is a dominant memory bottleneck for LLM inference. While 4-bit KV quantization preserves accuracy, 2-bit often degrades it, especially on long-context reasoning. We close this gap via an algorithm–system co-design for mixed-precision KV caching: Kitty. On the algorithm side, extensive experiments show that Dynamic Channel-wise Precision Boost — which ranks Key-cache channels by sensitivity and keeps only a small fraction at higher precision — maintains near-zero drop in accuracy while approaching 2-bit memory. On the system side, the primary challenge lies in managing these dynamic 4-bit channel boosts without compromising memory efficiency or the execution speed of attention layers. Kitty addresses this through a hardware-aware memory layout and highly optimized system designs, ensuring that our on-the-fly KV quantization incurs negligible runtime overhead while maximizing memory footprint reduction. This synergistic design allows Kitty to unlock the full potential of 2-bit quantization without sacrificing real-time inference throughput. Specifically, Kitty addresses these issues by decomposing each mixed-precision Key page into two tensors with unified 2-bit precision. Based on this, Kitty provides a page-centric KV layout, Triton-compatible page dequantization kernels, and a lightweight runtime pipeline that reduces and amortizes the runtime overhead. Across seven tasks and two model families (Qwen3, LLaMA3), Kitty cuts KV memory by nearly 8× with negligible accuracy loss, enabling up to 8× larger batches and 2.1×–4.1× higher throughput under the same memory budget. We release the full implementation of Kitty at https://github.com/Summer-Summer/Kitty.


**中文摘要**:

语义职位搜索需要对大量职位描述和候选人资料进行高效的语义匹配。本文研究了将LLM服务系统扩展到语义职位搜索场景的挑战和解决方案。通过优化嵌入匹配和检索管道，系统能够在大规模职位数据和实时查询条件下保持低延迟响应，为基于AI的招聘平台提供了可扩展的技术方案。


---


## [Using Span Queries to Optimize Cache and Attention Locality](https://mlsys.org/virtual/2026/poster/3524)


**英文摘要 (English Abstract)**:

Despite the rapid adoption of large language models (LLMs) in mobile applications, deploying them efficiently on resource-constrained devices remains challenging due to limited compute, memory, and energy constraints. In this paper, we first evaluate the energy efficiency of state-of-the-art mobile LLM frameworks across multiple models and uncover a key inefficiency: the default governors make independent decisions which can result in 23.0–40.4% longer latency or 5.0–16.6% higher energy use compared to optimal frequency combinations. We then conduct an in-depth analysis to reveal the root cause–the lack of cross-resource coordination of these governors during prefilling and decoding. Building on these findings, we present CORE, a unified, energy-aware governor that jointly coordinates CPU, GPU, and memory frequencies for mobile LLM inference. Experiments across diverse LLMs show that CORE reduces time-to-first-token by 8.5-17.7% and time-per-token by 27.8-39.6% on average, without increasing energy per token.


**中文摘要**:

客户端正在从简单的聊天补全演变为包含推理时扩展和深度推理的多样化工作负载，但推理服务器仍主要为聊天补全优化。本文利用跨度查询来优化缓存和注意力局部性，将聊天、RAG、推理时扩展和智能体工作负载统一为跨度查询的通用结构——一种带有交换性约束的推理调用表达式树。通过自动优化查询表达式树来提高KV缓存局部性，在vLLM上仅修改492行代码实现了跨度查询的高性能执行。使用该技术栈，跨度查询在两个不同的非聊天用例中实现了10-20倍的TTFT降低，并可通过注意力优化避免中间丢失问题。


---


## [Practical Unstructured Sparsity for Efficient LLM Inference](https://mlsys.org/virtual/2026/poster/10185)


**英文摘要 (English Abstract)**:

Homomorphic Encryption (HE) offers a promising solution for privacy-preserving Graph Convolutional Network (GCN) inference in untrusted cloud environments by enabling computation directly on encrypted data. This capability is particularly valuable in domains such as recommendation systems, financial analysis, and bioinformatics, where data confidentiality is paramount. However, applying HE to large-scale GCN inference introduces substantial computational and memory overhead, severely limiting scalability and runtime efficiency. While prior works focusing on algorithmic improvements have demonstrated feasibility on CPUs, these approaches struggle to scale effectively on GPUs due to excessive memory consumption and redundant computation. In this work, we present G-HEMP, the first framework that leverages multi-GPU systems to accelerate large-scale private GCN inference. G-HEMP introduces two key innovations: (i) a block-diagonal parallel packing scheme that eliminates redundant data replication in encrypted adjacency matrices, reducing the number of HE operations and achieving up to 4.41× speedup over conventional feature-wise packing under single GPU environment; and (ii) a multi-GPU workload partitioning strategy that halves per-GPU peak memory usage on a 4-GPU system and achieves up to 3.88× latency improvement. Compared to the limb-level-partitioning-based approach in Cinnamon–the state-of-the-art encrypted computation parallelization method, G-HEMP further attains up to 3.13× gain owing to our superior multi-device partition policy. Overall, G-HEMP is model-agnostic and scales seamlessly with graph size and GPU count, enabling efficient and practical privacy-preserving GCN inference on modern heterogeneous environments.


**中文摘要**:

非结构化稀疏性在LLM推理中展现出巨大的加速潜力，但实际部署面临稀疏计算效率低下的挑战。本文提出了一种实用的非结构化稀疏方法用于高效LLM推理。通过细粒度的权重剪枝和专门的稀疏计算内核，在保持模型质量的前提下大幅减少了计算量，实现了显著的推理加速。


---


## [TeleRAG: Efficient Retrieval-Augmented Generation Inference with Lookahead Retrieval](https://mlsys.org/virtual/2026/poster/3573)


**英文摘要 (English Abstract)**:

Local execution of AI on edge devices is critical for privacy, low latency, and offline operation. However, deploying models on diverse hardware remains fragmented, often requiring model conversion or complete implementation outside the PyTorch ecosystem where the model was originally authored. We introduce ExecuTorch, a unified PyTorch-native deployment framework for edge AI. ExecuTorch enables seamless deployment of machine learning models across heterogeneous compute environments. It scales from completely embedded microcontrollers to complex system-on-chips (SoCs) with dedicated accelerators, powering devices ranging from wearables and smartphones to large compute clusters. ExecuTorch preserves PyTorch semantics while allowing customization, support for optimizations like quantization, and pluggable execution ''backends''. These features together enable fast experimentation, allowing researchers to validate deployment behavior entirely within PyTorch, bridging the gap between research and production.


**中文摘要**:

检索增强生成通过引入外部数据源来增强LLM的事实正确性和领域覆盖。现代RAG管道依赖大型数据存储，在GPU内存有限时实现高吞吐量和低延迟面临重大系统挑战。我们提出TeleRAG，一个通过前瞻检索来加速RAG推理的高效推理系统。其核心创新是一种预取机制，在LLM生成的同时预测并预取所需数据，将数据传输与生成过程重叠。TeleRAG还采用预取调度器和缓存感知调度器来支持高效的多GPU推理。评估表明TeleRAG实现了平均1.98倍的端到端延迟降低和1.83倍的平均吞吐量提升，并具有良好的吞吐量可扩展性，为更快和更节省内存的RAG应用部署提供了实用价值。


---


## [Communication-Efficient Distributed Inference for Transformer Models via Vector Quantized Context](https://mlsys.org/virtual/2026/poster/10180)


**英文摘要 (English Abstract)**:

Federated Learning (FL) enables collaborative training of Large Language Models (LLMs) across distributed data sources while preserving privacy. However, when federated LLMs are deployed in critical applications, it remains unclear which client(s) contributed to specific generated responses, hindering debugging, malicious client identification, fair reward allocation, and trust verification. We present ProToken, a novel Provenance methodology for Token-level attribution in federated LLMs that addresses client attribution during autoregressive text generation while maintaining FL privacy constraints. ProToken leverages two key insights to enable provenance at each token: (1) transformer architectures concentrate task-specific signals in later blocks, enabling strategic layer selection for computational tractability, and (2) gradient-based relevance weighting filters out irrelevant neural activations, focusing attribution on neurons that directly influence token generation. We evaluate ProToken across 16 configurations spanning four LLM architectures (Gemma, Llama, Qwen, SmolLM) and four domains (medical, financial, mathematical, coding). ProToken achieves 98.62% average attribution accuracy in correctly localizing responsible client(s), and maintains high accuracy when the number of clients are scaled, validating its practical viability for real-world deployment settings.


**中文摘要**:

Transformer模型的分布式推理中，跨节点传输KV缓存产生大量通信开销。本文提出了一种通过向量量化上下文实现通信高效分布式推理的方法。通过将KV缓存向量量化为紧凑表示后再进行跨节点传输，显著降低了分布式推理中的通信开销，同时保持了模型输出质量。


---


## [GhostServe: A Lightweight Checkpointing System in the Shadow for Fault-Tolerant LLM Serving](https://mlsys.org/virtual/2026/poster/3513)


**英文摘要 (English Abstract)**:

The rise of million-token, agent-based applications has placed unprecedented demands on large language model (LLM) inference services. We propose GhostServe, a novel checkpointing solution to facilitate fault-tolerant LLM serving. GhostServe protects the streaming KV cache in the shadow by applying erasure coding to generate and store the parity shards in host memory. Evaluations demonstrate that GhostServe reduces checkpointing latency by up to 2.7x and recovery latency by 2.1x.


**中文摘要**:

百万token级智能体应用对LLM推理服务提出了前所未有的需求。这些长时间运行的任务容易受到硬件和软件故障的影响，导致昂贵的作业失败和资源浪费。有状态的KV缓存随序列长度增长，是分布式服务系统中关键且脆弱的组件。我们提出GhostServe，一种新颖的检查点方案以促进容错LLM服务。GhostServe通过在后台对KV缓存应用纠删码生成并存储校验分片来保护流式KV缓存。在设备故障时，GhostServe能够快速重建丢失的KV缓存，使推理过程无缝恢复，无需昂贵的完全重计算或状态复制。评估表明，在系统故障情况下，GhostServe相比现有方法将检查点延迟降低高达2.7倍、恢复延迟降低2.1倍，并为单批次降低1.2倍中位响应延迟。


---


## [Beyond the Buzz: A Pragmatic Take on Inference Disaggregation](https://mlsys.org/virtual/2026/poster/3596)


**英文摘要 (English Abstract)**:

We study the Multi-Armed Bandit problem in nonstationary adversarial environments, where the identity of the optimal arm can change over time due to shifts in the loss sequence. Motivated by applications such as physical design tuning in database systems, we focus on settings with a very large number of arms and seek practical algorithms with sublinear runtime. Our main contribution is a novel algorithm, Queuing Behind the Leader (QBL), which achieves a per-iteration complexity of O(m log k), where m is the number of arms selected at each step. QBL combines limited update operations via a priority queue, a constant sampling overhead, and a balanced exploration strategy. We evaluate QBL extensively on state-of-the-art benchmarks and demonstrate that it consistently outperforms existing methods in both time and solution quality.


**中文摘要**:

随着推理扩展到多节点部署，预填充-解码分离——将推理分割为不同阶段——为改善吞吐量-交互性Pareto前沿提供了有前景的路径。尽管热情日益高涨且开源努力激增，由于优化搜索空间和系统级协调的复杂性，分离式服务的大规模部署仍然有限。本文首次对大规模分离式推理进行了系统研究，在多种工作负载和硬件配置下评估了数十万个设计点。我们发现分离式架构对预填充密集型流量模式和大模型最为有效。我们的结果强调了动态速率匹配和弹性伸缩在实现Pareto最优性能中的关键作用。


---


## [HiServe: A Prefix Cache Serving System for Hybrid LLMs](https://mlsys.org/virtual/2026/poster/10184)


**英文摘要 (English Abstract)**:

Large language models (LLMs) require vast amounts of GPU compute to train, but limited availability and high costs of GPUs make homogeneous clusters impractical for many organizations. Instead, assembling heterogeneous clusters by pooling together GPUs of different generations allows them to achieve higher aggregate compute and make use of all available GPUs. However, training on heterogeneous clusters presents significant challenges. The workload must be carefully partitioned such that GPUs in the cluster with limited compute, memory, or network bandwidth do not bottleneck the training process. Existing heterogeneous training systems cannot do so efficiently since they integrate data, pipeline, and tensor parallelism in a way that trades off communication for memory overhead. Combining vanilla data parallelism with pipeline parallelism is communication-efficient but results in high memory overhead from replicating model parameters. Alternatively, using sharded data parallelism or tensor parallelism reduces memory overhead but increases communication overhead when combined with pipeline parallelism. To address this problem, we designed Zorse, a system that uses Pipeline-Efficient ZeRO DP, a novel integration of pipeline parallelism and data parallelism that is both communication- and memory-efficient. Zorse uses a planner to automatically find an optimized training configuration from the vast search space of possibilities on heterogeneous clusters, and our evaluation shows that Zorse achieves up to 3× higher training throughput than state-of-the-art systems across representative heterogeneous training scenarios.


**中文摘要**:

混合部署不同大小和架构的LLM正变得越来越普遍。HiServe是一个面向混合LLM的前缀缓存服务系统，针对多模型混合部署场景智能管理共享前缀缓存。系统在保持各模型服务质量的条件下最大化缓存利用率和命中率，降低了多模型服务的总体基础设施成本。


---


## [TriInfer: Hybrid EPD Disaggregation for Efficient Multimodal Large Language Model Inference](https://mlsys.org/virtual/2026/poster/3533)


**英文摘要 (English Abstract)**:

Recent advances in 3D Gaussian Splatting (3DGS) have enabled high-quality and efficient novel view synthesis, demonstrating great potential in real-world applications such as robotic perception and digital-twin construction. However, 3DGS requires processing up to millions of Gaussians in parallel, imposing significant computational and memory demands that limit its deployment on resource-constrained platforms. Through systematic profiling and analysis, this paper identifies several redundancy at both the algorithmic and system implementation levels. These insights motivate us to explore several novel optimizations, including adaptive early sorting, GPU-efficient axis-shared rasterization, and dynamic thresholding. Unlike prior work that focuses only on either algorithmic improvements or systems optimization, our approach explores a joint algorithm and system co-optimization to push the performance limits of 3DGS on GPUs. Comprehensive evaluation demonstrates that our co-optimization approach, named Flash3DGS achieves a speed-up of up to 1.41× with negligible algorithmic performance drop in rendering image quality compared with the gsplat baseline. Importantly, our co-optimization is orthogonal to most existing 3DGS acceleration methods, allowing for synergistic performance gains when used in combination. We plan to release our code publicly upon paper acceptance to support reproducibility and future research.


**中文摘要**:

多模态LLM的推理涉及编码器、预填充和解码等多个阶段，各阶段的计算特征和资源需求差异显著。TriInfer提出了一种混合EPD分离架构，通过将编码器、预填充和解码阶段灵活分配给不同的硬件资源来最大化资源利用率。该方法在多模态工作负载上实现了显著的吞吐量提升和延迟降低。


---


## [HELIOS : Adaptive Model And Early-Exit Selection for Efficient LLM Inference Serving](https://mlsys.org/virtual/2026/poster/3623)


**英文摘要 (English Abstract)**:

Quantization has emerged as a standard technique for accelerating inference for generative models by enabling faster low-precision computations and reduced memory transfers. Recently, GPU accelerators have added first-class support for microscaling Block Floating Point (BFP) formats. Standard BFP algorithms use a fixed scale based on the maximum magnitude of the block. We observe that this scale choice can be suboptimal with respect to quantization errors. In this work, we propose ScaleSearch, an alternative strategy for selecting these scale factors: using a fine-grained search leveraging the mantissa bits in microscaling formats to minimize the quantization error for the given distribution. ScaleSearch can be integrated with existing quantization methods such as Post Training Quantization and low precision attention, and is shown to improve their performance. Additionally, we introduce ScaleSearchAttention, an accelerated NVFP4-based attention algorithm, which uses ScaleSearch and adapted prior techniques to ensure near-0 performance loss for causal language modeling. Experiments show that ScaleSearch reduces quantization error by 27% for NVFP4 and improves language model PTQ by up to 15 points for MATH500 (Qwen3-8B), while ScaleSearchAttention improves Wikitext-2 PPL by up to 0.77 points for Llama 3.1 70B. The proposed methods closely match baseline performance while providing quantization accuracy improvements.


**中文摘要**:

不同查询对LLM推理深度的需求差异很大——简单查询可能在前几层就能得到满意的答案。HELIOS提出了一种自适应模型和早退选择方法，根据查询难度动态决定使用完整模型还是早期层输出。通过在每个潜在退出点评估置信度，简单查询可以提前退出以减少延迟和计算开销，复杂查询则使用完整模型保证质量，实现了延迟和质量的灵活平衡。


---


## [CDLM: Consistency Diffusion Language Models for Faster Sampling](https://mlsys.org/virtual/2026/poster/3562)


**英文摘要 (English Abstract)**:

Diffusion Language Models (DLMs) offer a promising parallel generation paradigm but suffer from slow inference due to numerous refinement steps and the inability to use standard KV caching. We introduce CDLM (Consistency Diffusion Language Models), a training-based acceleration method that simultaneously tackles both bottlenecks. Experiments show CDLM achieves 3.6x-14.5x lower latency while maintaining competitive accuracy on math and coding tasks.


**中文摘要**:

扩散语言模型提供了有前景的并行生成范式，但因大量细化步骤和无法使用标准KV缓存而导致推理缓慢。我们引入CDLM，一种基于训练的加速方法，通过集成一致性建模大幅减少所需采样步数并实现多token最终化，同时解决两个瓶颈。此外，我们在微调期间强制使用块状因果注意力掩码，使模型完全兼容KV缓存。实验显示CDLM实现3.6-14.5倍更低延迟，同时在数学和编程任务上保持竞争准确率。代码见 https://github.com/SqueezeAILab/CDLM。


---


## [BLAZE: Bias-Driven Load-Aware Zero-Overhead Expert Routing](https://mlsys.org/virtual/2026/poster/10166)


**英文摘要 (English Abstract)**:

Large reasoning models (LRMs) often incur significant key-value (KV) cache overhead, due to their linear growth with the verbose chain-of-thought (CoT) reasoning. This incurs both memory overhead and throughput bottlenecks, limiting efficient deployment. To reduce KV cache size during inference, we first investigate the effectiveness of existing KV cache eviction methods for CoT reasoning. Interestingly, we find that due to unstable token-wise scoring and reduced effective KV budget caused by padding, state-of-the-art (SoTA) eviction methods fail to maintain accuracy in multi-batch settings. Additionally, these methods often generate longer sequences than the original model without eviction, as semantic-unaware token-wise eviction leads to repeated revalidation during reasoning. To address these issues, we present SkipKV, a training-free KV compression method that performs selective eviction and generation, operating at a coarse-grained, sentence-level sequence removal for efficient CoT reasoning. In specific, it introduces a sentence-scoring metric to identify and remove highly similar sentences while maintaining semantic coherence. To suppress redundant generation, SkipKV dynamically adjusts a steering vector to update the hidden activation states during inference, enforcing the LRM to generate concise responses. Extensive evaluations on multiple reasoning benchmarks demonstrate that SkipKV achieves up to 26.7% higher accuracy compared to baseline methods, at a similar compression budget. Additionally, compared to SoTA, SkipKV yields up to 1.6× shorter generation length while improving throughput by up to 1.7×. Our code is released at: https://github.com/TTTTTTris/SkipKV.


**中文摘要**:

MoE模型中专家负载不均衡会导致计算资源浪费。BLAZE提出了一种偏置驱动的负载感知零开销专家路由方法。通过分析并利用专家选择中已有的内在偏置来优化路由决策，在不引入额外计算开销的情况下实现更均衡的专家负载分布，提高了MoE推理的硬件利用率和整体吞吐量。


---


## [Flexo: A User-Controllable Distributed Training System](https://mlsys.org/virtual/2026/poster/10198)


**英文摘要 (English Abstract)**:

Tensor parallelism (TP) enables large language models (LLMs) to scale inference efficiently across multiple GPUs, but its tight coupling makes systems fragile: a single GPU failure can halt execution, trigger costly KVCache recomputation, and introduce long-term compute and memory imbalance. We present RaidServe, a fault-tolerant TP serving system that sustains high performance under irregular GPU availability. RaidServe introduces three techniques to balance computation and memory across GPUs: (1) Cyclic KVCache Placement for even memory utilization, (2) Hybrid Attention combining tensor- and data-parallel attention to eliminate stragglers, and (3) Fine-Grained Load-Aware Routing to dynamically balance requests. It further employs proactive KVCache backup and on-demand weight recovery to avoid expensive recomputation and redundant data transfers. Implemented in a lightweight serving engine compatible with existing infrastructures, RaidServe achieves up to 2× higher throughput and two orders of magnitude faster recovery than standard fault-handling methods on an 8×H100 DGX system, maintaining strong performance even with multiple GPU failures.


**中文摘要**:

分布式训练系统通常采用固定的并行化策略，难以适应多变的工作负载和资源条件。Flexo是一个用户可控的分布式训练系统，提供直观的接口让用户根据需求自定义并行化策略、通信模式和资源分配。系统自动处理底层优化，实现了灵活性和高性能的兼顾。


---


## [Hippocampus: An Efficient and Scalable Memory Module for Agentic AI](https://mlsys.org/virtual/2026/poster/3640)


**英文摘要 (English Abstract)**:

Attention, as a core layer of the ubiquitous Transformer architecture, is the bottleneck for large language models and long-context applications. While optimized attention for Hopper GPUs through asynchronous execution and warp specialization, it primarily targets the H100 architecture. The AI industry has rapidly transitioned to deploying Blackwell-based systems such as the B200 and GB200, which exhibit fundamentally different performance characteristics due to asymmetric hardware scaling: tensor core throughput doubles while other functional units (shared memory bandwidth, exponential units) scale more slowly or remain unchanged. We develop several techniques to address these shifting bottlenecks on Blackwell GPUs: (1) redesigned pipelines that exploit fully asynchronous MMA operations and larger tile sizes, (2) software-emulated exponential and conditional softmax rescaling that reduces non-matmul operations, and (3) leveraging tensor memory and the 2-CTA MMA mode to reduce shared memory traffic and atomic adds in the backward pass. We demonstrate that our method, FlashAttention-4, achieves up to 1.3× speedup over cuDNN 9.13 and 2.7× over Triton on B200 GPUs with BF16, reaching up to 1613 TFLOPs/s (71% utilization). Beyond algorithmic innovations, we implement FlashAttention-4 entirely in CuTe-DSL embedded in Python, achieving 20-30× faster compile times compared to traditional C++ template-based approaches while maintaining full expressivity.


**中文摘要**:

智能体AI需要高效的记忆管理来跨会话保持知识和上下文。Hippocampus提出了一种高效可扩展的智能体AI内存模块，为智能体系统提供结构化的记忆管理。它支持长期信息存储、高效检索和智能遗忘，使智能体能够在复杂多步任务中保持更好的连贯性和适应性。


---


## [From Tokens to Layers: Redefining Stall-Free Scheduling for MoE Serving with Layered Prefill](https://mlsys.org/virtual/2026/poster/3509)


**英文摘要 (English Abstract)**:

Large Language Model (LLM) inference in production must meet stringent service-level objectives for both time-to-first-token (TTFT) and time-between-token (TBT) while maximizing throughput. We propose layered prefill, a new scheduling paradigm that treats transformer layer groups as the primary scheduling unit, specifically targeting MoE serving. Layered prefill reduces off-chip bandwidth demand, lowering TTFT by up to 70%, end-to-end latency by 41% and per-token energy by up to 22%.


**中文摘要**:

生产中LLM推理必须满足严格的首token时间和每token时间服务级别目标，同时在固定资源预算下最大化吞吐量。现代服务系统采用如分块预填充的无停顿调度技术，但这类技术在MoE模型中引入显著开销——冗余的专家权重加载将内存流量增加高达39%。我们提出分层预填充，一种将Transformer层组作为主要调度单元并专门针对MoE服务的新调度范式。通过垂直分区模型为连续层组并在组间交错预填充和解码，分层预填充在维持无停顿解码的同时消除了分块引起的MoE权重重载。它降低了片外带宽需求，将TTFT降低高达70%、端到端延迟降低41%、每token能耗降低高达22%。评估表明分层预填充始终改进了TTFT-TBT Pareto前沿，同时维持无停顿解码。


---


## [MorphServe: Efficient and Workload-Aware LLM Serving via Runtime Quantized Layer Swapping and KV Cache Resizing](https://mlsys.org/virtual/2026/poster/3593)


**英文摘要 (English Abstract)**:

Mixture-of-Experts (MoEs) enable massive model sizes but incur higher serving overheads than dense models at the same per-token compute cost. This MoE tax varies with the model architecture, inference phase, and parallelism strategy. We comprehensively study the tax for different MoE models, finding that they perform 2–3× worse than FLOP-equivalent dense models. Using microbenchmarks, we analyze and categorize the underlying tax sources and show how they manifest differently under different configurations. Our key result is that prefill and decode phases incur vastly different taxes; counterintuitively, load imbalance across experts that harms prefill performance can benefit decode by activating fewer experts. We decompose the tax into analytically separable components and propose a balls-bins-buckets framework to study recent MoE developments like fine-grained experts and data parallel attention. We conclude by discussing existing and new techniques to reduce the MoE tax and their associated trade-offs.


**中文摘要**:

不同工作负载对LLM精度和延迟有不同要求。MorphServe通过运行时量化层交换和KV缓存调整来实现高效且工作负载感知的LLM服务。系统根据实时负载特征动态调整量化精度和缓存大小，在高负载时降低精度以保证吞吐量，在低负载时恢复精度以提升质量，实现了自适应的工作负载优化。


---


## [Kitty: Accurate and Efficient 2-bit KV Cache Quantization with Dynamic Channel-wise Precision Boost](https://mlsys.org/virtual/2026/poster/3523)


**英文摘要 (English Abstract)**:

The proliferation of large language models (LLMs) demands inference systems with both low latency and high efficiency at scale. GPU-based serving relies on HBM for model weights and KV caches, creating a memory bandwidth bottleneck during decode. To break through this bottleneck, we present the first large-scale, SRAM-based LLM inference deployment—Groq's public cloud—serving hundreds of billions of tokens daily. This paper reviews Groq's first-generation SRAM-based Huge Inference Pipelines (SHIP), highlighting: (1) a synchronous, low-diameter interconnect enabling low-latency scaling across thousands of chips; (2) optimizations for LLM serving under limited memory capacity; and (3) a large pipeline design that sustains efficiency and latency under varying prefill-to-decode ratios and context lengths. Together, these yield state-of-the-art latency while maintaining efficiency across diverse traffic scenarios—key to real-world LLM serving.


**中文摘要**:

KV缓存量化是减少LLM服务内存占用的有效方法，但低位量化可能显著降低模型质量。Kitty提出了一种准确高效的2位KV缓存量化方法，采用动态通道级精度提升技术。通过在运行时识别重要通道并为其分配更高精度，Kitty在不显著增加内存开销的情况下大幅降低了KV缓存的量化误差，实现了与全精度缓存相当的模型质量。


---


## [When Machine Learning Isn't Sure: Building Resilient ML-Based Computer Systems by Embracing Uncertainty](https://mlsys.org/virtual/2026/poster/3549)


**英文摘要 (English Abstract)**:

Large Language Model (LLM) serving is rapidly becoming one of the most power-intensive workloads in modern datacenters. Unlike training, where throughput dominates, inference must satisfy strict per-request latency targets such as Time-to-First-Token (TTFT) and Time-Between-Tokens (TBT). Once an SLO is met, the remaining latency slack between the earliest possible completion and the deadline offers an opportunity for energy savings. Existing systems, however, exploit only one dimension of this trade-off: batching improves resource efficiency, while DVFS improves power efficiency. These two axes are tightly coupled, and optimizing one while fixing the other yields only a local optimum. We present BEAM, a fine-grained controller that dynamically co-optimizes resource and power efficiency under per-request SLOs. BEAM continuously allocates the available latency slack across both dimensions by jointly tuning GPU frequency, chunk size, and microbatch count in real time. Its event-driven design responds instantly to request arrivals and completions, while a lightweight predictive model enables sub-millisecond decision making with negligible overhead. Implemented atop the vLLM runtime, BEAM reduces end-to-end GPU energy consumption by up to 51% compared to vLLM.


**中文摘要**:

基于ML的系统在面临不确定性输入时可能做出错误决策。本文探讨了基于ML的计算机系统中不确定性处理的核心问题——当ML模型不再确定时，系统如何保持可靠性？论文提出了一个拥抱不确定性的框架，通过量化置信度、维护备选方案和设计安全回退机制来构建更加鲁棒的ML驱动系统。


---


## [PRISM: Parametrically Refactor Inference for Speculative Decoding Draft Models](https://mlsys.org/virtual/2026/poster/3566)


**英文摘要 (English Abstract)**:

Large Language Models (LLMs), constrained by their auto-regressive nature, suffer from slow decoding. Speculative decoding methods have emerged as a promising solution to accelerate LLM decoding, attracting attention from both systems and AI research communities. Recently, the pursuit of better draft quality has driven a trend toward parametrically larger draft models, which inevitably introduces substantial computational overhead. While existing work attempts to balance the trade-off between prediction accuracy and compute latency, we address this fundamental dilemma through architectural innovation. We propose PRISM, which disaggregates the computation of each predictive step across different parameter sets, refactoring the computational pathways of draft models to successfully decouple model capacity from inference cost. Through extensive experiments, we demonstrate that PRISM outperforms all existing draft architectures, achieving exceptional acceptance lengths while maintaining minimal draft latency for superior end-to-end speedup. We also re-examine scaling laws with PRISM, revealing that PRISM scales more effectively with expanding data volumes than other draft architectures. Through rigorous and fair comparison, we show that PRISM boosts the decoding throughput of an already highly optimized inference engine by more than 2.6×.


**中文摘要**:

推测解码中草稿模型的计算开销往往抵消了其加速效益。PRISM通过参数化重构来优化推测解码的草稿模型推理。通过识别草稿模型中可在推测过程中共享或简化的参数并进行重构，减少了草稿模型的计算开销，使推测解码的整体效率得到显著提升。


---


## [GriNNder: Breaking the Memory Capacity Wall in Full-Graph GNN Training with Storage Offloading](https://mlsys.org/virtual/2026/poster/3628)


**英文摘要 (English Abstract)**:

Full-graph training of graph neural networks (GNNs) is widely used as it enables direct validation of algorithmic improvements by preserving complete neighborhood information. We introduce GriNNder, which is the first work to leverage storage devices to enable full-graph training even with limited memory. GriNNder achieves up to 9.78x speedup over state-of-the-art baselines and throughput comparable to distributed systems.


**中文摘要**:

全图GNN训练因保留完整邻域信息而被广泛使用，但通常需要多个GPU或服务器。我们引入GriNNder，首个利用存储设备在有限内存下实现全图训练的工作。GriNNder通过结构化存储卸载框架管理GPU-主机-存储层次结构，实现高达9.78倍的加速和与分布式系统相当的吞吐量，使此前不可行的大规模全图训练在单个GPU上成为可能。


---


## [SpecDiff-2: Scaling Diffusion Drafter Alignment For Faster Speculative Decoding](https://mlsys.org/virtual/2026/poster/3532)


**英文摘要 (English Abstract)**:

Speculative decoding has become the standard approach for accelerating Large Language Model (LLM) inference. It exploits a lossless draft-then-verify procedure to circumvent the latency of autoregressive decoding, achieving impressive speed-ups. Yet, current speculative decoding approaches remain limited by two fundamental bottlenecks: (1) the autoregressive dependency during drafting which limits parallelism, and (2) frequent rejections of draft tokens caused by misalignment between the draft and verify models. This paper proposes SpecDiff-2, a novel framework to jointly address these two bottlenecks. It leverages discrete diffusion as a non-autoregressive drafter to address bottleneck (1) and develops novel techniques to calibrate discrete diffusion drafters with autoregressive verifiers, addressing bottleneck (2). Experimental results across a comprehensive benchmark suite show that SpecDiff-2 achieves a new state-of-the-art across reasoning, coding, and mathematical benchmarks, improving tokens-per-second by up to an average of +55% over previous baselines and obtaining up to 5.5× average speed-up over standard decoding, without any loss of accuracy.


**中文摘要**:

扩散模型作为推测解码的草稿生成器具有并行生成的优势。SpecDiff-2通过扩展扩散草稿模型的对齐训练来加速推测解码。通过改进的对齐训练使扩散草稿更好地匹配目标模型的分布，提高了草稿token的接受率，实现了更高效的推测解码。


---


## [CRAFT: Fine-Grained Cost-Aware Expert Replication For Efficient Mixture-of-Experts Serving](https://mlsys.org/virtual/2026/poster/3508)


**英文摘要 (English Abstract)**:

Mixture-of-Experts (MoE) has recently emerged as the mainstream architecture for efficiently scaling large language models while maintaining near-constant computational cost. We present CRAFT, an efficient expert replication framework that maximizes load balance under a given memory budget by performing fine-grained, per-layer replication based on the estimated replication benefit. CRAFT increases end-to-end serving throughput by 1.14x on average over existing replication techniques.


**中文摘要**:

MoE已成为在保持近恒定计算成本的同时高效扩展LLM的主流架构。专家并行通过跨设备分区专家来分配参数，但在推理期间引入token级负载不均衡。专家复制是服务框架中广泛采用的负载均衡技术。我们证明现有复制方案常常过度复制，许多副本仅提供边际改进。我们提出CRAFT，一个在给定内存预算下通过基于估计复制收益的细粒度逐层复制最大化负载均衡的高效专家复制框架。CRAFT可无缝集成到现有服务框架中，无需额外训练或模型更改。评估表明CRAFT相比现有复制技术在端到端服务吞吐量上平均提高1.14倍。


---


## [TokenWeave: Efficient Compute-Communication Overlap for Distributed LLM Inference](https://mlsys.org/virtual/2026/poster/3521)


**英文摘要 (English Abstract)**:

Distributed inference of large language models (LLMs) using tensor parallelism can introduce communication overheads of 20% even over GPUs connected via NVLink. We present TokenWeave, the first system to enable efficient compute-communication overlap for tensor-parallel model inference for token lengths as small as 1024. Our evaluations demonstrate up to 1.28x speedup in latency and up to 1.19x higher throughput across multiple models and workloads.


**中文摘要**:

使用张量并行的LLM分布式推理即使在NVLink连接的GPU上也会引入20%的通信开销。我们提出TokenWeave，首个在token长度小至1024时也能实现张量并行模型推理中高效计算-通信重叠的系统。TokenWeave将RMSNorm识别为关键操作，并通过实现新颖的融合AllReduce-RMSNorm内核优化它和通信。该内核利用现代GPU的NVSHARP/Multimem特性，仅使用2-8个流式多处理器高效联合执行通信和RMSNorm。评估显示延迟加速高达1.28倍、吞吐量提升高达1.19倍。代码见 https://github.com/microsoft/tokenweave。


---


## [Speculative Decoding: Performance or Illusion?](https://mlsys.org/virtual/2026/poster/3559)


**英文摘要 (English Abstract)**:

Speculative decoding (SD) has become a popular technique to accelerate Large Language Model (LLM) inference, yet its real-world effectiveness remains unclear as prior evaluations rely on research prototypes and unrealistically small batch sizes. We present, to our knowledge, the first systematic study of SD on a production-grade and widely deployed inference engine (vLLM), covering multiple SD variants (n-gram, EAGLE/EAGLE-3, Draft-Model, Multi-Token Prediction) across diverse workloads, model scales, and batch sizes. We analyze key factors governing SD performance, and quantify a theoretical upper bound on SD speedup. Our results show that verification by the target model dominates the execution, while acceptance length varies markedly across output token positions, requests, and datasets. Comparing measured performance with theoretical bounds reveals substantial gaps between observed and theoretical upper bounds, and we leverage this observation to highlight new research opportunities that our study opens up in improving SD.


**中文摘要**:

推测解码被广泛宣传为LLM推理加速的有效方法，但实际部署中的收益可能远低于理论预期。本文深入分析了推测解码在各种模型、硬件和工作负载下的实际性能。通过大量实验揭示了推测解码在真实部署中的性能瓶颈，包括草稿质量、验证开销和批处理效应，为实践者选择推测解码策略提供了基于实证的指导。


---


## [Breaking the Ice: Analyzing Cold Start Latency in vLLM](https://mlsys.org/virtual/2026/poster/3561)


**英文摘要 (English Abstract)**:

As scalable inference services become popular, the cold start latency of an inference engine becomes important. Today, vLLM has evolved into the de-facto inference engine of choice for many inference workloads. Although popular, due to its complexity and rapid evolution, there has not been a systematic study on the startup latency of its engine. With major architectural innovations under it (e.g., the V1 API, introduction of torch.compile), in this paper, we present the first detailed performance characterization of vLLM startup latency. We break down the startup process into six foundational steps and demonstrate that this process is predominantly CPU-bound. Each step exhibits consistent and interpretable scaling trends with respect to model- and system-level parameters, enabling fine-grained attribution of latency sources. Building on these insights, we develop a lightweight analytical model that accurately predicts vLLM's startup latency for a given hardware configuration, providing actionable guidance for resource planning in large-scale inference environments. All our benchmarking datasets, analysis tools, and prediction scripts are open-sourced at: https://github.com/upb-cn/vllm-startup-profiler


**中文摘要**:

vLLM是广泛使用的LLM推理引擎，但其冷启动延迟——从接收到首个请求到开始生成token的时间——可能长达数十秒。本文通过系统剖析识别了vLLM冷启动的关键瓶颈，包括模型权重加载、CUDA内核编译和KV缓存初始化。提出了一系列优化措施来减少vLLM在生产环境中首次服务请求的响应时间。


---


## [Rethinking DVFS for Mobile LLMs: Unified Energy-Aware Scheduling with CORE](https://mlsys.org/virtual/2026/poster/3591)


**英文摘要 (English Abstract)**:

Despite the rapid adoption of large language models (LLMs) in mobile applications, deploying them efficiently on resource-constrained devices remains challenging due to limited compute, memory, and energy constraints. In this paper, we first evaluate the energy efficiency of state-of-the-art mobile LLM frameworks across multiple models and uncover a key inefficiency: the default governors make independent decisions which can result in 23.0–40.4% longer latency or 5.0–16.6% higher energy use compared to optimal frequency combinations. We then conduct an in-depth analysis to reveal the root cause–the lack of cross-resource coordination of these governors during prefilling and decoding. Building on these findings, we present CORE, a unified, energy-aware governor that jointly coordinates CPU, GPU, and memory frequencies for mobile LLM inference. Experiments across diverse LLMs show that CORE reduces time-to-first-token by 8.5-17.7% and time-per-token by 27.8-39.6% on average, without increasing energy per token.


**中文摘要**:

移动端LLM推理的能耗效率受限于DVFS调速器缺乏协调。本文评估了最先进移动LLM框架的能耗效率，揭示了默认调速器的独立决策可导致相比最优频率组合增加23-40%的延迟或5-17%的能耗。我们提出CORE，一个统一协调CPU、GPU和内存频率的能耗感知调速器。实验表明CORE在不增加每token能耗的情况下将首token时间平均降低8.5-17.7%，每token时间降低27.8-39.6%。


---


## [Zorse: Optimizing LLM Training Efficiency on Heterogeneous GPU Clusters](https://mlsys.org/virtual/2026/poster/3636)


**英文摘要 (English Abstract)**:

Serverless computing is an attractive paradigm for cloud-based large language model (LLM) inference, but scaling LLMs on demand remains a major challenge due to high data transfer cost. We present FaaScale, a serverless LLM system that enables fast and resource-efficient model scaling. The key idea is a co-design principle—pipelined multicast inference—which synergizes multicast with dynamic, cross-node pipeline-parallel execution during model transfer. FaaScale implements this design through PipeCast, a model scaling scheme that adaptively multicasts model blocks and dynamically forms inference pipelines on the fly. Coupled with efficient memory management across GPU and host memory, FaaScale handles bursty LLM inference workloads effectively, achieving up to 5× lower tail time-to-first-token latency and 31.3% cost reduction on real-world LLM traces.


**中文摘要**:

异构GPU集群中不同GPU的计算能力差异给分布式LLM训练带来了挑战。Zorse是一个在异构GPU集群上优化LLM训练效率的系统，通过智能地将不同计算任务分配到最适合的GPU类型上并结合动态负载均衡和通信优化，在混合GPU环境中实现了显著更高的成本效益。


---


## [EarthSight: A Distributed Framework for Low-Latency Satellite Intelligence](https://mlsys.org/virtual/2026/poster/3569)


**英文摘要 (English Abstract)**:

Low-latency delivery of satellite imagery is essential for time-critical applications. We present EarthSight, a distributed runtime framework that redefines satellite image intelligence as a distributed decision problem between orbit and ground. EarthSight introduces multi-task inference on satellites using shared backbones, a ground-station query scheduler, and dynamic filter ordering. Evaluations show EarthSight reduces average compute time per image by 1.9x.


**中文摘要**:

卫星图像的低延迟交付对灾害响应等时间关键应用至关重要。传统管道依赖在分析之前将所有图像下传，因有限通信带宽导致数小时到数天的延迟。我们提出EarthSight，一个将卫星图像智能重新定义为轨道与地面之间分布式决策问题的分布式运行时框架。EarthSight引入三项创新：使用共享骨干的卫星多任务推理、聚合用户请求并分配计算预算的地面站查询调度器、以及集成模型选择性、准确率和执行成本的动态过滤排序。评估显示EarthSight将每张图像平均计算时间减少1.9倍，将第90百分位端到端延迟从51分钟降至21分钟。


---


## [Toward a Small ML Runtime Stack for Raspberry Pi 5 QPUs](https://mlsys.org/virtual/2026/poster/10181)


**英文摘要 (English Abstract)**:

Mixture-of-Experts (MoEs) enable massive model sizes but incur higher serving overheads than dense models at the same per-token compute cost. This MoE tax varies with the model architecture, inference phase, and parallelism strategy. We comprehensively study the tax for different MoE models, finding that they perform 2–3× worse than FLOP-equivalent dense models. Using microbenchmarks, we analyze and categorize the underlying tax sources and show how they manifest differently under different configurations. Our key result is that prefill and decode phases incur vastly different taxes; counterintuitively, load imbalance across experts that harms prefill performance can benefit decode by activating fewer experts. We decompose the tax into analytically separable components and propose a balls-bins-buckets framework to study recent MoE developments like fine-grained experts and data parallel attention. We conclude by discussing existing and new techniques to reduce the MoE tax and their associated trade-offs.


**中文摘要**: [待翻译]


---


## [Kascade: A Practical Sparse Attention Method for Long-Context LLM Inference](https://mlsys.org/virtual/2026/poster/10170)


**英文摘要 (English Abstract)**:

The proliferation of large language models (LLMs) demands inference systems with both low latency and high efficiency at scale. GPU-based serving relies on HBM for model weights and KV caches, creating a memory bandwidth bottleneck during decode. To break through this bottleneck, we present the first large-scale, SRAM-based LLM inference deployment—Groq's public cloud—serving hundreds of billions of tokens daily. This paper reviews Groq's first-generation SRAM-based Huge Inference Pipelines (SHIP), highlighting: (1) a synchronous, low-diameter interconnect enabling low-latency scaling across thousands of chips; (2) optimizations for LLM serving under limited memory capacity; and (3) a large pipeline design that sustains efficiency and latency under varying prefill-to-decode ratios and context lengths. Together, these yield state-of-the-art latency while maintaining efficiency across diverse traffic scenarios—key to real-world LLM serving.


**中文摘要**:

长上下文LLM推理的注意力计算开销随序列长度二次增长。Kascade是一种实用的稀疏注意力方法，通过分阶段过滤机制逐步减少需要计算的token对数量。首先快速排除明显不相关的token，然后对剩余候选项进行更精确的注意力计算，在保持模型质量的同时显著降低了长上下文推理的计算和内存开销。


---


## [Pylo: Towards Accessible Learned Optimizers in PyTorch](https://mlsys.org/virtual/2026/poster/3601)


**英文摘要 (English Abstract)**:

Learned optimizers have been an active research topic over the past decade, with increasing progress toward practical, general-purpose optimizers that can serve as drop-in replacements for widely used methods like Adam. However, recent advances such as VeLO, which was meta-trained for 4000 TPU-months, remain largely inaccessible to the broader community, in part due to their reliance on JAX and the absence of user-friendly packages for independently using the optimizers after meta-training. To address this gap, we introduce PyLO, a PyTorch-based library that brings learned optimizers to the remaining approximately 70% of machine learning community via the familiar torch.optim.Optimizer interface. Unlike prior work focused on limited-scale academic tasks, our emphasis is on applying learned optimization to real-world large-scale pre-training tasks. Our systems contribution includes CUDA-accelerated implementations of the small fc_lopt and VeLO learned optimizers, achieving substantial performance gains, with training throughput on ViT-B/16 (batch size 32) increasing from 39.36 and 49.73 to 205.59 and 191.18 samples per second, respectively. PyLO has the versatility that allows us to easily combine learned optimizers with existing optimization tools such as learning rate schedules and weight decay. When doing so, we discover that learned optimizers can substantially benefit from it. Our code is available at https://github.com/Belilovsky-Lab/pylo


**中文摘要**:

学习型优化器在过去十年中取得了显著进展，但VeLO等最新进展经过4000 TPU月的元训练仍因依赖JAX和缺乏用户友好包而难以被更广泛社区使用。我们引入PyLO，一个基于PyTorch的库，通过熟悉的torch.optim.Optimizer接口将学习型优化器带给约70%的机器学习社区。系统贡献包括CUDA加速实现，ViT-B/16训练吞吐量从39.36和49.73提高到205.59和191.18样本/秒。PyLO的通用性允许将学习型优化器与学习率调度和权重衰减等现有工具轻松结合。代码见 https://github.com/Belilovsky-Lab/pylo。


---


## [BatchLLM: Optimizing Large Batched LLM Inference with Global Prefix Sharing and Throughput-oriented Token Batching](https://mlsys.org/virtual/2026/poster/3610)


**英文摘要 (English Abstract)**:

Large language models (LLMs) increasingly play an important role in a wide range of information processing and management tasks in industry. Many of these tasks are performed in large batches or even offline, and the performance indicator for which is throughput. These tasks usually show the characteristic of prefix sharing, where different prompt input can partially show the common prefix. However, the existing LLM inference engines tend to optimize the streaming requests and show limitations of supporting the large batched tasks with the prefix sharing characteristic. The existing solutions use the LRU-based cache to reuse the KV context of common prefix between requests. The KV context that are about to be reused may be prematurely evicted with the implicit cache management. Besides, the streaming oriented systems do not leverage the request-batch information and can not mix the decoding tokens with the prefill chunks to the best for the batched scenarios, and thus fails to saturate the GPU. We propose BatchLLM to address the above problems. BatchLLM explicitly identifies the common prefixes globally. The requests sharing the same prefix will be scheduled together to reuse the KV context the best. BatchLLM reorders the requests and schedules the requests with larger ratio of decoding first to better mix the decoding tokens with the latter prefill chunks, and applies memory-centric token batching to enlarge the token-batch sizes, which helps to increase the GPU utilization. Extensive evaluation shows that BatchLLM outperforms vLLM and SGLang by 1.3x to 10.8x on a set of microbenchmarks and a typical industry workload under different hardware environments. Code is available at https://github.com/microsoft/MixLLM/tree/batchllm_vllm_064.


**中文摘要**:

工业界大量信息处理任务以大批量甚至离线方式执行L，吞吐量为关键指标。我们提出BatchLLM，通过全局识别公共前缀并共同调度共享前缀的请求来优化大批量LLM推理。BatchLLM重新排序请求优先调度解码比例大的请求以更好混合解码token与预填充块，应用以内存为中心的token批处理来提高GPU利用率。广泛评估表明BatchLLM在微基准测试和典型工业工作负载上相比vLLM和SGLang实现1.3倍到10.8倍性能提升。代码见 https://github.com/microsoft/MixLLM/tree/batchllm_vllm_064。


---


## [Spira: Exploiting Voxel Data Structural Properties for Efficient Sparse Convolution in Point Cloud Networks](https://mlsys.org/virtual/2026/poster/3574)


**英文摘要 (English Abstract)**:

Sparse Convolution (SpC) powers 3D point cloud networks widely used in autonomous driving and augmented/virtual reality. SpC builds a kernel map that stores mappings between input voxel coordinates, output coordinates, and weight offsets, then uses this map to compute feature vectors for output coordinates. Our work identifies three key properties of voxel coordinates: they are integer-valued, bounded within a limited spatial range, and geometrically continuous, i.e., neighboring voxels on the same object surface are highly likely to exist at small spatial offsets from each other. Prior SpC engines do not fully exploit these properties and suffer from high pre-processing and post-processing overheads during kernel map construction. To this end, we design Spira, the first voxel-property-aware SpC engine for GPUs. Spira proposes (i) a high-performance one-shot search algorithm that builds the kernel map with no pre-processing and high data locality, (ii) an effective packed-native processing scheme that accesses packed voxel coordinates at low cost, (iii) a flexible dual-dataflow execution mechanism that efficiently computes output feature vectors by adapting to layer characteristics, and (iv) a network-wide parallelization strategy that builds kernel maps for all SpC layers concurrently at network start. Our evaluation shows that Spira significantly outperforms prior state-of-the-art SpC engines by 1.68x on average and up to 3.04x for end-to-end inference, and by 2.11x on average and up to 3.44x for layer-wise execution across diverse layer configurations. The source code of Spira is freely available at https://github.com/SPIN-Research-Group/Spira.


**中文摘要**:

稀疏卷积驱动着自动驾驶和AR/VR中广泛使用的3D点云网络。我们识别了体素坐标的三个关键属性：整数值、在有限空间范围内有界、几何连续。先前SpC引擎未充分利用这些属性。我们设计Spira，首个体素属性感知GPU SpC引擎，提出高性能一次性搜索算法、有效打包原生处理方案、灵活双数据流执行机制和网络级并行策略。端到端推理平均1.68倍加速、最高3.04倍。代码见 https://github.com/SPIN-Research-Group/Spira。


---


## [HADIS: Hybrid Adaptive Diffusion Model Serving for Efficient Text-to-Image Generation](https://mlsys.org/virtual/2026/poster/10177)


**英文摘要 (English Abstract)**:

Adapting large language models (LLMs) via reinforcement learning (RL) is often bottlenecked by the generation stage, which can consume over 75% of the training time. Speculative decoding (SD) accelerates autoregressive generation in serving systems, but its behavior under RL training remains largely unexplored. We identify three critical gaps that hinder the naïve integration of SD into RL systems: diminishing speedups at large batch sizes, drafter staleness under continual actor updates, and drafter-induced policy degradation. To address these gaps, we present ReSpec, a system that adapts SD to RL through three complementary mechanisms: dynamically tuning SD configurations, evolving the drafter via knowledge distillation, and weighting updates by rollout rewards. On Qwen models (3B–14B), ReSpec achieves up to 4.5x speedup while preserving reward convergence and training stability, providing a practical solution for efficient RL-based LLM adaptation.


**中文摘要**:

文本到图像生成服务需要在高吞吐量和低延迟之间取得平衡。HADIS是一种混合自适应扩散模型服务系统，结合了多种扩散模型的优势，根据用户请求的复杂度动态选择最适合的模型和参数配置，在保持图像质量的同时显著降低了服务延迟和计算成本。


---


## [Shannonic: Efficient Entropy-Optimal Compression for ML Workloads](https://mlsys.org/virtual/2026/poster/3597)


**英文摘要 (English Abstract)**:

We present Shannonic, a lossless compression method for machine learning tensors that achieves near-entropy-optimal compression, minimal state footprint, and high throughput. Shannonic uses an off-line pre-processing step to partition the tensor value space into optimally selected subranges and generates encoding/decoding tables that encode each value as a (range index, offset) pair where the range is entropy encoded using the asymmetric numeral systems (ANS) method. We formally prove and empirically show that Shannonic achieves higher compression efficiency than standard ANS. For a variety of 8b-quantized models, Shannonic's codec uses just 530B of state and achieves coding efficiency within 1% of the Shannon limit. Shannonic enables 1.3-3.1x faster federated learning over bandwidth-constrained networks and 29-32% latency reduction in edge-cloud LLM inference.


**中文摘要**:

机器学习工作负载中的张量压缩可以减少网络传输和存储开销。我们提出Shannonic，一种接近熵最优的ML张量无损压缩方法，使用离线预处理步骤将张量值空间划分为最优选择的子范围。对于各种8位量化模型，Shannonic的编解码器仅使用530B状态，编码效率在香农极限的1%以内。Shannonic使带宽受限网络上的联邦学习加速1.3-3.1倍，边缘-云端LLM推理延迟降低29-32%。


---


## [Optimizing Deployment Configurations for LLM Inference](https://mlsys.org/virtual/2026/poster/3557)


**英文摘要 (English Abstract)**:

Advancements in large language models (LLMs) have made them increasingly useful for complex reasoning tasks which previously required domain experts. One such task is quality evaluation of query responses produced by a search engine. Evaluation generates metrics necessary to study the quality, impact, and usefulness of product changes and features. Typically, to compute evaluation metrics, human experts are asked to rate various attributes of search responses. This process is generally quite expensive and requires several days to complete. As an alternative, LLMs are now being used to perform rating tasks with lower costs and latency. In addition, many new metrics are being developed to evaluate Google's new AI-based offerings, which require ratings too. As a result, there is much higher demand for LLM rating prediction tasks in comparison with the allocated TPU (Tensor Processing Unit) budget. A larger portion of the company's TPU resources are reserved for serving live user traffic. In this paper, we present the AI Rater Service (AIRS), an inference pipeline that employs several software engineering techniques to generate AI ratings with high reliability and low latency. AIRS maximizes LLM inference throughput by optimizing TPU resource utilization across various evaluation workflows, while minimizing latency for higher priority tasks.


**中文摘要**: [待翻译]


---


## [Ontology-Guided Long-Term Agent Memory for Conversational RAG](https://mlsys.org/virtual/2026/poster/3515)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


## [SkipKV: Selective Skipping of KV Generation and Storage for Efficient Inference with Large Reasoning Models](https://mlsys.org/virtual/2026/poster/3641)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


## [Accelerating LLM Inference: Self-Speculative Decoding via Learned Seed Injection](https://mlsys.org/virtual/2026/poster/10178)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


## [NeSyKV: Neuro-Symbolic Architecture-Specific KV-Cache Eviction for LLM Inference](https://mlsys.org/virtual/2026/poster/10173)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


## [RaidServe: High-performance Resilient Serving](https://mlsys.org/virtual/2026/poster/3633)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**:

LLM服务集群的节点故障可能导致服务中断。RaidServe是一个高性能弹性服务系统，借鉴RAID存储思想将服务状态冗余分布在多个节点上。在节点故障时能够快速恢复服务而不需要完全重启，提高了LLM服务集群的可用性和韧性。


---


## [Shortcut-connected Expert Parallelism for Accelerating Mixture of Experts](https://mlsys.org/virtual/2026/poster/10175)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


## [Stream2LLM: Overlap Context Streaming and Prefill for Reduced Time-to-First-Token](https://mlsys.org/virtual/2026/poster/3619)


**英文摘要 (English Abstract)**:

Context retrieval systems for LLM inference face a critical challenge: high retrieval latency creates a fundamental tension between waiting for complete context and proceeding without it. We present Stream2LLM, a streaming-aware LLM serving system for concurrent prefill-decode disaggregated deployments. Our evaluation demonstrates that streaming architecture delivers up to 11x TTFT improvements.


**中文摘要**:

卫星图像的低延迟交付对时间关键应用至关重要。我们提出EarthSight，一个将卫星图像智能重新定义为轨道与地面之间分布式决策问题的分布式运行时框架。EarthSight引入了使用共享骨干的多任务推理、地面站查询调度器和动态过滤排序。评估显示EarthSight将每张图像的平均计算时间减少了1.9倍。


---


## [On the Diminishing Returns of Expert Load Balancing in MoE LLM Serving](https://mlsys.org/virtual/2026/poster/10193)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**:

MoE LLM服务中专家负载均衡被广泛优化，但过度均衡可能带来递减收益。本文分析了MoE LLM服务中专家负载均衡的收益递减现象，通过理论分析和实验验证揭示了在专家数量较大时继续优化负载均衡的边际收益递减规律。


---


## [FaaScale: Unlocking Fast LLM Scaling for Serverless Inference](https://mlsys.org/virtual/2026/poster/3546)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**:

LLM推理服务的负载波动要求弹性扩缩容能力。FaaScale通过无服务器架构实现了LLM推理的快速弹性扩展，利用无服务器计算的弹性特性根据请求量自动扩缩容推理实例，在保证延迟SLO的同时最小化了资源浪费和运营成本。


---


## [Locality-Aware Beam Scheduling for Efficient Test-Time Compute with a Consumer-grade GPU](https://mlsys.org/virtual/2026/poster/3565)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


## [Meeting SLOs, Slashing Hours: Automated Enterprise LLM Optimization with OptiKIT](https://mlsys.org/virtual/2026/poster/3529)


**英文摘要 (English Abstract)**:

Enterprise LLM deployment faces a critical scalability challenge: organizations must optimize models systematically to scale AI initiatives within constrained compute budgets, yet the specialized expertise required for manual optimization remains a niche and scarce skillset. We present OptiKIT, a distributed LLM optimization framework that democratizes model compression and tuning by automating complex optimization workflows for non-expert teams.


**中文摘要**:

企业LLM部署面临关键的可扩展性挑战——组织必须在有限的算力预算内系统优化模型，而所需专业知识是稀缺技能。我们提出OptiKIT，一个分布式LLM优化框架，通过自动化复杂优化工作流为缺乏专业知识的团队实现模型压缩和调优的民主化。在生产中提供超过2倍GPU吞吐量提升。


---


## [Beat the long tail: Distribution-Aware Speculative Decoding for RL Training](https://mlsys.org/virtual/2026/poster/3543)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


## [HiSpec: Hierarchical Speculative Decoding for LLMs](https://mlsys.org/virtual/2026/poster/10202)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


## [Demystifying the Mixture of Experts Serving Tax](https://mlsys.org/virtual/2026/poster/3541)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


## [SHIP: SRAM-Based Huge Inference Pipelines for Fast LLM Serving](https://mlsys.org/virtual/2026/poster/3611)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


## [BEAM: Joint Resource–Power Optimization for Energy-Efficient LLM Inference under SLO contraints](https://mlsys.org/virtual/2026/poster/3626)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


## [ReSpec: Towards Optimizing Speculative Decoding in Reinforcement Learning Systems](https://mlsys.org/virtual/2026/poster/3613)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


## [AIRS: Scaling Live Inference in Resource Constrained Environments](https://mlsys.org/virtual/2026/poster/3558)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


## [LYNX: Workload-Agnostic Expert Remapping for Efficient MoE Inference](https://mlsys.org/virtual/2026/poster/10188)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


## [When Enough is Enough: Rank-Aware Early Termination for Vector Search](https://mlsys.org/virtual/2026/poster/3612)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


## [BOOST: BOttleneck-Optimized Scalable Training Framework for Low-Rank Large Language Models](https://mlsys.org/virtual/2026/poster/3607)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


# LLM 训练系统（22 篇）


## [ProTrain: Efficient LLM Training via Automatic Memory Management](https://mlsys.org/virtual/2026/poster/3577)


**英文摘要 (English Abstract)**:

Memory pressure has emerged as a dominant constraint in scaling the training of large language models (LLMs), particularly in resource-constrained environments. While modern frameworks incorporate various memory-saving techniques, they often expose low-level configuration knobs that require manual tuning and specialized system expertise. This not only adds engineering overhead but also risks suboptimal hardware utilization when misconfigured. This paper introduces ProTrain, a novel training system that automatically tailors memory management policies to the model architecture and underlying hardware resources, eliminating the need for manual intervention. The core of ProTrain is its automated memory management that abstracts complex memory management strategies into a few tunable configuration parameters, allowing searches for optimal parameter settings using cost models. ProTrain is equipped with a runtime profiler that provides precise estimates of latency, memory usage, and I/O bandwidth to build high-fidelity cost models. ProTrain does not change the training algorithm and thus does not compromise accuracy. Experiments show that ProTrain improves training throughput by 1.43× to 2.71× compared to the state-of-the-art training systems.


**中文摘要**:

内存压力已成为扩展大语言模型训练的主要制约因素，尤其在资源受限环境中。虽然现代框架集成了各种内存节省技术，但它们通常暴露需要手动调优和专门系统知识的低级配置选项，这不仅增加了工程开销，还可能在配置错误时导致硬件利用率不佳。本文介绍ProTrain，一个新颖的训练系统，能根据模型架构和底层硬件资源自动定制内存管理策略，消除了手动干预的需要。ProTrain的核心是其自动内存管理，将复杂的内存管理策略抽象为几个可调配置参数，允许使用成本模型搜索最优参数设置。ProTrain配备运行时分析器，提供对延迟、内存使用和I/O带宽的精确估计以构建高保真成本模型。ProTrain不改变训练算法，因此不会影响精度。实验表明，ProTrain相比最先进的训练系统将训练吞吐量提高了1.43至2.71倍。


---


## [FP8-Flow-MoE: A Casting-Free FP8 Recipe without Double Quantization Error](https://mlsys.org/virtual/2026/poster/3514)


**英文摘要 (English Abstract)**:

Scaling up training large language models (LLMs) in computing and data perspectives motivates distributed training across different geo-distributed data centers. Communication in geo-distributed data parallel training (DDP) with stochastic gradient descent (S-SGD) is the main bottleneck in low-bandwidth environments. Recent studies have successfully applied Local SGD to mitigate the communication overhead and geo-distributedly pre-train LLMs. However, we identify that the strict model synchronization mechanism in Local SGD prevents overlapping communication and computation, which makes the system lose opportunities to overlap communication and computation. To overcome this limitation, we expand the design space of local SGD by layer-wisely decoupling model synchronization. In each iteration, only partial layers are synchronized instead of the entire model after a specific number of iterations. Leveraging this methodology, we introduce DreamDDP, a training framework to accelerate low-bandwidth distributed training with three key innovations: (1) partial local SGD with theoretical assurances of convergence rates comparable to S-SGD; (2) overlapping parameter synchronization with computation without extra GPU memory occupation; (3) identifying and exploiting three properties to schedule communication and computation based on fine-grained layer-wise profiling to reduce training time. Empirical evaluations conducted on 32 GPUs using prominent deep learning models, including ResNet-18, ResNet-50, GPT-2, and Llama-2, demonstrate that DreamDDP enhances the convergence properties of Local SGD (and Adam) and achieves speedups ranging from 1.49× to 3.91× over leading baseline methods.


**中文摘要**: [待翻译]


---


## [DreamDDP: Accelerating Low-Bandwidth Geo-Distributed LLM Training with Layer-wise Partial Synchronization](https://mlsys.org/virtual/2026/poster/3567)


**英文摘要 (English Abstract)**:

Production LLM deployments lack systematic methods to assess output consistency risks when infrastructure changes. We present DriftBench, a measurement and prediction framework comprising 236,985 prompt-response pairs across 105 configurations spanning 5 models, 4 GPU platforms, 3 frameworks, 3 precisions. We develop the Portability Risk Index (PRI), achieving held-out-dimension generalization of R²=0.909 for unseen hardware and R²=0.763 for unseen precision (R² ranges up to 1.0; higher is better). We discover a fundamental dichotomy: hardware/precision changes exhibit systematic drift (R²≥0.76) enabling predict-once deployment, while framework/model changes show idiosyncratic drift (R²<0.48) requiring re-measurement. Production validation blocked a high-drift upgrade where 23.85% of safety prompts flipped between safe and unsafe classifications (nearly 1 in 4 answers changed from safe to unsafe or unsafe to safe), demonstrating operational value. Our contribution is measurement and risk assessment; we do not propose drift mitigation techniques, as this remains an open challenge for future work.


**中文摘要**:

从计算和数据维度扩展LLM训练激发了跨不同地理分布式数据中心进行分布式训练的需求。在低带宽环境中，使用随机梯度下降进行地理分布式数据并行训练的通信是主要瓶颈。最近的研究已成功应用Local SGD来缓解通信开销并进行LLM的地理分布式预训练。然而，我们发现Local SGD中严格的模型同步机制阻碍了通信和计算的重叠，使系统丧失了重叠通信和计算的机会。为克服这一限制，我们通过逐层解耦模型同步来扩展Local SGD的设计空间。在每次迭代中，只有部分层被同步，而非在特定迭代次数后同步整个模型。利用这一方法，我们引入DreamDDP，一个加速低带宽分布式训练的训练框架，包含三个关键创新：具有与S-SGD相当收敛速率理论保证的部分Local SGD；在不占用额外GPU内存的情况下重叠参数同步与计算；基于细粒度逐层分析来识别和利用三个属性来调度通信和计算以减少训练时间。在使用ResNet-18、ResNet-50、GPT-2和Llama-2等模型在32个GPU上进行的实证评估表明，DreamDDP增强了Local SGD的收敛特性，并实现了相比领先基线方法1.49至3.91倍的加速。


---


## [NEST: Network- and Memory-Aware Device Placement for Distributed Deep Learning](https://mlsys.org/virtual/2026/poster/3544)


**英文摘要 (English Abstract)**:

The growing scale of deep learning demands distributed training frameworks that jointly reason about parallelism, memory, and network topology. We present NEST, a network-, compute-, and memory-aware device placement framework that unifies model parallelism, topology modeling, and memory feasibility via structured dynamic programming. Evaluations across diverse hardware and networks show NEST achieves up to 2.43 times higher throughput, better memory efficiency, and improved scalability over state-of-the-art baselines.


**中文摘要**:

深度学习规模的不断增长要求分布式训练框架联合推理并行性、内存和网络拓扑。先前工作通常依赖启发式或拓扑无关的搜索，将通信和内存分开处理。没有逐设备内存感知，这些方法通常通过跨多个设备分片参数和激活来事后确保可行性，增加了同步、膨胀了通信并低效利用计算——限制了在真实数据中心网络上的可扩展性和效率。我们提出NEST，一个网络、计算和内存感知的设备放置框架，通过结构化动态规划统一模型并行性、拓扑建模和内存可行性。NEST的DP在具有张量和专家并行配置、跨层次化或任意网络的显式AllReduce延迟以及内存/计算配置文件的算子图上操作。通过跨张量、流水线、数据和专家维度分解并行性，NEST为混合策略定义了一个有原则的搜索空间，同时联合优化共置、网络延迟和内存可行性。跨多种硬件和网络的评估显示，NEST相比最先进基线实现了高达2.43倍更高的吞吐量、更好的内存效率和改进的可扩展性。源代码见 https://github.com/scai-tech/Nest。


---


## [MixLLM: LLM Quantization with Global Mixed-precision between Output-features and Highly-efficient System Design](https://mlsys.org/virtual/2026/poster/3582)


**英文摘要 (English Abstract)**:

Quantization has become one of the most effective methodologies to compress LLMs into smaller size. We propose MixLLM that explores the optimization space of mixed-precision quantization between output features, based on the insight that different features matter differently in the model. MixLLM identifies the important output features in the global view, effectively assigning larger bit-width to output features that need it the most. Extensive experiments show that with only 10% more bits, the perplexity increase can be reduced from about 0.5 in SOTA to within 0.2 for Llama 3.1 70B.


**中文摘要**:

量化已成为将LLM压缩到更小尺寸的最有效方法之一。然而，现有量化方案仍存在不可忽略的精度下降或系统效率低的局限性。本文提出MixLLM，探索输出特征间混合精度量化的优化空间，基于不同输出特征在模型中重要性不同的洞察。MixLLM在全局视角而非单层内识别重要输出特征，有效地为最需要的输出特征分配更大的位宽，以实现高精度和低内存使用。我们提出算法-系统协同设计的量化配置最佳点，实现高精度和系统效率。为解决系统挑战，我们设计了两步反量化以轻松利用Tensor Core，以及快速数据类型转换以减少反量化开销，并提出软件流水线以最佳重叠内存访问、反量化和矩阵乘法。大量实验表明，仅增加10%的位宽，Llama 3.1 70B的困惑度增加可从SOTA的约0.5降至0.2以内，而三个流行模型的MMLU-Pro损失可从1.92降至0.99。除优越的精度外，MixLLM还实现了最先进的系统效率。代码见 https://github.com/microsoft/MixLLM。


---


## [HetRL: Efficient Reinforcement Learning for LLMs in Heterogeneous Environments](https://mlsys.org/virtual/2026/poster/3602)


**英文摘要 (English Abstract)**:

As large language models (LLMs) continue to scale and new GPUs are released even more frequently, there is an increasing demand for LLM post-training in heterogeneous environments. We present HetRL, a distributed system for efficient RL training in infrastructures with heterogeneous GPUs and networks. Our extensive evaluation, consuming 20,000 GPU-hours, shows that HetRL achieves up to 9.17x the throughput of state-of-the-art systems, and 3.17x on average.


**中文摘要**:

随着大语言模型持续扩展和新GPU更频繁地发布，在异构环境中进行LLM后训练以充分利用未充分利用的中档或前代GPU并缓解同构高端GPU短缺的需求日益增长。然而，在异构环境中为LLM实现高性能强化学习训练仍然具有挑战性，因为工作流涉及多个模型和具有复杂计算和数据依赖关系的任务。本文提出HetRL，一个在异构GPU和网络基础设施中实现高效RL训练的分布式系统。HetRL将异构环境中的RL训练调度形式化为约束联合优化问题，并提供两种互补方法：一个高效识别近优解的混合调度算法，以及一个获得最优解的基于整数线性规划的调度算法。我们广泛的评估消耗了20,000 GPU小时，显示HetRL在广泛的工作负载和设置中实现了相比最先进系统高达9.17倍、平均3.17倍的吞吐量。


---


## [Unleashing Scalable Context Parallelism for Foundation Models Pre-Training via FCP](https://mlsys.org/virtual/2026/poster/3599)


**英文摘要 (English Abstract)**:

Context parallelism (CP) has been widely adopted to support the growing context length in foundation model pretraining. We propose FCP, a flexible context parallelism paradigm that shards and schedules sequences at block-level granularity. Instead of relying on rigid communication topologies such as ring, FCP enables arbitrary peer-to-peer communication, allowing flexible placement of sequence blocks across workers. Extensive evaluations show that FCP attains near-linear scalability on up to 256 NVIDIA GPUs.


**中文摘要**:

上下文并行性已被广泛采用以支持基础模型预训练中不断增长的上下文长度。然而，现有设计无法处理训练数据集中序列长度的大幅变化，导致性能不佳。这些方法通常对短序列过度分片，导致计算效率低下和过多的通信，或将长序列和短序列分开处理而没有适当的装箱，造成工作负载不平衡。本文提出FCP，一个灵活的上下文并行范式，以块级粒度分片和调度序列。FCP不依赖环形等刚性通信拓扑，而是支持任意点对点通信，允许多个worker之间灵活放置序列块。通过将来自短序列和长序列的块进行装箱，FCP同时实现了高计算效率和均衡的工作负载分布。广泛评估显示FCP在最多256个NVIDIA GPU上实现近线性扩展，注意力MFU提高1.13-2.21倍。


---


## [veScale-FSDP: Flexible and High-Performance FSDP at Scale](https://mlsys.org/virtual/2026/poster/3637)


**英文摘要 (English Abstract)**:

Deep learning using large models has achieved great success in a wide range of domains. However, training these models on billions of parameters is very challenging in terms of training speed, memory cost, and communication efficiency, especially under the privacy-preserving regime with differential privacy (DP). On the one hand, the efficiency of DP optimization is comparable to that of standard non-DP optimization on a single GPU, but existing DP distributed learning is significantly inefficient on multiple GPUs. On the other hand, the Zero Redundancy Optimizer (ZeRO) is a state-of-the-art solution to the standard distributed learning, which can be technically complicated to work compatibly with DP. In this work, we develop a new systematic solution, DP-ZeRO, (I) to scale up the trainable DP model size, e.g. to GPT-100B, (II) to obtain the same computation and communication efficiency as the standard ZeRO, and (III) to enable mixed-precision DP training. Our DP-ZeRO, like the standard ZeRO, has the potential to train models with arbitrary size and exhibits excellent training efficiency on large models. Code at https://github.com/awslabs/fast-differential-privacy.


**中文摘要**:

全分片数据并行，也称为零冗余优化器，因其内存效率和可扩展性而被广泛用于大规模分布式LLM训练。然而，标准FSDP实现面临通信开销和内存碎片问题，限制了其在大规模集群上的效率。veScale-FSDP引入了灵活且高性能的FSDP变体，通过优化的分片策略、智能的参数预取和异步通信来克服这些限制。在大规模基准测试中，veScale-FSDP在保持PyTorch兼容性的同时实现了相比原生FSDP显著的吞吐量提升。


---


## [fabric-lib: RDMA Point-to-Point Communication for LLM Systems](https://mlsys.org/virtual/2026/poster/3584)


**英文摘要 (English Abstract)**:

Long-context large language model (LLM) inference faces severe KV cache inflation, making GPU memory a key bottleneck. Existing recallable sparsity methods mitigate memory pressure by offloading non-critical key–value (KV) pairs to CPU memory and recalling them on demand, they are intrusive to KV cache management in the existing inference frameworks and fail to cope with the linearly increasing recall overhead under high batches. To address these limitations, we propose OPKV, a high-throughput plugin-driven framework that seamlessly integrates recallable sparsity into paged KV cache systems and performs unified recall optimization. OPKV introduces a plugin interface that decouples sparsity logic from model and cache management, and applies object reaggregation and hot page hit algorithms to reduce the recall overhead based on the observation of spatial discreteness and temporal locality in critical KV selection. In addition, a local intra-iteration metadata manager is implemented to perform millisecond-level page retrieval and cache eviction. The experimental results show that OPKV helps the SoTA methods attain 1.3 - 1.8x higher decoding throughput under different batches.


**中文摘要**:

大语言模型的分布式训练和推理依赖高效的跨节点通信。fabric-lib是一个专门为LLM系统设计的RDMA点对点通信库，通过直接内存访问技术绕过操作系统内核和CPU参与，提供低延迟高带宽的通信原语。相比传统的TCP/IP通信，fabric-lib在大规模分布式LLM工作负载中显著降低了跨节点通信开销。


---


## [MTraining: Distributed Dynamic Sparse Attention for Efficient Ultra-Long Context Training](https://mlsys.org/virtual/2026/poster/3552)


**英文摘要 (English Abstract)**:

Attention is a fundamental building block of large language models (LLMs), so there have been many efforts to implement it efficiently. For example, FlashAttention leverages tiling and kernel fusion to optimize attention. Recently, a number of variants of attention have been introduced to enhance model quality or efficiency. Supporting them efficiently remains difficult since they usually require specialized kernels or hand-tuned implementations. FlexAttention recently addressed part of this gap by using static programming templates to support FlashAttention-like kernels for a subset of attention variants. In this paper, we introduce Flashlight, a compiler-native framework within the PyTorch ecosystem that automatically generates fused, FlashAttention-style kernels for arbitrary attention-based programs, without relying on static templates or predefined kernel specializations. Flashlight leverages PyTorch's compilation workflow to fuse and tile attention computations transparently, enabling efficient execution for diverse attention patterns. Not only does it support all variants expressible in the FlexAttention model but it also handles more general, data-dependent attention formulations that are beyond the capabilities of FlexAttention. Our results show that Flashlight produces kernels with competitive or superior performance to FlexAttention, while offering the flexibility of native PyTorch code, enabling developers to rapidly explore new attention models without sacrificing performance.


**中文摘要**:

超长上下文训练中的注意力计算呈二次增长，导致严重的计算和内存瓶颈。MTraining提出了一种面向超长上下文训练的高效分布式动态稀疏注意力系统。通过动态识别和聚焦关键注意力模式，在训练过程中自适应地调整稀疏策略，在保持模型质量的同时大幅降低了超长序列训练的计算和内存开销。


---


## [Efficient Long-Context Language Model Training by Core Attention Disaggregation](https://mlsys.org/virtual/2026/poster/3531)


**英文摘要 (English Abstract)**:

Compilers play a fundamental role at achieving peak performance for machine learning (ML) workloads. However, given the diverse nature of workloads and accelerators, compilers' heuristics and analytical cost models can result in sub-optimal performance, and thus waste precious datacenter resources. Furthermore, the multitude of tunable parameters and their complex interplay often make it impossible for human experts to manually find optimal configurations. In this paper, we present CATWILD, a system that automatically optimizes ML jobs in Google's TPU fleet using compiler autotuning techniques. We describe CATWILD's design and implementation, and evaluate its performance using a handful of representative metrics. We further report experiences and lessons learned from its five-year development and operation. To the best of our knowledge, CATWILD represents the first ML compiler autotuning solution deployed in datacenters at scale. Its successful rollout yielded substantial benefits, generating tuned configurations for a large portion of Google's TPU training workloads and achieving significant chip savings.


**中文摘要**:

长上下文LLM训练中注意力计算的二次增长导致数据并行和流水线并行组之间的负载不均衡。我们提出核心注意力分离，通过将无参数的核心注意力计算从主训练流水线中分离出来并在独立的资源池上调度来解决这一问题。CAD由两个关键观察驱动：核心注意力没有可训练参数且瞬态状态最小，平衡可简化为调度计算密集型任务；现代注意力内核在任意长度的token级分片融合批次上维持高利用率。我们在DistCA系统中实现了CAD，使用乒乓方案完全重叠通信与计算，以及就地注意力服务器提高内存利用率。扩展到512个H200 GPU和512K上下文长度，DistCA消除了DP/PP慢节点，实现了近乎完美的计算和内存平衡，相比Megatron-LM将端到端训练吞吐量提高了高达1.9倍。


---


## [GUARD: SCALABLE STRAGGLER DETECTION AND NODE HEALTH MANAGEMENT FOR LARGE-SCALE TRAINING](https://mlsys.org/virtual/2026/poster/3608)


**英文摘要 (English Abstract)**:

Training frontier-scale foundation models involves coordinating tens of thousands of GPUs over multi-month runs, where even minor performance degradations can accumulate into substantial efficiency losses. We present Guard, a scalable system for detecting stragglers and ensuring node health in large-scale training clusters. Deployed on large-scale foundation model pretraining workloads, Guard improves mean FLOPs utilization by up to 1.7x, reduces run-to-run training step variance from 20% to 1%.


**中文摘要**:

百万token级智能体应用对LLM推理服务提出了前所未有的需求。我们提出GhostServe，一种新颖的检查点方案以促进容错LLM服务。GhostServe通过在后台应用纠删码生成并存储校验分片来保护流式KV缓存。评估表明GhostServe相比现有方法将检查点延迟降低高达2.7倍、恢复延迟降低2.1倍。


---


## [FlexTrain: Scalable Hybrid-Parallel Training with Elastic Resource Utilization and Consistent Accuracy](https://mlsys.org/virtual/2026/poster/3553)


**英文摘要 (English Abstract)**:

We present FlexTrain, a scalable hybrid-parallel training system that enables elastic resource utilization while maintaining consistent model accuracy. FlexTrain dynamically adjusts the parallelization strategy based on available computational resources, allowing training jobs to efficiently scale across varying GPU counts without sacrificing model quality or convergence guarantees.


**中文摘要**:

训练作业的GPU可用性经常动态变化。我们提出FlexTrain，一个可扩展的混合并行训练系统，实现弹性资源利用同时保持一致的模型准确率。FlexTrain根据可用计算资源动态调整并行化策略，使训练作业能够在不同GPU数量间高效扩展，而不牺牲模型质量或收敛保证。


---


## [Sparing Strategies to Minimize Reliability Impact On Large Training Jobs](https://mlsys.org/virtual/2026/poster/3639)


**英文摘要 (English Abstract)**:

Training large language models (LLMs) on Meta's AI clusters requires running long, distributed jobs that are vulnerable to hardware failures. To maintain high availability and efficiency, production systems use sparing, i.e., pre-allocating spare compute resources that can replace failed components. However, choosing the optimal sparing strategy-including compute block size, number of spare blocks, and spare GPU trays—is complex and directly impacts cluster performance. We present an analytical framework with closed-form expressions to guide sparing strategy decisions, making practical, first-order recommendations for production environments. We also develop a simulation component to cross-validate the analytical model. Applied in Meta's hyperscale infrastructure, this model helps engineers optimize fault tolerance, minimize downtime, and maximize goodput during LLM training. Our real-world use case demonstrates how the framework informs robust, cost-effective design choices critical to Meta's AI operations.


**中文摘要**:

大规模训练作业的可靠性受GPU故障影响严重。本文分析了通过备用策略最小化大规模训练作业可靠性影响的方法。通过预分配备用GPU并在检测到故障时快速切换，结合智能的检查点和状态恢复机制，该策略显著降低了训练作业因硬件故障而失败或严重降级的概率。


---


## [FreeScale: Distributed Training for Sequence Recommendation Models with Minimal Scaling Cost](https://mlsys.org/virtual/2026/poster/3598)


**英文摘要 (English Abstract)**:

Modern industrial Deep Learning Recommendation Models typically extract user preferences through the analysis of sequential interaction histories. This paper introduces FreeScale, a solution designed to mitigate the straggler problem through meticulously load balanced input samples, minimize the blocking communication by overlapping prioritized embedding communications with computations, and resolve the GPU resource competition. Empirical evaluation demonstrates that FreeScale achieves up to 90.3% reduction in computational bubbles.


**中文摘要**:

现代工业深度学习推荐模型通过分析序列交互历史提取用户偏好，但在大规模训练中因数据特征异质性导致的严重慢节点和阻塞通信而产生大量计算气泡。本文介绍FreeScale，通过精心负载均衡的输入样本缓解慢节点问题，通过重叠优先嵌入通信与计算最小化阻塞通信，并通过SM-Free技术解决计算通信重叠期间的GPU资源竞争。实证评估表明FreeScale在256个H100 GPU上运行真实工作负载时实现了高达90.3%的计算气泡减少。


---


## [AXLearn: Modular, Hardware-Agnostic Large Model Training](https://mlsys.org/virtual/2026/poster/3635)


**英文摘要 (English Abstract)**:

AXLearn is a production system which facilitates scalable and high-performance training of large deep learning models. Compared to other state-of-the-art deep learning systems, AXLearn has a unique focus on modularity and support for hardware-agnostic training. AXLearn's internal interfaces between software components follow strict encapsulation, allowing different components to be assembled to facilitate rapid model development and experimentation on different hardware infrastructure. AXLearn maintains constant complexity as we scale the components in the system, compared to linear or quadratic complexity in state-of-the-art training systems. This allows integrating features such as Rotary Position Embeddings (RoPE) into AXLearn across hundreds of modules with just 10 lines of code, compared to hundreds, as required in other systems. At the same time, AXLearn maintains equivalent performance compared to state-of-the-art training systems. We also share our experience in the development and operation of AXLearn at Apple.


**中文摘要**:

AXLearn是一个促进大规模深度学习模型可扩展和高性能训练的生产系统。与其他最先进系统相比，AXLearn独特地专注于模块化和硬件无关训练。软件组件之间的内部接口遵循严格封装，允许组装不同组件以促进在不同硬件上的快速模型开发。AXLearn在扩展系统组件时保持常数复杂度，而最先进训练系统为线性或二次复杂度。这使得将RoPE等功能集成到数百个模块中只需10行代码。同时保持了与最先进系统相当的性能。


---


## [PLayer-FL: A Principled Approach to Personalized Layer-wise Cross-Silo Federated Learning](https://mlsys.org/virtual/2026/poster/3590)


**英文摘要 (English Abstract)**:

Federated learning (FL) with non-IID data often degrades client performance below local training baselines. Partial FL addresses this by federating only early layers that learn transferable features, but existing methods rely on ad-hoc, architecture-specific heuristics. We first conduct a systematic analysis of layer-wise generalization dynamics in FL, revealing an early-emerging transition between generalizable (safe-to-federate) and task-specific (should-remain-local) layers. Building on this, we introduce Principled Layer-wise Federated Learning (PLayer-FL), which aims to deliver the benefits of federation more robustly. PLayer-FL computes a novel federation-sensitivity metric efficiently after a single training epoch to choose the optimal split point for a given task. Inspired by model pruning, the metric quantifies each layer's robustness to aggregation and highlights where federation shifts from beneficial to detrimental. We show that this metric correlates strongly with established generalization measures across diverse architectures. Crucially, experiments demonstrate that PLayer-FL achieves consistently competitive performance across a wide range of tasks while distributing gains more equitably and reducing client-side regressions relative to baselines.


**中文摘要**:

非IID数据的联邦学习通常使客户端性能降至本地训练基线以下。部分联邦学习通过仅联邦化学习可迁移特征的早期层来解决此问题，但现有方法依赖特定架构的启发式。我们首先对FL中逐层泛化动态进行了系统分析，揭示了可泛化和任务特定层之间的早期过渡。基于此，引入有原则的逐层联邦学习PLayer-FL，在单个训练周期后高效计算新颖的联邦敏感性度量来选择给定任务的最佳分割点。实验表明PLayer-FL在广泛任务中持续实现有竞争力的性能，同时更公平地分配收益并减少客户端性能退化。


---


## [DisAgg: Distributed Aggregators for Efficient Secure Aggregation](https://mlsys.org/virtual/2026/poster/3614)


**英文摘要 (English Abstract)**:

Federated learning enables collaborative model training across distributed clients, yet vanilla FL exposes client updates to the central server. We propose DisAgg that leverages a small committee of clients called Aggregators to perform the aggregation itself. This design eliminates local masking and expensive homomorphic encryption. DisAgg processes 100k-dimensional update vectors from 100k 5G clients with a 4.6x speedup compared to OPA.


**中文摘要**:

联邦学习中的安全聚合保护客户端更新隐私，但现有方案存在通信轮次多或加密开销高的问题。我们提出DisAgg，利用一小部分客户端作为聚合器执行聚合本身。每个客户端将其更新向量秘密共享给聚合器，聚合器本地计算部分和并仅返回聚合分片供服务器端重建。该设计消除了本地掩码和昂贵的同态加密。处理来自100k个5G客户端的100k维更新向量相比OPA实现4.6倍加速。


---


## [FLoRIST: Singular Value Thresholding for Efficient and Accurate Federated Fine-Tuning of Large Language Models](https://mlsys.org/virtual/2026/poster/3617)


**英文摘要 (English Abstract)**:

Integrating Low-Rank Adaptation (LoRA) into federated learning offers a promising solution for parameter-efficient fine-tuning of Large Language Models (LLMs) without sharing local data. We propose FLoRIST, a federated fine-tuning framework that achieves mathematically accurate aggregation without incurring high communication or computational overhead. Extensive empirical evaluations demonstrate that FLoRIST consistently strikes the best balance between communication efficiency and competitive performance.


**中文摘要**:

将LoRA集成到联邦学习为LLM的参数高效微调提供了有前景的解决方案。我们提出FLoRIST，一个实现数学上准确聚合而不产生高通信或计算开销的联邦微调框架。通过在服务器端对堆叠的本地适配器分别执行奇异值分解，在紧凑中间空间中操作。引入可调奇异值阈值进行服务器端最优秩选择。广泛实证评估表明FLoRIST在通信效率和竞争性能之间持续达到最佳平衡。


---


## [MoEBlaze: Breaking the Memory Wall for Efficient MoE Training on Modern GPUs](https://mlsys.org/virtual/2026/poster/3603)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


## [HexiScale: Facilitating Large Language Model Training over Heterogeneous Hardware](https://mlsys.org/virtual/2026/poster/3605)


**英文摘要 (English Abstract)**:

Training large language models (LLMs) is a computationally intensive task, typically conducted in data centers with homogeneous high-performance GPUs. We propose HexiScale, a novel system that can flexibly support asymmetric partition of training computations in the scope of data-, pipeline-, and tensor model parallelism. Compared to heterogeneous baselines, HexiScale delivers 1.5x to 2.4x higher throughput.


**中文摘要**:

生成模型正在重塑直播行业。我们提出StreamDiffusionV2，一个无需训练的交互式直播视频扩散流水线，集成了SLO感知批处理调度器和块调度器。在无需TensorRT或量化的情况下，StreamDiffusionV2在四块H100 GPU上使用14B参数模型在0.5秒内渲染首帧并达到58.28 FPS。


---


## [FarSkip-Collective: Unhobbling Blocking Communication in Mixture of Experts Models](https://mlsys.org/virtual/2026/poster/3520)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


# Agentic AI（智能体）（11 篇）


## [VeriMoA: A Mixture-of-Agents Framework for Spec-to-HDL Generation](https://mlsys.org/virtual/2026/poster/3632)


**英文摘要 (English Abstract)**:

Automation of Register Transfer Level (RTL) design can help developers meet increasing computational demands. Large Language Models (LLMs) show promise for Hardware Description Language (HDL) generation, but face challenges due to limited parametric knowledge and domain-specific constraints. While prompt engineering and fine-tuning have limitations in knowledge coverage and training costs, multi-agent architectures offer a training-free paradigm to enhance reasoning through collaborative generation. However, current multi-agent approaches suffer from two critical deficiencies: susceptibility to noise propagation and constrained reasoning space exploration. We propose VeriMoA, a training-free mixture-of-agents (MoA) framework with two synergistic innovations. First, a quality-guided caching mechanism to maintain all intermediate HDL outputs and enables quality-based ranking and selection across the entire generation process, encouraging knowledge accumulation over layers of reasoning. Second, a multi-path generation strategy that leverages C++ and Python as intermediate representations, decomposing specification-to-HDL translation into two-stage processes that exploit LLM fluency in high-resource languages while promoting solution diversity. Comprehensive experiments on VerilogEval 2.0 and RTLLM 2.0 benchmarks demonstrate that VeriMoA achieves 15--30% improvements in Pass@1 across diverse LLM backbones, especially enabling smaller models to match larger models and fine-tuned alternatives without requiring costly training.


**中文摘要**:

寄存器传输级设计的自动化可以帮助开发者满足日益增长的计算需求。大语言模型在硬件描述语言生成方面展现出潜力，但因参数知识有限和领域特定约束而面临挑战。尽管提示工程和微调在知识覆盖和训练成本方面存在局限，但多智能体架构提供了一种无需训练的范式，通过协作生成来增强推理能力。然而，当前的多智能体方法存在两个关键缺陷：易受噪声传播影响和推理空间探索受限。我们提出VeriMoA，一个无需训练的混合智能体框架，具有两项协同创新。首先，质量引导的缓存机制维护所有中间HDL输出，并在整个生成过程中实现基于质量的排序和选择，促进知识在推理层间的积累。其次，多路径生成策略利用C++和Python作为中间表示，将规格到HDL的转换分解为两阶段过程，充分利用LLM在高资源语言中的流畅性，同时促进解决方案的多样性。在VerilogEval 2.0和RTLLM 2.0基准测试上的全面实验表明，VeriMoA在多种LLM主干上实现了15-30%的Pass@1提升，尤其使较小模型能够匹敌更大模型和微调方案，而无需昂贵的训练。


---


## [Matrix: Peer-to-Peer Multi-Agent Synthetic Data Generation Framework](https://mlsys.org/virtual/2026/poster/3530)


**英文摘要 (English Abstract)**:

Synthetic data has become increasingly important for training large language models, especially when real data is scarce, expensive, or privacy-sensitive. We present Matrix, a decentralized framework that represents both control and data flow as serialized messages passed through distributed queues. This peer-to-peer design eliminates the central orchestrator. Built on Ray, Matrix scales to tens of thousands of concurrent agentic workflows. In all cases, Matrix achieves 2-15x higher data generation throughput under identical hardware resources, without compromising output quality.


**中文摘要**:

合成数据对训练大语言模型越来越重要，尤其在真实数据稀缺、昂贵或隐私敏感时。许多此类生成任务需要协调的多智能体工作流，其中专门化智能体协作产生更高质量、更多样且结构更丰富的数据。然而，现有的多智能体合成框架通常依赖集中式编排器，产生可扩展性瓶颈，或为特定领域硬编码，限制了灵活性。我们提出Matrix，一个去中心化框架，将控制流和数据流表示为通过分布式队列传递的序列化消息。这种点对点设计消除了中央编排器。每个任务通过轻量级智能体独立推进，而计算密集型操作由分布式服务处理。基于Ray构建，Matrix可扩展到数万个并发智能体工作流，并提供模块化、可配置的设计，能够轻松适配广泛的数据生成工作流。我们在多种合成场景下评估了Matrix，在所有情况下，Matrix在相同硬件资源下实现了2-15倍更高的数据生成吞吐量，而不牺牲输出质量。


---


## [Agentic Operator Generation for ML ASICs](https://mlsys.org/virtual/2026/poster/3594)


**英文摘要 (English Abstract)**:

Clients are evolving beyond chat completion, and now include a variety of innovative inference-time scaling and deep reasoning techniques. At the same time, inference servers remain heavily optimized for chat completion and thus largely use linear KV cache strategies. Prior work has shown that large improvements to KV cache hit rate are possible if inference servers evolve towards these more non-linear use cases. However, they offer solutions that are also optimized for a single use case, RAG. In this paper, we demonstrate that chat, RAG, inference-time scaling, and agentic workloads can be expressed as special cases of a more general structure, the span query. The critical distinction that had been assumed by prior work lies in whether the order of the inputs matters. Do they commute? In chat, they do not. In RAG, they often do. A span query is an expression tree of inference calls, linked together with commutativity constraints. We describe span query syntax and semantics. We show how they can be automatically optimized to improve KV cache locality. We show how a small change to vLLM (affecting only 492 lines) can enable high-performance execution of span queries. Using this stack, we demonstrate that span queries can achieve 10-20x reductions in TTFT for two distinct non-chat use cases. Finally, we show that span queries can also be optimized to improve attention locality, so as to avoid the so-called lost-in-the-middle problem. We demonstrate that an attention-optimized span query on a 2b parameter model vastly outperforms the accuracy of a stock inference server using an 8b model.


**中文摘要**:

ML ASIC的开发需要大量手动优化的底层算子代码。本文提出了面向ML ASIC的智能体算子生成方法，利用LLM智能体自动从硬件规格描述生成和优化专用AI加速器的底层算子代码。系统通过迭代测试和反馈循环持续改进生成的代码质量，大幅缩短了ASIC算子开发周期，同时生成的代码性能接近甚至超过手工优化版本。


---


## [AccelOpt: A Self-Improving LLM Agentic System for AI Accelerator Kernel Optimization](https://mlsys.org/virtual/2026/poster/10168)


**英文摘要 (English Abstract)**:

Early-Exit Large Language Models (EE-LLMs) enable high throughput inference by allowing tokens to exit early at intermediate layers. However, their throughput is limited by the computational and memory savings. Existing EE-LLM frameworks rely on a single model and therefore, their token generation latencies are bottlenecked by tokens that do not exit early and traverse additional layers. Moreover, early exits are only known at runtime and depend on the request. Therefore, these frameworks load the weights of all model layers even though large portions remain unused when tokens exit early. The lack of memory savings limit us from scaling the batch sizes. We propose HELIOS, a framework that improves both token generation latency and batch sizes to enable high-throughput in EE-LLMs. HELIOS exploits two insights. First, early exits are often complementary across models — tokens that do not exit early on one model often take an early-exit on another. HELIOS employs multiple models and dynamically switches between them to collectively maximize the number of tokens that exit early, and minimize token generation latencies. Second, even when a predicted token does not exit early due to poor confidence, it often remains unchanged even after additional layer traversal. HELIOS greedily allows such tokens to exit early and only loads the weights of the most likely to be used layers, yielding memory savings which is then re-purposed to increase batch sizes. HELIOS employs real-time profiling to accurately identify the early-exit distributions, and adaptively switches between models by tracking tokens in real-time to minimize the performance degradation caused by greedy model loading and exiting. Our evaluations show that HELIOS achieves 1.48× higher throughput and 15.14× larger batch size compared to existing EE-LLM frameworks.


**中文摘要**:

AI加速器内核优化是一个耗时且需要专业知识的过程。AccelOpt提出了一个自改进的LLM智能体系统，自动生成、测试和优化加速器内核代码。智能体通过分析性能分析数据和编译器反馈持续学习和改进，实现了内核优化过程的自动化，在多种加速器平台上生成的代码性能接近或超过手工优化版本。


---


## [Impact of Scheduling for Terminal Agent Workloads on Unified-Memory Workstations](https://mlsys.org/virtual/2026/poster/10203)


**英文摘要 (English Abstract)**:

Decentralized machine learning relies on peer-to-peer communication, yet the role of network topology in shaping learning dynamics remains poorly understood due to the lack of controlled, reproducible evaluation frameworks. We present SONAR, a modular framework for topology-aware decentralized learning that unifies communication, topology management, and fine-grained telemetry, enabling end-to-end measurement of performance, communication, robustness, and privacy under consistent conditions. Using SONAR, we show that topology is a first-class systems variable whose impact amplifies with scale and data heterogeneity. We find that sparse, structured topologies (e.g., rings and tori) can achieve comparable or superior accuracy to dense graphs at substantially lower communication cost under circumstances, revealing a clear efficiency frontier. We further identify and provide insights on collaborator collapse, a systematic failure mode in adaptive collaboration, where similarity-based neighbor selection reduces diversity and degrades generalization. By exposing topology as a controllable and measurable dimension, SONAR enables systematic, reproducible evaluation of decentralized learning and provides practical guidance for designing efficient and robust collaborative systems.


**中文摘要**: [待翻译]


---


## [Optimizing PyTorch Inference with LLM-Based Multi-Agent Systems](https://mlsys.org/virtual/2026/poster/3600)


**英文摘要 (English Abstract)**:

Large Language Models (LLMs) are central to modern NLP applications, yet their deployment on consumer-grade GPUs is limited by limited memory capacity and bandwidth. In typical single-batch inference on local devices, the key–value (KV) cache occupies only a small fraction of total memory, so prior studies have largely focused on model weights. The rise of test-time compute (TTC), however, introduces a new bottleneck: the rapidly expanding KV cache. In TTC methods such as step-wise beam search, concurrent decoding paths cause KV cache size and transfer costs to scale with exploration space, resulting in severe I/O stalls on consumer-grade GPUs. We identify two complementary forms of data locality in TTC workloads. Inter-token locality occurs within each decoding step, as consecutive tokens in the same beam access nearly identical KV cache data. Inter-beam locality arises across decoding steps, as beams that share common prefixes reuse overlapping KV segments. Building on these observations, we propose Locality-Aware Beam Scheduling, which exploits these locality patterns to reduce redundant KV cache transfers. It also employs balanced grouping with prefetching to overlap data movement with computation. Evaluated on OPT-6.7B, LLaMA-2-7B, and Qwen-7B, our method reduces KV cache transfer volume by over 95% and achieves consistent end-to-end speedups of 3.39×–9.72×, 3.60×–8.74×, and 4.17×–7.99×, respectively, compared to layer-wise offloading.


**中文摘要**:

PyTorch模型的推理优化通常需要深入的框架知识。本文探索了利用基于LLM的多智能体系统来自动优化PyTorch推理的方法。多个专门化智能体协同分析模型计算图、识别优化机会并生成优化的执行代码，自动化了PyTorch模型的推理性能调优过程。


---


## [Tiered Autonomy Framework for Human–Agent Collaboration in Mission-Critical Cyber-Physical Systems](https://mlsys.org/virtual/2026/poster/10194)


**英文摘要 (English Abstract)**:

Large Language Models (LLMs) are increasingly deployed as collaborating agents in Multi-Agent Systems (MAS), where sequential agent interactions create significant latency bottlenecks. Traditional serving systems require each downstream agent to wait for complete upstream generation before starting prefill, leaving substantial idle time during inter-agent transitions. We present FlashAgents, a system that accelerates multi-agent workflows through token-level streaming and prefix-aware coordination. FlashAgents introduces Inter-agent streaming and incremental prefill, which streams tokens between agents and performs incremental prefill to overlap downstream prefill with upstream decode, reducing inter-agent latency. For concurrent workloads, an intra-turn prefix cache built on radix trees detects and eliminates redundant prefill across requests sharing common instruction templates, avoiding recomputation of shared prefixes within the same processing turn. Implemented on SGLang, FlashAgents achieves up to 40% end-to-end latency reduction on real workflows and 3.5× speedup in controlled two-agent benchmarks, demonstrating consistent improvements across diverse models and interaction patterns.


**中文摘要**: [待翻译]


---


## [AccelOpt: A Self-Improving LLM Agentic System for AI Accelerator Kernel Optimization](https://mlsys.org/virtual/2026/poster/3585)


**英文摘要 (English Abstract)**:

We present AccelOpt, a self-improving large language model (LLM) agentic system that autonomously optimizes kernels for emerging AI accelerators, eliminating the need for expert-provided hardware-specific optimization knowledge. AccelOpt explores the kernel optimization space through iterative generation, informed by an optimization memory that curates experiences and insights from previously encountered slow-fast kernel pairs. We build NKIBench, a new benchmark suite of AWS Trainium accelerator kernels with varying complexity extracted from real-world LLM workloads to evaluate the effectiveness of AccelOpt. Our evaluation confirms that AccelOpt's capability improves over iterations, boosting the average percentage of peak throughput from 49% to 61% on Trainium 1 and from 45% to 59% on Trainium 2 for NKIBench kernels. Moreover, AccelOpt is highly cost-effective: using open-source models, it matches the kernel improvements of Claude Sonnet 4 while being 26× cheaper. The code is open-sourced at https://github.com/zhang677/AccelOpt.


**中文摘要**: [待翻译]


---


## [OSWorld-Human: Benchmarking the Efficiency of Computer-Use Agents](https://mlsys.org/virtual/2026/poster/3642)


**英文摘要 (English Abstract)**:

Generative AI is being leveraged to solve a variety of computer-use tasks involving desktop applications. State-of-the-art systems have focused solely on improving accuracy on leading benchmarks. However, these systems are practically unusable due to extremely high end-to-end latency (e.g. tens of minutes) for tasks that typically take humans just a few minutes to complete. To understand the cause behind this and to guide future developments of computer agents, we conduct the first study on the temporal performance of computer-use agents on OSWorld, the flagship benchmark in computer-use AI. We find that large model calls for planning, reflection, and judging account for most of the overall latency, and as an agent uses more steps to complete a task, each successive step can take 3× longer than steps at the beginning of a task. We then construct OSWorld-Human, a manually annotated version of the original OSWorld dataset that contains a human-determined trajectory for each task. We evaluate 16 agents on their efficiency using OSWorld-Human and found that even the best agents take 2.7−4.3× more steps than necessary.


**中文摘要**: [待翻译]


---


## [The OpenHands Software Agent SDK: A Composable and Extensible Foundation for Production Agents](https://mlsys.org/virtual/2026/poster/3526)


**英文摘要 (English Abstract)**:

Agents are now used widely in the process of software development, but building production-ready software engineering agents is a complex task. Deploying software agents effectively requires flexibility in implementation and experimentation, reliable and secure execution, and interfaces for users to interact with agents. In this paper, we present the OpenHands Software Agent SDK, a toolkit for implementing software development agents that satisfy these desiderata. This toolkit is a complete architectural redesign of the agent components of the popular OpenHands framework for software development agents. To achieve flexibility, we design a simple interface for implementing agents that requires only a few lines of code in the default case, but is easily extensible to more complex full-featured agents with features such as custom tools, memory management, and more. For security and reliability, it delivers seamless local-to-remote execution portability, integrated REST/WebSocket services. For interaction with human users, it can connect directly to a variety of interfaces, such as visual workspaces (VS Code, VNC, browser), command-line interfaces, and APIs. Compared with existing SDKs from OpenAI, Claude and Google, OpenHands uniquely integrates native sandboxed execution, lifecycle control, model-agnostic multi-LLM routing, and built-in security analysis. We validate the architecture empirically: production deployment data shows that V1 substantially reduces system-attributable failures over V0 with negligible event-sourcing overhead, and evaluations across multiple models and benchmarks demonstrate strong agent performance. Put together, these elements allow the OpenHands Software Agent SDK to provide a practical foundation for prototyping, unlocking new classes of custom applications, and reliably deploying agents at scale.


**中文摘要**:

智能体现已广泛应用于软件开发过程，但构建生产就绪的软件工程智能体是一项复杂任务。我们提出OpenHands软件智能体SDK，一个完整的架构重新设计。为实现灵活性，设计了仅需几行代码的简单接口，并可轻松扩展到全功能智能体。在安全性和可靠性方面，提供无缝的本地到远程执行可移植性和集成REST/WebSocket服务。与OpenAI、Claude和Google的现有SDK相比，OpenHands独特地集成了原生沙箱执行、生命周期控制、模型无关的多LLM路由和内置安全分析。生产部署数据表明V1大幅减少了系统归因故障，跨多模型和基准测试的评估展现出强大的智能体性能。


---


## [FlashAgents: Accelerating Multi-Agent LLM Systems via Streaming Prefill Overlap](https://mlsys.org/virtual/2026/poster/3537)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


# Attention & Kernel 优化（14 篇）


## [Event Tensor: A Unified Abstraction for Compiling Dynamic Megakernel](https://mlsys.org/virtual/2026/poster/3592)


**英文摘要 (English Abstract)**:

Modern GPU workloads, especially large language model (LLM) inference, suffer from kernel launch overheads and coarse synchronization that limit inter-kernel parallelism. Recent megakernel techniques fuse multiple operators into a single persistent kernel to eliminate launch gaps and expose inter-kernel parallelism, but struggle to handle dynamic shapes and data-dependent computation in real workloads. We present Event Tensor, a unified compiler abstraction for dynamic megakernels. Event Tensor encodes dependencies between tiled tasks, and enables first-class support for both shape and data-dependent dynamism. Built atop this abstraction, our Event Tensor Compiler (ETC) applies static and dynamic scheduling transformations to generate high-performance persistent kernels. Evaluations show that ETC achieves state-of-the-art LLM serving latency while significantly reducing system warmup overhead.


**中文摘要**:

现代GPU工作负载，尤其是大语言模型推理，受到内核启动开销和粗粒度同步的影响，限制了内核间并行性。最近的大内核技术将多个算子融合为单个持久内核，以消除启动间隙并暴露内核间并行性，但在处理真实工作负载中的动态形状和数据依赖计算方面存在困难。我们提出Event Tensor，一个用于动态大内核的统一编译器抽象。Event Tensor编码分块任务之间的依赖关系，并为形状动态性和数据依赖动态性提供一等支持。基于这一抽象，我们的Event Tensor编译器应用静态和动态调度转换来生成高性能持久内核。评估表明，ETC在实现最先进的LLM服务延迟的同时，显著降低了系统预热开销。


---


## [Hawkeye: Reproducing GPU-Level Non-Determinism](https://mlsys.org/virtual/2026/poster/3606)


**英文摘要 (English Abstract)**:

We present Hawkeye, a system for analyzing and reproducing GPU-level arithmetic operations. Using our framework, anyone can re-execute on a CPU the exact matrix multiplication operations underlying a machine learning model training or inference workflow that was executed on an NVIDIA GPU, without any precision loss. This is in stark contrast to prior approaches to verifiable machine learning, which either introduce significant computation overhead to the original model owner, or suffer from non-robustness and quality degradation. The main technical contribution of Hawkeye is a systematic sequence of carefully crafted tests that study rounding direction, subnormal number handling, and order of (non-associative) accumulation during matrix multiplication on NVIDIA's Tensor Cores. We test and evaluate our framework on multiple NVIDIA GPU architectures (Ampere, Hopper, and Lovelace) and precision types (FP16, BFP16, FP8). In all test cases, Hawkeye enables perfect reproduction of matrix multiplication on a CPU, paving the way for efficient and trustworthy third-party auditing of ML model training and inference.


**中文摘要**:

我们提出Hawkeye，一个用于分析和重现GPU级算术运算的系统。使用我们的框架，任何人都可以在CPU上精确重新执行在NVIDIA GPU上运行的机器学习模型训练或推理工作流中的矩阵乘法运算，且没有任何精度损失。这与先前的可验证机器学习方法形成鲜明对比，那些方法要么给原始模型所有者带来显著的计算开销，要么存在鲁棒性不足和质量下降的问题。Hawkeye的主要技术贡献是一系列系统性的精心设计的测试，研究NVIDIA Tensor Core上矩阵乘法中的舍入方向、次正规数处理以及累加顺序。我们在多种NVIDIA GPU架构和精度类型上测试和评估了我们的框架。在所有测试案例中，Hawkeye都能在CPU上完美重现矩阵乘法，为高效且可信的ML模型训练和推理第三方审计铺平了道路。源代码见 https://github.com/badasherez/gpu-simulator。


---


## [FlashInfer-Bench: Building the Virtuous Cycle for AI-driven LLM Systems](https://mlsys.org/virtual/2026/poster/3609)


**英文摘要 (English Abstract)**:

Recent advances show that large language models (LLMs) can act as autonomous agents capable of generating GPU kernels, but integrating these AI-generated kernels into real-world inference systems remains challenging. FlashInfer-Bench addresses this gap by establishing a standardized, closed-loop framework that connects kernel generation, benchmarking, and deployment. At its core, FlashInfer Trace provides a unified schema describing kernel definitions, workloads, implementations, and evaluations, enabling consistent communication between agents and systems. Built on real serving traces, FlashInfer-Bench includes a curated dataset, a robust correctness- and performance-aware benchmarking framework, a public leaderboard to track LLM agents' GPU programming capabilities, and a dynamic substitution mechanism (apply()) that seamlessly injects the best-performing kernels into production LLM engines such as SGLang and vLLM. Using FlashInfer-Bench, we further evaluate the performance and limitations of LLM agents, compare the trade-offs among different GPU programming languages, and provide insights for future agent design. FlashInfer-Bench thus establishes a practical, reproducible pathway for continuously improving AI-generated kernels and deploying them safely into large-scale LLM inference systems.


**中文摘要**:

最新进展表明，大语言模型（LLM）可以作为自主智能体生成GPU内核，但将这些AI生成的内核集成到实际推理系统中仍然具有挑战性。FlashInfer-Bench通过建立一个标准化的闭环框架来填补这一空白，该框架将内核生成、基准测试和部署连接起来。其核心是FlashInfer Trace，它提供了一个统一的模式来描述内核定义、工作负载、实现和评估，使智能体和系统之间能够进行一致的通信。基于真实服务追踪，FlashInfer-Bench包含一个精选数据集、一个鲁棒的兼顾正确性和性能的基准测试框架、一个跟踪LLM智能体GPU编程能力的公共排行榜，以及一个动态替换机制（apply()），能够将性能最佳的内核无缝注入到SGLang和vLLM等生产级LLM引擎中。利用FlashInfer-Bench，我们进一步评估了LLM智能体的性能和局限性，比较了不同GPU编程语言之间的权衡，并为未来的智能体设计提供了见解。FlashInfer-Bench因此建立了一条实用、可复现的路径，用于持续改进AI生成的内核并将其安全部署到大规模LLM推理系统中。


---


## [HipKittens: Fast and Furious AMD Kernels](https://mlsys.org/virtual/2026/poster/3512)


**英文摘要 (English Abstract)**:

The adoption of long context windows has become a standard feature in Large Language Models (LLMs), as extended contexts significantly enhance their capacity for complex reasoning and broaden their applicability across diverse scenarios. Dynamic sparse attention is a promising approach for reducing the computational cost of long-context training. However, efficiently training LLMs with dynamic sparse attention on ultra-long contexts, especially in distributed settings, remains a significant challenge, largely due to worker- and step-level imbalance. This paper introduces MTraining, a novel distributed methodology leveraging dynamic sparse attention to enable efficient training for LLMs with ultra-long contexts. Specifically, MTraining integrates three key components: a distributed sparse index approximating algorithm, balanced sparse ring attention, and hierarchical sparse ring attention. These components are designed to synergistically address the computational imbalance and communication overheads inherent in dynamic sparse attention mechanisms during training LLMs with extensive context lengths. We demonstrate the efficacy of MTraining mainly by training Qwen2.5-3B and Llama-3.1-8B, successfully expanding its context window from 32K/128K to 512K tokens on a cluster of 32× A100 GPUs. Our evaluations on a comprehensive suite of downstream tasks, including RULER, PG-19, InfiniteBench, and NIAH, reveal that MTraining achieves up to a 6x higher training throughput while preserving model accuracy. The core code is available at https://github.com/microsoft/MInference/tree/main/mtraining.


**中文摘要**:

AMD GPU架构在ML工作负载中展现出强大的计算能力，但现有内核库通常为NVIDIA GPU优化。HipKittens是一套专门为AMD GPU设计的高性能内核库，充分利用了AMD GPU架构特性，包括矩阵核心和高速缓存层次。通过针对性的内存访问模式优化、指令调度和并行化策略，HipKittens在多种ML运算上实现了与NVIDIA GPU上主流内核库相当甚至更优的性能。


---


## [ParallelKittens: Systematic and Practical Simplification of Multi-GPU AI Kernels](https://mlsys.org/virtual/2026/poster/3622)


**英文摘要 (English Abstract)**:

Diffusion language models hold the promise of fast parallel generation, while autoregressive (AR) models typically excel in quality due to their causal structure aligning naturally with language modeling. This raises a fundamental question: can we achieve a synergy with high throughput, higher GPU utilization, and AR level quality? Existing methods fail to effectively balance these two aspects, either prioritizing AR using a weaker model for sequential drafting (speculative decoding), leading to lower drafting efficiency, or using some form of left-to-right (AR-like) decoding logic for diffusion, which still suffers from quality degradation and forfeits its potential parallelizability. We introduce TIDAR, a sequence-level hybrid architecture that drafts tokens (Thinking) in Diffusion and samples final outputs (Talking) AutoRegressively — all within a single forward pass using specially designed structured attention masks. This design exploits the free compute density on GPUs, achieving a strong balance between drafting and verification capacity. Moreover, we design TIDAR to be serving-friendly as a standalone model. We extensively evaluate TIDAR against AR models, speculative decoding, and diffusion variants across generative and likelihood tasks at both 1.5B and 8B scales. Thanks to parallel drafting and sampling as well as efficient exact KV cache support, TIDAR outperforms speculative decoding in measured throughput and surpasses diffusion models like Dream and Llada in both efficiency and quality. Most notably, TIDAR is the first architecture to close the quality gap with AR models while delivering 4.71× to 5.91× more tokens per second.


**中文摘要**:

多GPU AI内核的开发涉及复杂的分片、同步和通信管理，编写难度大且容易出错。ParallelKittens提出了一套系统化简化多GPU AI内核的方法和工具，通过自动化分片和通信管理将复杂的多GPU内核开发简化为直观的编程模式，显著降低了分布式内核的开发门槛，同时保持了接近手工优化的性能水平。


---


## [BLASST: Dynamic BLocked Attention Sparsity via Softmax Thresholding](https://mlsys.org/virtual/2026/poster/3631)


**英文摘要 (English Abstract)**:

Retrieval-augmented generation (RAG) enables LLMs to ground responses in external knowledge, but long-term, multi-session conversations still suffer from implicit recall failures: when current user queries lack lexical overlap with earlier facts (e.g., preferences), standard dense retrieval and long-context prompting often miss the most relevant memories. We present a dialogue-aware RAG system that jointly addresses what to store and how to retrieve under constraints. Our design extracts durable user facts into a lightweight memory graph, enriches queries with conversational cues, performs hybrid retrieval, and uses a budget-aware router to balance quality and serving cost. On our Implicit Preference Recall benchmark, the system lifts Recall@10 to 0.70 (vs. 0.58 for dense-only) and improves nDCG@10 from 0.41 to 0.51. The system also reduces cross-modality disagreement by 47% and achieves a 81% cost reduction compared to long-context methods.


**中文摘要**:

长序列推理中的注意力计算开销随序列长度二次增长。BLASST提出了一种基于softmax阈值的动态分块注意力稀疏方法。通过在计算过程中动态识别和跳过注意力分数低于阈值的块，BLASST在不影响模型质量的前提下大幅减少了注意力计算量。该方法特别适用于长序列推理场景，实现了显著的加速和内存节省。


---


## [Flashlight: PyTorch Compiler Extensions to Accelerate Attention Variants](https://mlsys.org/virtual/2026/poster/3540)


**英文摘要 (English Abstract)**:

Serverless computing is an attractive paradigm for cloud-based large language model (LLM) inference, but scaling LLMs on demand remains a major challenge due to high data transfer cost. We present FaaScale, a serverless LLM system that enables fast and resource-efficient model scaling. The key idea is a co-design principle—pipelined multicast inference—which synergizes multicast with dynamic, cross-node pipeline-parallel execution during model transfer. FaaScale implements this design through PipeCast, a model scaling scheme that adaptively multicasts model blocks and dynamically forms inference pipelines on the fly. Coupled with efficient memory management across GPU and host memory, FaaScale handles bursty LLM inference workloads effectively, achieving up to 5× lower tail time-to-first-token latency and 31.3% cost reduction on real-world LLM traces.


**中文摘要**:

注意力机制的变体日益增多，但PyTorch编译器对这些变体的支持有限。Flashlight是PyTorch编译器的一组扩展，专门用于加速各种注意力变体。它通过自动识别注意力模式并高效映射到底层硬件，实现了跨模型架构的统一加速，同时保持与PyTorch生态系统的完全兼容。


---


## [db-SP: Accelerating Sparse Attention for Visual Generative Models with Dual-Balanced Sequence Parallelism](https://mlsys.org/virtual/2026/poster/3575)


**英文摘要 (English Abstract)**:

Scaling Diffusion Transformer (DiT) inference via sequence parallelism is critical for reducing latency in visual generation, but is severely hampered by workload imbalance when applied to models employing block-wise sparse attention. The imbalance stems from the inherent variation in sparsity across attention heads and the irregular distribution of dense blocks within the sparse mask, when sequence parallelism is applied along the head dimension (as in Ulysses) or the block dimension (as in Ring Attention). In this paper, we formalize a sparse imbalance ratio to quantify the imbalance, and propose db-SP, a sparsity-aware sequence parallelism technique that tackles the challenge. db-SP contains a dual-level partitioning approach that achieves near-perfect workload balance at both the head and block levels with negligible overhead. Furthermore, to handle the evolving sparsity patterns across denoising steps and layers, db-SP dynamically determines the parallel degrees for the head and block dimensions at runtime. Experimental results demonstrate that db-SP delivers an end-to-end speedup of 1.25× and an attention-specific speedup of 1.40× over state-of-the-art sequence parallel methods on average.


**中文摘要**: [待翻译]


---


## [CATWILD: Compiler Autotuning for TPU workloads in the Wild](https://mlsys.org/virtual/2026/poster/3551)


**英文摘要 (English Abstract)**:

Large Language Models (LLMs) are central to modern NLP applications, yet their deployment on consumer-grade GPUs is limited by limited memory capacity and bandwidth. In typical single-batch inference on local devices, the key–value (KV) cache occupies only a small fraction of total memory, so prior studies have largely focused on model weights. The rise of test-time compute (TTC), however, introduces a new bottleneck: the rapidly expanding KV cache. In TTC methods such as step-wise beam search, concurrent decoding paths cause KV cache size and transfer costs to scale with exploration space, resulting in severe I/O stalls on consumer-grade GPUs. We identify two complementary forms of data locality in TTC workloads. Inter-token locality occurs within each decoding step, as consecutive tokens in the same beam access nearly identical KV cache data. Inter-beam locality arises across decoding steps, as beams that share common prefixes reuse overlapping KV segments. Building on these observations, we propose Locality-Aware Beam Scheduling, which exploits these locality patterns to reduce redundant KV cache transfers. It also employs balanced grouping with prefetching to overlap data movement with computation. Evaluated on OPT-6.7B, LLaMA-2-7B, and Qwen-7B, our method reduces KV cache transfer volume by over 95% and achieves consistent end-to-end speedups of 3.39×–9.72×, 3.60×–8.74×, and 4.17×–7.99×, respectively, compared to layer-wise offloading.


**中文摘要**:

TPU编译器选项的调优对模型执行效率有显著影响，但手动搜索最优配置非常耗时。CATWILD是一个针对TPU工作负载的编译器自动调优工具，在实际生产环境中自动搜索最优编译选项组合，无需人工干预即可为各种ML模型找到高效的编译配置。


---


## [SwiftGS: Algorithm and System Co-Optimization for Fast 3D Gaussian Splatting on GPUs](https://mlsys.org/virtual/2026/poster/3550)


**英文摘要 (English Abstract)**:

Large Language Models (LLMs) are increasingly deployed as collaborating agents in Multi-Agent Systems (MAS), where sequential agent interactions create significant latency bottlenecks. Traditional serving systems require each downstream agent to wait for complete upstream generation before starting prefill, leaving substantial idle time during inter-agent transitions. We present FlashAgents, a system that accelerates multi-agent workflows through token-level streaming and prefix-aware coordination. FlashAgents introduces Inter-agent streaming and incremental prefill, which streams tokens between agents and performs incremental prefill to overlap downstream prefill with upstream decode, reducing inter-agent latency. For concurrent workloads, an intra-turn prefix cache built on radix trees detects and eliminates redundant prefill across requests sharing common instruction templates, avoiding recomputation of shared prefixes within the same processing turn. Implemented on SGLang, FlashAgents achieves up to 40% end-to-end latency reduction on real workflows and 3.5× speedup in controlled two-agent benchmarks, demonstrating consistent improvements across diverse models and interaction patterns.


**中文摘要**:

3D高斯溅射在场景重建和新视角合成方面展现了卓越质量，但训练和渲染速度仍有提升空间。SwiftGS通过算法和系统协同优化实现了GPU上的快速3D高斯溅射。结合高效的并行渲染算法和GPU友好的数据结构，在保持渲染质量的同时大幅提升了训练和推理速度。


---


## [MAC-Attention: a Match–Amend–Complete scheme for fast and accurate attention computation](https://mlsys.org/virtual/2026/poster/3571)


**英文摘要 (English Abstract)**:

Long-context decoding in LLMs is IO-bound: each token re-reads an ever-growing KV cache. Prior accelerations cut bytes via compression (lowering fidelity) or selection/eviction (restricting what remains accessible), which can degrade delayed recall and long-form generation. We introduce MAC-Attention, a fidelity and access-preserving alternative that accelerates decode by reusing prior attention computations for semantically similar recent queries. It starts with a match stage that performs pre-RoPE L2 matching over a short local window; an amend stage rectifies the reused attention by recomputing a small band near the match boundary; and a complete stage fuses the rectified results with a fresh attention computed on the KV tail, via a numerically stable merge. On a match hit, the compute and bandwidth complexity is constant regardless of the context length. The method is model-agnostic, and composes with IO-aware kernels, paged-KV managers, and MQA/GQA. Across LongBench v2 (120K), RULER (120K), and LongGenBench (16K continuous generation), MAC-Attention reduces KV accesses by up to 99%, cuts token generation latency by over 60% at 128K, and achieves over 14.3x attention-phase speedups (up to 2.6x end-to-end), while maintaining full-attention quality. By reusing computation rather than compressing or discarding tokens, MAC-Attention delivers long-context inference that is both fast and faithful. Code is available.


**中文摘要**:

LLM中的长上下文解码受IO限制：每个token需要重新读取不断增长的KV缓存。先前的加速方法通过压缩（降低保真度）或选择/驱逐（限制可访问内容）来减少字节数，这可能降低延迟召回和长文本生成的质量。我们提出了MAC-Attention，一种保真度和访问保持的替代方案，通过为语义相似的近期查询重用先前的注意力计算来加速解码。它从匹配阶段开始，在短局部窗口内执行pre-RoPE L2匹配；修正阶段通过在匹配边界附近重新计算小范围来修正重用的注意力；完成阶段通过数值稳定的合并，将修正结果与KV尾部计算的新注意力融合。在匹配命中时，计算和带宽复杂度与上下文长度无关，为常数级别。该方法与模型无关，可与IO感知内核、分页KV管理器和MQA/GQA组合使用。在LongBench v2、RULER和LongGenBench上，MAC-Attention将KV访问减少了高达99%，在128K时将token生成延迟降低了超过60%，实现了超过14.3倍的注意力阶段加速（端到端高达2.6倍），同时保持了全注意力质量。通过重用计算而非压缩或丢弃token，MAC-Attention提供了既快速又保真的长上下文推理。


---


## [From 805 ms to 23 ms: Accelerating State-Space Models for Real-Time ICU Monitoring with Fused Triton Kernels](https://mlsys.org/virtual/2026/poster/10197)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**:

状态空间模型在医疗时序数据上展现出潜力，但推理速度限制了实时应用。本文通过融合Triton内核将状态空间模型的执行从805毫秒加速到23毫秒，实现35倍加速用于ICU实时监控。通过针对医疗时间序列数据特点优化的定制内核，使大模型能够在生命攸关的实时医疗场景中部署。


---


## [FlashAttention-4: Algorithm and Kernel Pipelining Co-Design for Asymmetric Hardware Scaling](https://mlsys.org/virtual/2026/poster/3536)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**:

FlashAttention系列持续推动注意力计算效率的提升。FlashAttention-4通过算法和内核流水线协同设计实现对非对称硬件扩展的优化，专门针对Blackwell等新一代GPU架构中计算和内存带宽的非对称增长进行优化，在保持数值精度的同时实现了更高效的注意力计算。


---


## [Dataflow Is All You Need](https://mlsys.org/virtual/2026/poster/3629)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


# 模型压缩与量化（5 篇）


## [Attribution-based Sparse Activation in Large Language Models](https://mlsys.org/virtual/2026/poster/3556)


**英文摘要 (English Abstract)**:

Emerging Large Language Model (LLM) system patterns, such as disaggregated inference, Mixture-of-Experts (MoE) routing, and asynchronous reinforcement fine-tuning, require flexible point-to-point communication beyond simple collectives. Existing implementations are locked to specific Network Interface Controllers (NICs), hindering integration into inference engines and portability across hardware providers. We present fabric-lib, which bridges the functionality of common NICs to expose a uniform interface. fabric-lib exposes one-sided WriteImm operations with a ImmCounter primitive for completion notification, without ordering assumptions of network transport, transparently managing multiple NICs per GPU. We demonstrate peak throughput of 400 Gbps on both NVIDIA ConnectX-7 and AWS Elastic Fabric Adapter (EFA). We showcase fabric-lib through three production systems: (1) KvCache transfer for disaggregated inference with dynamic scaling, (2) RL weight updates achieving 1.3 seconds for trillion-parameter models, and (3) MoE dispatch/combine implementation exceeding DeepEP decode latency on ConnectX-7, with the first viable latencies on EFA. We demonstrate that our portable point-to-point communication complements collectives while avoiding lock-in. fabric-lib is open-sourced at https://github.com/perplexityai/pplx-garden/.


**中文摘要**:

基于归因的稀疏激活利用归因分数识别大语言模型中每个token最重要的神经元。通过仅激活对当前输入贡献最大的神经元路径，跳过贡献度低的计算，该方法在不进行任何微调的情况下实现了高效的推理加速，同时保持了模型的完整表达能力。在多种LLM架构上的实验验证了该方法的有效性。


---


## [IntAttention: A Fully Integer Attention Pipeline for Efficient Edge Inference](https://mlsys.org/virtual/2026/poster/3625)


**英文摘要 (English Abstract)**:

Deploying Transformer models on edge devices is limited by latency and energy budgets. While INT8 quantization effectively accelerates the primary matrix multiplications, it exposes the softmax-related path as the dominant bottleneck. This stage incurs a costly dequantize -> softmax -> requantize detour, which can account for up to 65% of total attention latency and disrupts the end-to-end integer dataflow critical for edge hardware efficiency. To address this limitation, we present IntAttention, the first fully integer attention pipeline that serves as a training-free drop-in replacement. At the core of our approach lies IndexSoftmax, a hardware-friendly operator that replaces floating-point exponentials entirely within the integer domain. IntAttention integrates sparsity-aware clipping, a 32-entry lookup table approximation, and direct integer normalization, thereby eliminating datatype conversion overhead along the attention path. Experiments on Armv8 CPUs show that our method achieves up to 3.7x speedup and 61% energy reduction over FP16 baselines, and up to 2.0x speedup over conventional INT8 attention pipelines. Across diverse language and vision models, as well as additional reasoning and long-context evaluations, IntAttention maintains strong overall fidelity and demonstrates a more favorable trade-off than existing LUT-based softmax approximations. Code is available at: https://github.com/WanliZhong/IntAttention


**中文摘要**:

Transformer模型在边缘设备上的部署受到延迟和能耗预算限制。虽然INT8量化有效加速了主要矩阵乘法，但它使softmax相关路径成为主导瓶颈，可能占据注意力总延迟的65%。我们提出IntAttention，首个完全整数注意力流水线，核心是IndexSoftmax——一种在整数域内替代浮点指数的硬件友好算子。在Armv8 CPU上实现高达3.7倍加速和61%能耗降低，同时保持强大的整体保真度。代码见 https://github.com/WanliZhong/IntAttention。


---


## [CAGE: Curvature-Aware Gradient Estimation For Accurate Quantization-Aware Training](https://mlsys.org/virtual/2026/poster/3618)


**英文摘要 (English Abstract)**:

Despite significant work on low-bit quantization-aware training (QAT), there is still an accuracy gap between such techniques and native training. To address this, we introduce CAGE (Curvature-Aware Gradient Estimation), a new QAT method that augments the straight-through estimator (STE) gradient with a curvature-aware correction designed to counteract the loss increase induced by quantization. CAGE is derived from a multi-objective view of QAT that balances loss minimization with adherence to quantization constraints, yielding a principled correction term that depends on local curvature information. On the theoretical side, we introduce the notion of Pareto-optimal solutions for quantized optimization, and establish that CAGE yields strong convergence guarantees in the smooth non-convex setting. In terms of implementation, our approach is optimizer-agnostic, but we provide a highly-efficient implementation that leverages Adam statistics. CAGE significantly improves upon the prior state-of-the-art methods in terms of accuracy, for similar computational cost: for QAT fine-tuning, it halves the compression accuracy loss relative to the prior best method, while for QAT pre-training of Llama models, its accuracy for 3-bit weights-and-activations (W3A3) matches that of 4-bit training (W4A4) with the prior best method (QuEST).


**中文摘要**:

尽管在低位量化感知训练方面已有大量工作，但QAT与原生训练之间仍存在精度差距。我们引入CAGE，一种通过曲率感知校正增强直通估计器梯度的新QAT方法。CAGE源自QAT的多目标视角，在损失最小化与遵守量化约束之间取得平衡。我们引入量化优化帕累托最优解概念，并证明CAGE在光滑非凸环境中具有强大收敛保证。在类似计算成本下，CAGE将QAT微调的压缩精度损失相比先前最佳方法减半；对于Llama模型的3位权重和激活QAT预训练，其精度与先前最佳方法的4位训练相当。


---


## [Search Your Block Floating Point Scales!](https://mlsys.org/virtual/2026/poster/3547)


**英文摘要 (English Abstract)**:

Blocking communication presents a major hurdle in running MoEs efficiently in distributed settings. To address this, we present FarSkip-Collective which modifies the architecture of modern models to enable overlapping of their computation with communication. Our approach modifies the architecture to skip connections in the model and it is unclear a priori whether the modified model architecture can remain as capable, especially for large state-of-the-art models and while modifying all of the model layers. We answer this question in the affirmative and fully convert a series of state-of-the-art models varying from 16B to 109B parameters to enable overlapping of their communication while achieving accuracy that is comparable with their original open-source releases. For example, we convert Llama 4 Scout (109B) via self-distillation and achieve average accuracy within 1% of its instruction tuned release averaged over a wide range of downstream evaluations. In addition to demonstrating retained accuracy of the large modified models, we realize the benefits of FarSkip-Collective through optimized implementations that explicitly overlap communication with computation, accelerating both training and inference in existing frameworks. For inference, we demonstrate 32.6% speedup in Time To First Token when serving a converted DeepSeek-V3 architecture with expert parallelism in SGLang and achieve 97.3% communication-computation overlap during the prefill stage. During training, our approach enables 88.9% communication overlap of the all-to-all communication collectives when pre-training DeepSeek-V3 MoE layers with expert parallelism.


**中文摘要**: [待翻译]


---


## [Once-for-All Channel Mixers (HyperTinyPW): Generative Compression for TinyML](https://mlsys.org/virtual/2026/poster/3595)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


# 硬件与基础设施（29 篇）


## [Unified LLM Model for Power, Performance, and Area Prediction from Hardware Code](https://mlsys.org/virtual/2026/poster/3538)


**英文摘要 (English Abstract)**:

We present RocketPPA, a unified LLM-based model that predicts power, performance, and area for Verilog designs across technology nodes and optimization styles. The approach combines a large language model backbone with mixture-of-experts regression and low-rank adaptation for parameter efficiency. To improve generalization, we introduce a contrastive learning framework that encourages semantically similar designs to cluster in embedding space, providing an inductive bias that reflects the structure of the hardware design space. Trained on 15nm and 45nm nodes with area- and delay-optimized flows, the model achieves 9.4 percentage point improvement in pass rate at ten percent tolerance over prior methods, with approximately 20× higher throughput (0.12 seconds per design). Ablations show contrastive learning contributes 2.5 points to accuracy, while leave-one-regime-out experiments demonstrate robust cross-regime generalization with minimal degradation. These results validate that combining supervised and contrastive objectives enables rapid, accurate PPA prediction across nodes and optimization styles.


**中文摘要**:

我们提出RocketPPA，一个基于统一LLM的模型，用于跨工艺节点和优化风格预测Verilog设计的功耗、性能和面积。该方法将大语言模型主干与专家混合回归和低秩适配相结合，以实现参数效率。为提高泛化能力，我们引入了一个对比学习框架，促使语义相似的设计在嵌入空间中聚类，提供了一种反映硬件设计空间结构的归纳偏置。在15nm和45nm节点上使用面积和延迟优化流程进行训练后，该模型在10%容差下的通过率比先前方法提高了9.4个百分点，吞吐量提高了约20倍（每个设计0.12秒）。消融实验表明对比学习对准确率贡献了2.5个百分点，而留一区域实验展示了鲁棒的跨区域泛化能力，性能退化极小。这些结果验证了将监督目标和对比目标相结合能够实现跨节点和优化风格的快速、准确PPA预测。


---


## [MLCommons Chakra: Advancing Performance Benchmarking and Co-design using Standardized Execution Traces](https://mlsys.org/virtual/2026/poster/3519)


**英文摘要 (English Abstract)**:

The fast pace of artificial intelligence (AI) innovation demands an agile methodology for observation, reproduction and optimization of distributed machine learning (ML) workload behavior in production AI systems and enables efficient software-hardware (SW-HW) co-design for future systems. We present Chakra, an open and portable ecosystem for performance benchmarking and co-design. The core component of Chakra is an open and interoperable graph-based representation of distributed AI/ML workloads, called Chakra execution trace (ET). Chakra has been adopted by MLCommons and has active contributions across the industry including NVIDIA, AMD, Meta, Keysight, HPE, and Scala.


**中文摘要**:

人工智能创新的快节奏要求一种敏捷的方法来观察、复现和优化生产AI系统中的分布式机器学习工作负载行为，并实现高效的软硬件协同设计。我们提出Chakra，一个开放且可移植的性能基准测试和协同设计生态系统。Chakra的核心组件是Chakra执行追踪——一种开放且可互操作的分布式AI/ML工作负载图表示。这些ETs表示关键操作，如计算、内存和通信，数据和控制的依赖关系，时序以及资源约束。此外，Chakra包含一套互补的工具和能力，使广泛的仿真器、模拟器和重放工具能够收集、分析、生成和采纳Chakra ETs。我们展示了对生产AI集群上收集的Chakra ETs的分析，并通过真实世界案例研究证明其价值。Chakra已被MLCommons采纳，并在业界有积极贡献和参与，包括但不限于NVIDIA、AMD、Meta、Keysight、HPE和Scala。


---


## [Neuro-Analog](https://mlsys.org/virtual/2026/poster/10192)


**英文摘要 (English Abstract)**:

Length-Aware Prefill Serving (LAPS) identifies and disaggregates requests with different prompt lengths in LLM serving to reduce TTFT latency. While recent systems have decoupled the prefill and decode stages to improve throughput, they still rely on unified scheduling policies that fail to adapt to heterogeneous workload characteristics. We observe that prompt-length variations lead to distinct performance bottlenecks, motivating an adaptive scheduling strategy. LAPS disaggregates multi-turn long-prefill requests from short-prefill ones and introduces a length-aware smart batching mechanism for short-prefill workloads. It adopts a dual-queue design that supports temporal disaggregation on a single prefill instance or spatial disaggregation across multiple instances. For short-prefill batches, a batch waiting window and CUDA Graph-based clustering mitigate interference from heterogeneous computation, reducing batching delay and lowering average latency. In real multi-turn workloads, LAPS reduces prefill latency by over 30% compared to vanilla SGLang under prefill–decode disaggregation, and further decreases SLO violations by 28% in multi-instance deployments with vanilla data-parallel configuration. Compared to the SGLang router with load balancing, it further lowers SLO violations by 12% in multi-GPU settings. Under high concurrency and mixed-request scenarios, LAPS improves request throughput by 35% serving Qwen2.5-32B model for prefill instance, demonstrating its effectiveness in optimizing heterogeneous LLM serving workloads.


**中文摘要**: [待翻译]


---


## [Wave: A Symbolic Python DSL And Compiler for High-Performance Machine Learning](https://mlsys.org/virtual/2026/poster/3555)


**英文摘要 (English Abstract)**:

Fully Sharded Data Parallel (FSDP), also known as Zero Redundancy Optimizer (ZeRO), is widely used for large-scale model training, because of its memory efficiency and minimal intrusion on model code. However, existing FSDP systems rely on fixed element-wise or row-wise sharding formats that conflict with block-structured computations. As a result, they struggle to support modern structure-aware training methods, including block-wise quantization and non-element-wise optimizers such as Shampoo and Muon. In addition, today's implementations incur communication and memory overheads that degrade efficiency at the scale of tens of thousands of GPUs. We introduce veScale-FSDP, a novel FSDP system that combines RaggedShard, a flexible sharding format, with a structure-aware planning algorithm to deliver both flexibility and performance. veScale-FSDP enables zero-copy FSDP communications and natively supports block-wise quantization and non-element-wise optimizers, achieving 5% to 66% higher throughput and 16% to 30% lower memory usage than existing FSDP systems, while scaling efficiently to tens of thousands of GPUs.


**中文摘要**:

现代ML模型要求越来越高的算力，促使硬件供应商在其GPU中添加专门的矩阵核心。虽然这些单元解锁了高吞吐量，但它们强加了复杂的编程模型和寻址方案，手动管理非常困难。本文介绍Wave，一个嵌入Python的DSL用于内核编写，自动化这些复杂的地址计算，让开发者专注于核心计算。在实验中，它匹配或超越了最先进的内核DSL和库的性能。


---


## [A Lightweight High-Throughput Collective-Capable NoC for Large-Scale ML Accelerators](https://mlsys.org/virtual/2026/poster/3581)


**英文摘要 (English Abstract)**:

AMD GPUs offer state-of-the-art compute and memory bandwidth; however, peak performance AMD kernels are written in raw assembly. To address the difficulty of mapping AI algorithms to hardware, recent work proposes C++ embedded and PyTorch-inspired domain-specific languages like ThunderKittens (TK) to simplify high performance AI kernel development on NVIDIA hardware. We explore the extent to which such primitives — for explicit tile-based programming with optimized memory accesses and fine-grained asynchronous execution across workers — are NVIDIA-specific or general. We provide the first detailed study of the programming primitives that lead to performant AMD AI kernels, and we encapsulate these insights in the HipKittens (HK) programming framework. We find that tile-based abstractions used in prior DSLs generalize to AMD GPUs, however we need to rethink the algorithms that instantiate these abstractions for AMD. We validate the HK primitives across CDNA3 and CDNA4 AMD platforms. In evaluations, HK kernels compete with AMD's hand-optimized assembly kernels for GEMMs and attention, and consistently outperform compiler baselines. Moreover, assembly is difficult to scale to the breadth of AI workloads; reflecting this, in some settings HK outperforms all available baselines by 1.2−2.4× (d=64 attention, GQA non-causal backwards, memory-bound kernels). HK demonstrates a portable tile-based programming model that abstracts over hardware-specific implementation details. These findings help pave the way for a single, tile-based software layer for high-performance AI kernels across GPU vendors. HipKittens has been productionalized in AITER and is released at: https://github.com/HazyResearch/HipKittens.


**中文摘要**:

大规模机器学习加速器需要高效的片上网络来支持集合通信操作。本文提出了一种面向大规模ML加速器的轻量级高吞吐量集合通信NoC。通过优化的路由策略和专用的集合通信硬件支持，该NoC架构在保持低功耗和小面积的同时，为AllReduce等关键通信模式提供了接近线速的吞吐量，显著加速了分布式训练中的通信瓶颈。


---


## [Cost-aware Duration Prediction for Software Upgrades in Datacenters](https://mlsys.org/virtual/2026/poster/3542)


**英文摘要 (English Abstract)**:

Software upgrades are critical to maintaining server reliability in datacenters. This paper presents the first in-depth investigation into software upgrade scheduling at datacenter scale. We introduce Acela, a cost-aware duration prediction framework designed to improve upgrade scheduling efficiency and throughput while meeting service-level objectives (SLOs). Evaluations on Meta's production datacenter systems demonstrate that Acela significantly increases efficiency by improving upgrade window utilization by 1.25X.


**中文摘要**:

软件升级对维护数据中心服务器可靠性至关重要。虽然作业持续时间预测和调度已被广泛研究，但软件升级带来的独特挑战仍然很大程度上未被探索。本文首次深入研究了数据中心规模的软件升级调度。我们首先对各种类型的升级进行特征分析，然后将调度任务形式化为约束优化问题。为解决此问题，我们引入Acela，一个成本感知的持续时间预测框架，旨在提高升级调度效率和吞吐量，同时满足服务级别目标。Acela考虑了非对称误预测成本，策略性地选择最佳预测模型，并缓解慢节点引起的过高估计。在Meta生产数据中心系统上的评估表明，Acela通过将升级窗口利用率提高1.25倍、将计划和完成的升级数量增加33%和41%、并将取消率降低2.4倍，显著提升了现有升级调度器的效率。


---


## [Towards Efficient Systems for Long-Context Automatic Speech Recognition](https://mlsys.org/virtual/2026/poster/10195)


**英文摘要 (English Abstract)**:

Reasoning language models have demonstrated remarkable capabilities on challenging tasks by generating elaborate chain-of-thought (CoT) solutions. However, such lengthy generation shifts the inference bottleneck from compute-bound to memory-bound. To generate each token, the model applies full attention to all previously generated tokens, requiring memory access to an increasingly large KV-Cache. Consequently, longer generations demand more memory access for every step, leading to substantial pressure on memory bandwidth. To address this, we introduce SpecGen, a speculative decoding framework that reuses the same model as the draft and target models (i.e., self-speculation). SpecGen features a novel sparse attention mechanism PillarAttn as the draft model, which accurately selects critical tokens via elegantly reusing information from the verification stage. Furthermore, SpecGen co-designs self-speculation with three system innovations: (1) a unified scheduler to batch token drafting and verification, (2) delayed verification for CPU/GPU overlap, and (3) dynamic KV-Cache management to maximize memory utilization. Across various models and datasets, SpecGen outperforms state-of-the-art solutions, with an up to 2.13× throughput speedup.


**中文摘要**:

面向长上下文的自动语音识别需要高效处理长时间音频输入。本文提出了一个专为长上下文ASR设计的高效系统，通过创新的注意力机制和流式处理架构来解决超长音频转录中的计算和存储瓶颈。系统在处理长达数小时的音频时仍能保持低延迟和高准确率，适用于会议转录、讲座记录等实际应用场景。


---


## [Virtual Machine NUMA Placement at Scale: Learning the Norm, Shielding the Tail](https://mlsys.org/virtual/2026/poster/3554)


**英文摘要 (English Abstract)**:

As inference scales to multi-node deployments, prefill-decode disaggregation — splitting inference into distinct phases — offers a promising path to improving the throughput-interactivity Pareto frontier. Despite growing enthusiasm and a surge of open-source efforts, large-scale deployment of disaggregated serving remains limited due to the complexity of the optimization search space and system-level coordination. In this paper, we present the first systematic study of disaggregated inference at scale, evaluating hundreds of thousands of design points across diverse workloads and hardware configurations. We find that disaggregation is most effective for prefill-heavy traffic patterns and larger models. Our results highlight the critical role of dynamic rate matching and elastic scaling in achieving Pareto-optimal performance. These insights, in conjunction with the deployment flexibility offered by NVIDIA Dynamo, provide a foundation to navigate the trade-off between system throughput and interactivity in efficient disaggregated deployments.


**中文摘要**:

数据中心中虚拟机的NUMA放置对性能有显著影响。本文研究了大规模虚拟机NUMA放置问题，提出基于学习的方法自动优化数据中心中虚拟机的NUMA拓扑分配。通过学习历史放置决策和相应的性能数据，系统能够预测最优的NUMA配置，在遵循硬件和业务约束的同时最大化性能，同时有效处理尾部延迟问题。


---


## [Massive-Scale Out-Of-Core UMAP on the GPU](https://mlsys.org/virtual/2026/poster/3624)


**英文摘要 (English Abstract)**:

Existing MLLM inference systems are typically designed based on the architecture of language models, coupling image processing and language processing. This design struggles to accommodate the heterogeneous demands of different stages in terms of computational resources, memory access patterns, and service-level objectives (SLOs), leading to low resource utilization and high request latency, ultimately failing to meet the service requirements of diverse inference scenarios. To address these challenges, we propose TriInfer, an efficient MLLM inference system that adopts a Hybrid Encode-Prefill-Decode (EPD) Disaggregation architecture. By scheduling the three stages — encode, prefill, and decode — onto separate heterogeneous inference instances, the system flexibly reallocates resources across stages, significantly reducing idle computation, alleviating resource bottlenecks, and improving overall system throughput and scalability. In addition, TriInfer supports a stage-level batching strategy that enhances load balancing, enables parallel execution of visual and language models, and further optimizes inference performance. Experiments under real multimodal inference workloads demonstrate that TriInfer can achieve up to 3.7× higher inference throughput compared to state-of-the-art systems (e.g., vLLM, SGLang) while meeting the 90th percentile request SLO. The source code of TriInfer will be released at https://github.com/dongxianzhe/triinfer.


**中文摘要**:

UMAP是广泛使用的降维和可视化算法，但GPU版本受限于显存容量无法处理大规模数据集。本文提出了在GPU上实现大规模外存UMAP的算法和系统优化，通过将部分数据存储在CPU内存中并智能调度数据移动，突破显存限制。该方法支持处理远超GPU显存容量的数据集，同时保持了与内存内版本相当的运行速度。


---


## [Automated Algorithm Design for Auto-Tuning Optimizers](https://mlsys.org/virtual/2026/poster/3525)


**英文摘要 (English Abstract)**:

Agentic AI systems require persistent memory to store user-specific histories beyond the limited context window of LLMs. Existing memory systems rely on the dense vector databases, knowledge-graph traversal, or hybrids, which incur high retrieval latency and poor storage scalability. We introduce HIPPOCAMPUS, an agentic memory management system that uses compact binary signatures for semantic search and lossless token-ID streams for exact content reconstruction. Its core is a Dynamic Wavelet Matrix (DWM) that compresses and co-indexes both streams to support ultra-fast search in the compressed domain, thus avoiding costly dense-vector or graph computations. For a fixed tokenizer vocabulary, the storage footprint of this design grows linearly with memory size, making it suitable for long-horizon agentic deployments. Empirically, across LoCoMo and LongMemEval, HIPPOCAMPUS achieves end-to-end retrieval latency that is comparable to or lower than the evaluated agentic memory baselines, with 1.1X–31.5X speedups over the evaluated baselines, and reduces per-query token footprint by 1.1X–14.5X, while maintaining competitive task accuracy.


**中文摘要**:

优化器的超参数自动调优通常依赖网格搜索或贝叶斯优化等通用方法。本文提出了自动调优优化器的算法自动设计方法，将优化器设计空间参数化并使用自动搜索算法探索，能够自动发现针对特定工作负载和硬件配置的最优优化器配置，减少了对人工调参的依赖。


---


## [ov_training_kit : Model training and inference on local AI PC to strengthen the AI ecosystem](https://mlsys.org/virtual/2026/poster/10174)


**英文摘要 (English Abstract)**:

Meta's Large Language Models (LLMs)---the Llama model family---serve nearly one billion monthly active users. Deploying these models for inference involves navigating a complex design space that spans diverse hardware options (e.g., H100, H200, MI300X), multiple parallelism strategies (tensor, pipeline, expert, context, and data parallelism), and nuanced runtime choices (e.g., continuous batching versus prefill-decode disaggregation)---all while leveraging workload-specific characteristics and meeting stringent service level objectives (SLOs). This paper presents insights we gained from developing and applying a systematic approach to analyze millions of deployment configurations and identify those that maximize throughput while meeting latency SLOs. We share lessons learned from our experience operating Llama inference at scale, including trade-offs among runtime designs, the phase-specific nature of parallelism strategies, opportunities for leveraging hardware heterogeneity, platform scaling behaviors, and system-level implications of model architectures such as Mixture-of-Experts (MoE). We hope our production experience offers practical insights for the broader LLM inference community.


**中文摘要**: [待翻译]


---


## [Machine Learning Fleet Efficiency: Improving TPU Systems at Scale with ML Productivity Goodput](https://mlsys.org/virtual/2026/poster/3511)


**英文摘要 (English Abstract)**:

The pervasive "memory wall" bottleneck is significantly amplified in modern large-scale Mixture-of-Experts (MoE) architectures. MoE's inherent architectural sparsity leads to sparse arithmetic compute and also introduces substantial activation memory overheads—driven by large token routing buffers and the need to materialize and buffer intermediate tensors. This memory pressure limits the maximum batch size and sequence length that can fit on GPUs, and also results in excessive data movements that hinders performance and efficient model scaling. We present MoEBlaze, a memory-efficient MoE training framework that addresses these issues through a co-designed system approach: (i) an end-to-end token dispatch and MoE training method with optimized data structures to eliminate intermediate buffers and activation materializing, and (ii) co-designed kernels with smart activation checkpoint to mitigate memory footprint while simultaneously achieving better performance. We demonstrate that MoEBlaze can achieve over 4× speedups and over 50% memory savings compared to existing MoE frameworks. MoEBlaze has been deployed in Meta recommendation production.


**中文摘要**:

大规模TPU集群的利用效率对ML生产力有直接影响。本文介绍了机器学习集群效率优化方法，通过ML生产力良率指标来改进TPU系统的大规模运行效率。该指标综合考量了硬件利用率、任务完成率和资源浪费等多个维度，为大规模ML基础设施管理提供了数据驱动的决策依据。


---


## [DynaFlow: Transparent and Flexible Intra-Device Parallelism via Programmable Operator Scheduling](https://mlsys.org/virtual/2026/poster/3548)


**英文摘要 (English Abstract)**:

We propose DynaFlow, a framework that enables the transparent and flexible integration of intra-device parallelism by decoupling the logical model definition from the physical execution schedule. DynaFlow introduces a flexible frontend with annotations for graph partitioning and a programmable interface for defining custom intra-device parallelism strategies. We demonstrate that DynaFlow can integrate representative parallelism strategies into 6 state-of-the-art ML systems with minimal code changes, achieving up to a 1.29x throughput improvement.


**中文摘要**:

设备内并行性通过重叠不同资源使用的算子执行来解决ML推理和训练中的资源未充分利用问题。但其广泛应用受到与现有框架静态顺序编程模型的根本冲突的阻碍。我们提出DynaFlow，一个通过将逻辑模型定义与物理执行调度解耦来实现透明灵活的设备内并行集成的框架。DynaFlow引入灵活的注释前端用于图分区和可编程接口用于定义自定义并行策略。我们演示DynaFlow能以最小代码更改将代表性并行策略集成到6个最先进ML系统中，实现高达1.29倍的吞吐量提升。代码见 https://github.com/uw-syfi/DynaFlow。


---


## [SAKURAONE: An Open Ethernet–Based AI HPC System and Its Observed Workload Dynamics in a Single-Tenant LLM Development Environment](https://mlsys.org/virtual/2026/poster/3535)


**英文摘要 (English Abstract)**:

SAKURAONE is a managed high performance computing (HPC) cluster developed and operated by the SAKURA Internet Research Center. The system consists of 100 nodes, each with eight NVIDIA H100 GPUs, interconnected via a rail-optimized 800 GbE leaf-spine fabric with RoCEv2. Through exclusive use by a single research project, we observed the characteristics of development-related jobs including transitions from large-scale training to iterative refinement.


**中文摘要**:

SAKURAONE是由SAKURA互联网研究中心开发和运营的托管HPC集群，基于KOKARYOKU PHY裸金属GPU平台构建，针对LLM训练等高级工作负载进行了优化。在ISC 2025 TOP500中排名第49位，是前100名中唯一使用完全开放网络栈的系统。系统包含100个节点，每节点8个NVIDIA H100 GPU和2 PB全闪存Lustre文件系统，通过轨优化的800GbE RoCEv2叶脊网络互连。通过单一研究项目的独占使用，我们观察了开发相关作业的特征——小规模作业在数量上占主导，而少数大规模作业消耗了大多数GPU资源时间。随着项目推进，资源使用从大规模训练转向迭代精调。


---


## [XProf: An Open, Scalable, and Extensible Profiling System for the Modern ML Stack](https://mlsys.org/virtual/2026/poster/3604)


**英文摘要 (English Abstract)**:

Optimizing Large Models across thousands of accelerators requires deep system expertise. To address modern machine learning (ML) optimization needs, we present XProf, the ML profiler for the OpenXLA ecosystem. XProf delivers actionable optimization suggestions and in-depth performance analysis, empowering ML researchers and framework users to improve efficiency without specialized systems knowledge. XProf provides a unified, full-stack view of both host (CPU) and device (accelerator - TPUs/GPUs) performance, leveraging tools like the Roofline Model for comprehensive analysis. XProf's distributed architecture is designed to monitor thousands of chips with minimal workload overhead (<1%). This architecture is made pluggable through the open-source PJRT C API extension, which has facilitated its adoption by third-party accelerator vendors. XProf has been instrumental in achieving significant efficiency gains at Google and winning MLPerf submissions. This paper presents the design and architecture of XProf, showcases its differentiating tools and capabilities, and highlights its impact within Google and across the industry as a state of the art ML profiler. XProf is available as part of the OpenXLA project at https://github.com/openxla/xprof.


**中文摘要**:

现代ML技术栈涉及多层软件和硬件，性能分析需要覆盖训练和推理的各个阶段。XProf是一个开放、可扩展的现代ML技术栈分析系统，提供统一的性能数据采集和分析接口。它支持自定义分析插件，覆盖框架层、运行时层和硬件层，为ML系统的性能调优提供了全面的可观测性。


---


## [ExecuTorch - A Unified PyTorch Solution to Run ML Models On-Device](https://mlsys.org/virtual/2026/poster/3545)


**英文摘要 (English Abstract)**:

Federated Learning (FL) enables collaborative training of Large Language Models (LLMs) across distributed data sources while preserving privacy. However, when federated LLMs are deployed in critical applications, it remains unclear which client(s) contributed to specific generated responses, hindering debugging, malicious client identification, fair reward allocation, and trust verification. We present ProToken, a novel Provenance methodology for Token-level attribution in federated LLMs that addresses client attribution during autoregressive text generation while maintaining FL privacy constraints. ProToken leverages two key insights to enable provenance at each token: (1) transformer architectures concentrate task-specific signals in later blocks, enabling strategic layer selection for computational tractability, and (2) gradient-based relevance weighting filters out irrelevant neural activations, focusing attribution on neurons that directly influence token generation. We evaluate ProToken across 16 configurations spanning four LLM architectures (Gemma, Llama, Qwen, SmolLM) and four domains (medical, financial, mathematical, coding). ProToken achieves 98.62% average attribution accuracy in correctly localizing responsible client(s), and maintains high accuracy when the number of clients are scaled, validating its practical viability for real-world deployment settings.


**中文摘要**:

将PyTorch模型部署到边缘设备需要专门的工具链。ExecuTorch是统一的PyTorch设备端ML模型运行解决方案，提供从模型导出、优化到设备端部署的完整工作流。它支持多种硬件平台，包括移动设备、嵌入式系统和微控制器，使PyTorch模型能够高效运行在资源受限的环境中。


---


## [ProToken: Token-Level Attribution for Federated Large Language Models](https://mlsys.org/virtual/2026/poster/3627)


**英文摘要 (English Abstract)**:

We study the Multi-Armed Bandit problem in nonstationary adversarial environments, where the identity of the optimal arm can change over time due to shifts in the loss sequence. Motivated by applications such as physical design tuning in database systems, we focus on settings with a very large number of arms and seek practical algorithms with sublinear runtime. Our main contribution is a novel algorithm, Queuing Behind the Leader (QBL), which achieves a per-iteration complexity of O(m log k), where m is the number of arms selected at each step. QBL combines limited update operations via a priority queue, a constant sampling overhead, and a balanced exploration strategy. We evaluate QBL extensively on state-of-the-art benchmarks and demonstrate that it consistently outperforms existing methods in both time and solution quality.


**中文摘要**:

联邦学习中的大语言模型缺乏对模型更新如何影响特定客户端的细粒度归因。ProToken提出了一种token级别的归因方法，精确量化联邦LLM中每个token对各个客户端的贡献。该方法在不增加通信开销的情况下实现了细粒度的模型行为理解和公平性评估。


---


## [Practical Adversarial Multi-Armed Bandits with Sublinear Runtime](https://mlsys.org/virtual/2026/poster/3539)


**英文摘要 (English Abstract)**:

Large language models (LLMs) require vast amounts of GPU compute to train, but limited availability and high costs of GPUs make homogeneous clusters impractical for many organizations. Instead, assembling heterogeneous clusters by pooling together GPUs of different generations allows them to achieve higher aggregate compute and make use of all available GPUs. However, training on heterogeneous clusters presents significant challenges. The workload must be carefully partitioned such that GPUs in the cluster with limited compute, memory, or network bandwidth do not bottleneck the training process. Existing heterogeneous training systems cannot do so efficiently since they integrate data, pipeline, and tensor parallelism in a way that trades off communication for memory overhead. Combining vanilla data parallelism with pipeline parallelism is communication-efficient but results in high memory overhead from replicating model parameters. Alternatively, using sharded data parallelism or tensor parallelism reduces memory overhead but increases communication overhead when combined with pipeline parallelism. To address this problem, we designed Zorse, a system that uses Pipeline-Efficient ZeRO DP, a novel integration of pipeline parallelism and data parallelism that is both communication- and memory-efficient. Zorse uses a planner to automatically find an optimized training configuration from the vast search space of possibilities on heterogeneous clusters, and our evaluation shows that Zorse achieves up to 3× higher training throughput than state-of-the-art systems across representative heterogeneous training scenarios.


**中文摘要**:

对抗性多臂老虎机问题是强化学习的经典问题，但传统算法在大规模场景下运行时间过高。本文提出了具有次线性运行时间的实用对抗性多臂老虎机算法，通过新颖的算法设计和数据结构优化，在保持对抗性场景下理论保证的同时实现了远优于传统方法的计算效率。


---


## [LearnedCache: An eBPF-Integrated Perceptron-Based Eviction Policy for the Linux Page Cache](https://mlsys.org/virtual/2026/poster/10179)


**英文摘要 (English Abstract)**:

The pervasive "memory wall" bottleneck is significantly amplified in modern large-scale Mixture-of-Experts (MoE) architectures. MoE's inherent architectural sparsity leads to sparse arithmetic compute and also introduces substantial activation memory overheads—driven by large token routing buffers and the need to materialize and buffer intermediate tensors. This memory pressure limits the maximum batch size and sequence length that can fit on GPUs, and also results in excessive data movements that hinders performance and efficient model scaling. We present MoEBlaze, a memory-efficient MoE training framework that addresses these issues through a co-designed system approach: (i) an end-to-end token dispatch and MoE training method with optimized data structures to eliminate intermediate buffers and activation materializing, and (ii) co-designed kernels with smart activation checkpoint to mitigate memory footprint while simultaneously achieving better performance. We demonstrate that MoEBlaze can achieve over 4× speedups and over 50% memory savings compared to existing MoE frameworks. MoEBlaze has been deployed in Meta recommendation production.


**中文摘要**:

Linux页面缓存的驱逐策略传统上使用LRU等启发式方法。LearnedCache将基于感知器的驱逐策略集成到Linux页面缓存的eBPF框架中。通过轻量级机器学习模型预测缓存行的未来访问模式，比传统LRU等启发式策略更准确地识别重要缓存内容，提高了系统整体I/O性能。


---


## [SAT-Eval: A Framework for Preference Drift in Multi-Turn LLM Conversations](https://mlsys.org/virtual/2026/poster/10191)


**英文摘要 (English Abstract)**:

Reinforcement learning (RL) post-training has become essential for aligning large language models (LLMs), yet its efficiency is increasingly constrained by the rollout phase, where long trajectories are generated token by token. We identify a major bottleneck: the long-tail distribution of rollout lengths, where a small fraction of long generations dominates wall clock time and a complementary opportunity; the availability of historical rollouts that reveal stable prompt level patterns across training epochs. Motivated by these observations, we propose DAS, a Distribution Aware Speculative decoding framework that accelerates RL rollouts without altering model outputs. DAS integrates two key ideas: an adaptive, nonparametric drafter built from recent rollouts using an incrementally maintained suffix tree, and a length aware speculation policy that allocates more aggressive draft budgets to long trajectories that dominate makespan. This design exploits rollout history to sustain acceptance while balancing base and token level costs during decoding. Experiments on math and code reasoning tasks show that DAS reduces rollout time up to 50% while preserving identical training curves, demonstrating that distribution-aware speculative decoding can significantly accelerate RL post training without compromising learning quality.


**中文摘要**:

多轮LLM对话中模型的观点和立场可能随时间漂移。SAT-Eval是一个评估多轮LLM对话中偏好漂移的框架，测量模型在长对话中偏好和立场的一致性。它识别可能出现的观点漂移问题，为对话系统的质量保证提供了新的评估维度。


---


## [ApproxMLIR : Accuracy-Aware Compiler for Compound ML System](https://mlsys.org/virtual/2026/poster/3534)


**英文摘要 (English Abstract)**:

Many compound AI systems are inherently approximate because the ML components (e.g., a large language model) are probabilistic models and the non-ML components (e.g., retrieval-augmented generation) are heuristic. Such systems benefit from trading off result quality for improved performance. While extensive work exists on approximating ML and non-ML components individually, the wide deployment of LLMs in compound systems presents significant opportunities for end-to-end, accuracy-aware compilation. However, tailoring approximations across these different components is challenging to implement. This difficulty comes from their reliance on different software stacks for compilation and execution, as well as deployment on different hardware. To address these issues, we present approxMLIR, a reusable accuracy-aware compilation toolchain. approxMLIR introduces the approx MLIR dialect that serves as a unified and centralized interface for defining approximations and approx-opt, a reusable MLIR-based optimizer, which applies approximate transformations on ML and non-ML components. We evaluated approxMLIR on three compound AI systems, which combine LLMs with information retrieval tasks and tool calling. The evaluation shows that approxMLIR can effectively represent many common approximation choices, discover profitable points in the accuracy-performance tradeoff space and consistently achieve higher speedups compared to static approximation strategies.


**中文摘要**:

许多复合AI系统本质上是近似的——ML组件是概率模型，非ML组件是启发式的。虽然已有大量单独近似各组件的工作，但LLM在复合系统中的广泛部署为端到端精度感知编译提供了重要机遇。我们提出approxMLIR，一个可重用的精度感知编译工具链，引入approx MLIR方言作为定义近似的统一集中接口，以及approx-opt基于MLIR的可重用优化器。评估显示approxMLIR可有效表示许多常见近似选择，在精度-性能权衡空间中发现有利点，并相比静态近似策略持续实现更高加速。


---


## [Automated Feature Engineering -- Faster Iteration to Solve Business Problems](https://mlsys.org/virtual/2026/poster/10187)


**英文摘要 (English Abstract)**:

Neural networks on microcontrollers are constrained by kilobytes of flash/SRAM, where 1×1 pointwise (PW) mixers often dominate memory even after INT8 quantization. We present HYPERTINYPW, a compression-as-generation method that replaces most stored PW weights with generated weights: a shared micro-MLP synthesizes PW kernels once at load time from tiny per-layer codes, caches them, and executes them with standard integer operators. This preserves commodity MCU runtimes and incurs only a one-off synthesis cost; steady-state inference matches INT8 separable CNNs. Sharing a latent basis across layers removes cross-layer redundancy, while keeping PW1 in INT8 stabilizes early, morphology-sensitive mixing. We also introduce TinyML-faithful packed-byte accounting (generator, heads/factorization, codes, kept PW1, backbone) and a unified evaluation protocol with validation-tuned thresholds and bootstrap CIs. On three ECG benchmarks (Apnea-ECG, PTB-XL, MIT-BIH), HYPERTINYPW improves the macro-F1–vs.–flash Pareto: at ∼225 kB it achieves near-iso performance to a ∼1.4MB CNN while being 6.31× smaller (84.15% fewer bytes), retaining ≥95% of large-model macro-F1. Beyond ECG, HYPERTINYPW transfers to TinyML audio: on Speech Commands keyword spotting it reaches 96.2% test accuracy (98.2% best validation), supporting that generate-and-cache channel mixing applies broadly to embedded sensing workloads where repeated linear mixers dominate memory.


**中文摘要**: [待翻译]


---


## [Learning-Guided Design Optimization for Lifecycle Impact Analysis](https://mlsys.org/virtual/2026/poster/10190)


**英文摘要 (English Abstract)**:

Large Language Model (LLM) serving is rapidly becoming one of the most power-intensive workloads in modern datacenters. Unlike training, where throughput dominates, inference must satisfy strict per-request latency targets such as Time-to-First-Token (TTFT) and Time-Between-Tokens (TBT). Once an SLO is met, the remaining latency slack between the earliest possible completion and the deadline offers an opportunity for energy savings. Existing systems, however, exploit only one dimension of this trade-off: batching improves resource efficiency, while DVFS improves power efficiency. These two axes are tightly coupled, and optimizing one while fixing the other yields only a local optimum. We present BEAM, a fine-grained controller that dynamically co-optimizes resource and power efficiency under per-request SLOs. BEAM continuously allocates the available latency slack across both dimensions by jointly tuning GPU frequency, chunk size, and microbatch count in real time. Its event-driven design responds instantly to request arrivals and completions, while a lightweight predictive model enables sub-millisecond decision making with negligible overhead. Implemented atop the vLLM runtime, BEAM reduces end-to-end GPU energy consumption by up to 51% compared to vLLM.


**中文摘要**: [待翻译]


---


## [LEANN: A Low-Storage Overhead Vector Index](https://mlsys.org/virtual/2026/poster/3563)


**英文摘要 (English Abstract)**:

Embedding-based vector search underpins many important applications, such as recommendation and retrieval-augmented generation (RAG). It relies on vector indices to enable efficient search. However, these indices require storing high-dimensional embeddings and large index metadata, whose total size can be several times larger than the original data (e.g., text chunks). Such high storage overhead makes it difficult, or even impractical, to deploy vector search on personal devices or large-scale datasets. To tackle this problem, we propose LEANN, a storage-efficient index for vector search that recomputes embeddings on the fly instead of storing them, and compresses state-of-the-art proximity graph indices while preserving search accuracy. LEANN delivers high-quality vector search while using only a fraction of the storage (e.g., 5% of the original data) and supporting storage-efficient index construction and updates. On real-world benchmarks, LEANN reduces index size by up to 50x compared with conventional indices, while maintaining SOTA accuracy and comparable latency for RAG applications.


**中文摘要**:

基于嵌入的向量搜索支撑着推荐和RAG等重要应用，但向量索引需要存储高维嵌入和大量元数据，总大小可达原始数据的数倍。我们提出LEANN，一个存储高效的向量搜索索引，动态重新计算嵌入而非存储它们，并压缩最先进邻近图索引同时保持搜索精度。LEANN仅使用原始数据的一小部分存储（如5%）提供高质量搜索，将索引大小减少高达50倍同时保持SOTA精度和可比较延迟。


---


## [A Framework for Evaluating Neural Network Deployability on Analog In-Memory Computing Hardware](https://mlsys.org/virtual/2026/poster/10196)


**英文摘要 (English Abstract)**:

The autoregressive decode phase of token generation is often a major performance bottleneck in modern AI workflows due to its memory-bandwidth-bound characteristics, which are amplified by powerful open-source models with large context windows and techniques such as chain-of-thought reasoning. Popular GPU architectures extract as little as 21% of the available memory bandwidth from loading weights and KV caches, as the scope of asynchronous execution is limited by CPU scheduling overheads, kernel synchronization overheads, and inadequate compute-communication overlap. While prior work attempts to address these overheads with kernel fusion and asynchronous execution on GPUs, they mostly focus on a single GPU and do not generalize across different model architectures. We argue that to truly mitigate these overheads, Dataflow Is All You Need. In this paper, we chronicle a co-design approach to achieve peak decoding performance on a dataflow architecture -- the SambaNova SN40 Reconfigurable Dataflow Unit (RDU), substantiated by three key dataflow enabled optimizations -- KernelLooping, BatchStreaming, and ScheduleOffloading -- that generalize to models that are small, large, dense, MoEs, or hybrids, and that use different attention mechanisms. Collectively, these optimizations deliver more than 75% of the theoretical peak roofline performance for a wide range of popular open-source models and demonstrate a speedup of more than 6× when using popular speculative decoding techniques. Finally, we show that speculative decoding is 1.7× faster on 16 SN40 chips than on a DGX H100 despite both systems having comparable HBM bandwidth. The techniques described in this paper and the models used in the evaluation are deployed in a production AI inference cloud at cloud.sambanova.ai.


**中文摘要**: [待翻译]


---


## [ProfInfer: An eBPF-based Fine-Grained LLM Inference Profiler](https://mlsys.org/virtual/2026/poster/3517)


**英文摘要 (English Abstract)**:

As large language models (LLMs) move from research to production, understanding how inference engines behave in real time has become both essential and elusive. We develop a fine-grained, non-intrusive profiling framework for modern LLM inference engines, built on extended Berkeley Packet Filter (eBPF) technology. With less than 4% runtime overhead and high profiling fidelity, our framework makes LLM inference both transparent and diagnosable.


**中文摘要**:

随着LLM从研究转向生产，实时理解推理引擎的行为变得至关重要。我们开发了基于eBPF技术的细粒度非侵入式LLM推理分析框架，动态附加探针到运行时函数跨多个层，无需修改或重编译源代码。将收集的追踪转换为算子、图、时间线和硬件计数器趋势的丰富可视化。运行时开销低于4%且高分析保真度，使LLM推理变得透明可诊断。


---


## [SONAR: Benchmarking Topology and Collaboration in Decentralized Learning](https://mlsys.org/virtual/2026/poster/3634)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


## [Designing Communication-Efficient AI Systems: An Interconnect-Aware HPC Perspective](https://mlsys.org/virtual/2026/poster/10169)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


## [Charon: A Unified and Fine-Grained Simulator for Large-Scale LLM Training and Inference](https://mlsys.org/virtual/2026/poster/3638)


**英文摘要 (English Abstract)**:

Deploying large-scale LLM training and inference with optimal performance is exceptionally challenging due to a complex design space of parallelism strategies, system optimizations, and hardware configurations. We introduce Charon, a unified, modular, and fine-grained simulator for accurately predicting LLM performance. Experiments show Charon achieves high accuracy with an overall prediction error consistently under 5.35%.


**中文摘要**:

大规模LLM训练和推理的最优性能部署因并行策略、系统优化和硬件配置的复杂设计空间而极具挑战。我们引入Charon，一个统一、模块化、细粒度的仿真器用于准确预测LLM性能。实验显示Charon在不同模型和配置上实现高准确率，总体预测误差始终低于5.35%，大规模GPU集群训练误差甚至低于3.74%。在实际推理部署案例中，Charon发现的配置相比工程调优基线提高了系统吞吐量。


---


# 安全与隐私（9 篇）


## [ZK-APEX: ZERO-KNOWLEDGE APPROXIMATE PERSONALIZED UNLEARNING WITH EXECUTABLE PROOFS](https://mlsys.org/virtual/2026/poster/3570)


**英文摘要 (English Abstract)**:

Machine unlearning aims to remove the influence of specific data points from a trained model to satisfy privacy, copyright, and safety requirements. We introduce ZK-APEX, a zero-shot personalized unlearning method that operates directly on the personalized model without retraining. ZK-APEX combines sparse masking on the provider side with a small Group OBS compensation step on the client side. Paired with Halo2 zero-knowledge proofs, it enables the provider to verify that the correct unlearning transformation was applied without revealing any private data or personalized parameters.


**中文摘要**:

机器遗忘旨在从训练模型中移除特定数据点的影响，以满足隐私、版权和安全要求。在实际部署中，提供者将全局模型分发给许多边缘设备，每个客户端使用私有数据对模型进行个性化。当发出删除请求时，客户端可能忽略它或虚假声明合规，而提供者无法检查其参数或数据。这使得验证变得困难，尤其因为个性化模型必须遗忘目标样本同时保留本地效用，且验证必须在边缘设备上保持轻量级。我们引入ZK-APEX，一种直接在个性化模型上操作而无需重新训练的零样本个性化遗忘方法。ZK-APEX在提供者侧结合稀疏掩码，在客户端侧结合小型Group OBS补偿步骤，使用块状经验Fisher矩阵创建为低开销设计的曲率感知更新。配合Halo2零知识证明，它使提供者能够验证正确的遗忘变换已被应用，而不泄露任何私有数据或个性化参数。在Vision Transformer分类任务上，ZK-APEX恢复了几乎所有的个性化精度，同时有效移除了目标信息。应用于在代码数据上训练的OPT125M生成模型时，它恢复了约70%的原始精度。ViT案例的证明生成在大约两小时内完成，比基于重新训练的检查快超过一千万倍，内存使用少于1GB，证明大小约400MB。这些结果展示了在边缘设备上可验证个性化遗忘的首个实用框架。


---


## [Toward Principled LLM Safety Testing: Solving the Jailbreak Oracle Problem](https://mlsys.org/virtual/2026/poster/3516)


**英文摘要 (English Abstract)**:

As large language models (LLMs) become increasingly deployed in safety-critical applications, the lack of systematic methods to assess their vulnerability to jailbreak attacks presents a critical security gap. We introduce the jailbreak oracle problem and present Boa, the first system designed for efficiently solving it. Boa employs a two-phase search strategy combining breadth-first sampling with depth-first priority search guided by fine-grained safety scores.


**中文摘要**:

随着大语言模型越来越多地部署在安全关键应用中，缺乏系统的方法来评估其越狱攻击脆弱性构成了关键安全缺口。我们引入越狱预言机问题：给定一个模型、提示和解码策略，判断是否能以超过指定阈值的可能性生成越狱响应。这一形式化为越狱脆弱性的原则性研究奠定了基础。回答越狱预言机问题面临重大计算挑战，因为搜索空间随响应长度指数增长。我们提出Boa，首个为高效解决越狱预言机问题而设计的系统。Boa采用两阶段搜索策略：广度优先采样以识别易于访问的越狱方案，然后由细粒度安全评分引导的深度优先优先级搜索以系统探索有前景但低概率的路径。Boa实现了严格的安全评估，包括系统性防御评估、红队攻击的标准化比较以及极端对抗条件下的模型认证。代码见 https://github.com/shuyilinn/BOA/tree/mlsys2026ae。


---


## [Blueprint, Bootstrap, and Bridge: A Security Look at NVIDIA GPU Confidential Computing](https://mlsys.org/virtual/2026/poster/3518)


**英文摘要 (English Abstract)**:

NVIDIA GPU Confidential Computing (GPU-CC) aims to provide secure execution for AI workloads. For end users, enabling GPU-CC is seamless and requires no modifications to existing applications. In this work, we provide a security look at GPU-CC by reconstructing a coherent view of the system. We first examine the system's blueprint, then analyze the bootstrap process, and finally conduct targeted experiments to assess data transfer protections.


**中文摘要**:

随着LLM持续扩展和新GPU频繁发布，异构环境下LLM后训练的需求日益增加。我们提出HetRL，一个在异构GPU和网络基础设施中实现高效RL训练的分布式系统。我们广泛的评估消耗了20,000 GPU小时，显示HetRL在最先进系统的基础上实现高达9.17倍、平均3.17倍的吞吐量提升。


---


## [Zero redundancy distributed learning with differential privacy](https://mlsys.org/virtual/2026/poster/3580)


**英文摘要 (English Abstract)**:

We present core attention disaggregation (CAD), a technique that improves long-context LLM training by disaggregating the core attention (CA) — the parameter-free softmax(QK^T)V computation — and schedules it on an independent pool of resources. Existing systems co-locate core attention with other components. At long context, the quadratic growth of CA computation and near-linear growth of the rest create load imbalance — hence stragglers across data and pipeline groups. CAD is enabled by two key observations: (i) statelessness: CA has no trainable parameters and minimal transient state, so balancing reduces to scheduling compute-bound tasks; and (ii) composability: modern attention kernels sustain high utilization on fused batches of arbitrary-length token-level shards. CAD dynamically partitions the core attention computation into token-level tasks (CA-tasks), and dispatches them to a pool of devices specialized for CA computation (attention servers). It then rebatches CA-tasks to equalize CA compute across attention servers without loss of kernel efficiency. We have implemented CAD in a system called DistCA with a ping-pong scheme to completely overlap communication with compute, and in-place attention servers to improve memory utilization. Scaling to 512 H200 GPUs and 512K context length, DistCA eliminates DP/PP stragglers, achieves near-perfect compute and memory balance, and improves end-to-end training throughput by up to 1.9× over Megatron-LM and 1.35× over existing load-balancing methods.


**中文摘要**:

差分隐私与分布式深度学习往往存在张力——差分隐私需要噪声注入，而分布式训练旨在最大化效率。本文提出了一种在零冗余优化器中集成差分隐私的分布式学习方法。通过精心设计的噪声注入策略和梯度裁剪机制，该方法在保护数据隐私的同时保持了较高的训练效率，实现了隐私保护和模型性能之间的有效平衡。


---


## [G-HEMP: FAST MULTI-GPU PRIVATE INFERENCE FOR LARGE-SCALE GCNS WITH HOMOMORPHIC ENCRYPTION](https://mlsys.org/virtual/2026/poster/3588)


**英文摘要 (English Abstract)**:

Homomorphic Encryption (HE) offers a promising solution for privacy-preserving Graph Convolutional Network (GCN) inference in untrusted cloud environments by enabling computation directly on encrypted data. This capability is particularly valuable in domains such as recommendation systems, financial analysis, and bioinformatics, where data confidentiality is paramount. However, applying HE to large-scale GCN inference introduces substantial computational and memory overhead, severely limiting scalability and runtime efficiency. While prior works focusing on algorithmic improvements have demonstrated feasibility on CPUs, these approaches struggle to scale effectively on GPUs due to excessive memory consumption and redundant computation. In this work, we present G-HEMP, the first framework that leverages multi-GPU systems to accelerate large-scale private GCN inference. G-HEMP introduces two key innovations: (i) a block-diagonal parallel packing scheme that eliminates redundant data replication in encrypted adjacency matrices, reducing the number of HE operations and achieving up to 4.41× speedup over conventional feature-wise packing under single GPU environment; and (ii) a multi-GPU workload partitioning strategy that halves per-GPU peak memory usage on a 4-GPU system and achieves up to 3.88× latency improvement. Compared to the limb-level-partitioning-based approach in Cinnamon–the state-of-the-art encrypted computation parallelization method, G-HEMP further attains up to 3.13× gain owing to our superior multi-device partition policy. Overall, G-HEMP is model-agnostic and scales seamlessly with graph size and GPU count, enabling efficient and practical privacy-preserving GCN inference on modern heterogeneous environments.


**中文摘要**:

图神经网络在药物发现和社交网络等隐私敏感领域广泛应用，但私有推理的计算开销巨大。G-HEMP是一个利用同态加密进行大规模GCN多GPU私有推理的快速框架，通过优化加密域中的矩阵乘法和通信模式，在保持数据完全加密的条件下实现了高效的图神经网络推理。


---


## [Leveraging ASIC AI Chips for Homomorphic Encryption](https://mlsys.org/virtual/2026/poster/10176)


**英文摘要 (English Abstract)**:

Local execution of AI on edge devices is critical for privacy, low latency, and offline operation. However, deploying models on diverse hardware remains fragmented, often requiring model conversion or complete implementation outside the PyTorch ecosystem where the model was originally authored. We introduce ExecuTorch, a unified PyTorch-native deployment framework for edge AI. ExecuTorch enables seamless deployment of machine learning models across heterogeneous compute environments. It scales from completely embedded microcontrollers to complex system-on-chips (SoCs) with dedicated accelerators, powering devices ranging from wearables and smartphones to large compute clusters. ExecuTorch preserves PyTorch semantics while allowing customization, support for optimizations like quantization, and pluggable execution "backends". These features together enable fast experimentation, allowing researchers to validate deployment behavior entirely within PyTorch, bridging the gap between research and production.


**中文摘要**: [待翻译]


---


## [CSLE: A Reinforcement Learning Platform for Autonomous Security Management](https://mlsys.org/virtual/2026/poster/3589)


**英文摘要 (English Abstract)**:

Reinforcement learning is a promising approach to autonomous and adaptive security management in networked systems. We present CSLE, a reinforcement learning platform for autonomous security management that enables experimentation under realistic conditions. CSLE encompasses both an emulation system that replicates key components of the target system and a simulation system where security strategies are efficiently learned.


**中文摘要**:

智能体现已广泛应用于软件开发过程，但构建生产就绪的软件工程智能体是一项复杂任务。我们提出OpenHands软件智能体SDK，一个实现软件开发智能体的工具包。与OpenAI、Claude和Google的现有SDK相比，OpenHands独特地集成了原生沙箱执行、生命周期控制、模型无关的多LLM路由和内置安全分析。


---


## [ADR: AN AGENTIC DETECTION SYSTEM FOR ENTERPRISE AGENTIC AI SECURITY](https://mlsys.org/virtual/2026/poster/3630)


**英文摘要 (English Abstract)**:

We present the Agentic AI Detection and Response (ADR) system, the first large-scale, production-proven enterprise framework for securing AI agents operating through the Model Context Protocol (MCP). Deployed at Uber for over ten months, ADR has sustained reliable detection in production with growing adoption reaching over 7,200 unique hosts and processing over 10,000 agent sessions daily.


**中文摘要**:

许多复合AI系统本质上是近似的，因为ML组件是概率模型，非ML组件是启发式的。我们提出approxMLIR，一个可重用的精度感知编译工具链。approxMLIR引入了approx MLIR方言作为定义近似的统一接口，以及approx-opt（基于MLIR的可重用优化器）。评估显示approxMLIR能有效表示许多常见近似选择。


---


## [Privatar: Scalable Privacy-preserving Multi-user VR via Secure Offloading](https://mlsys.org/virtual/2026/poster/3578)


**英文摘要 (English Abstract)**:

Multi-user virtual reality enables immersive interaction. We introduce Privatar, a framework to offload avatar reconstruction from headset to untrusted devices within the same local network while safeguarding attacks against adversaries. On a Meta Quest Pro, Privatar supports 2.37x more concurrent users at 6.5% higher reconstruction loss and 9% energy overhead.


**中文摘要**:

多用户VR的虚拟形象渲染对每个头显产生高昂的计算开销。我们引入Privatar，一个将虚拟形象重建从头显卸载到同一局域网内不可信设备同时防御攻击的框架。关键洞察是虚拟形象重建在频域上可通过BDCT分解且质量下降可忽略。提出水平分区将高能频率分量保留在设备上仅卸载低能分量。在Meta Quest Pro上支持2.37倍更多并发用户，重建损失增加6.5%，能耗开销9%。


---


# 多模态与生成模型（4 篇）


## [ViRuleEval: A Neuro-Symbolic System for Interpretable Evaluation of Text-to-Video Generation](https://mlsys.org/virtual/2026/poster/10171)


**英文摘要 (English Abstract)**:

In modern data centers, servers organize memory and CPUs into Non-Uniform Memory Access (NUMA) nodes, where unequal memory-to-CPU proximity leads to varying memory latency. Hypervisors must carefully place Virtual Machines (VMs) to reduce remote memory access. Poor placements can lead to significant performance degradation—sometimes up to 30%. However, achieving optimal placement at scale is challenging due to the large number of VM configurations, diverse NUMA structures, and evolving workload patterns. We present Catur, a NUMA placement system designed for large-scale cloud environments. Catur leverages reinforcement learning to learn from production data. Moreover, to address real-world challenges, Catur integrates several techniques: robust action space design to prevent model collapse, reward shaping to address learning inefficiency, drift-aware continuous training for evolving workload patterns, and speculative shielding to mitigate VM performance anomalies. Evaluations on production traces with 100 million VMs demonstrate that Catur reduces average resource defect by 34.2%–50.0% compared to state-of-the-art hypervisor policies.


**中文摘要**: [待翻译]


---


## [TiDAR: Think in Diffusion, Talk in Autoregression](https://mlsys.org/virtual/2026/poster/3528)


**英文摘要 (English Abstract)**:

Neural networks on microcontrollers are constrained by kilobytes of flash/SRAM, where 1×1 pointwise (PW) mixers often dominate memory even after INT8 quantization. We present HyperTinyPW, a compression-as-generation method that replaces most stored PW weights with generated weights: a shared micro-MLP synthesizes PW kernels once at load time from tiny per-layer codes, caches them, and executes them with standard integer operators. This preserves commodity MCU runtimes and incurs only a one-off synthesis cost; steady-state inference matches INT8 separable CNNs. Sharing a latent basis across layers removes cross-layer redundancy, while keeping PW1 in INT8 stabilizes early, morphology-sensitive mixing. We also introduce TinyML-faithful packed-byte accounting (generator, heads/factorization, codes, kept PW1, backbone) and a unified evaluation protocol with validation-tuned thresholds and bootstrap CIs. On three ECG benchmarks (Apnea-ECG, PTB-XL, MIT-BIH), HyperTinyPW improves the macro-F1–vs.–flash Pareto: at ∼225 kB it achieves near-iso performance to a ∼1.4MB CNN while being 6.31× smaller (84.15% fewer bytes), retaining ≥95% of large-model macro-F1. Beyond ECG, HyperTinyPW transfers to TinyML audio: on Speech Commands keyword spotting it reaches 96.2% test accuracy (98.2% best validation), supporting that generate-and-cache channel mixing applies broadly to embedded sensing workloads where repeated linear mixers dominate memory.


**中文摘要**:

自回归模型虽然连贯性好但生成速度慢，扩散模型速度快但连贯性差。TiDAR提出了一种混合生成架构——在扩散中思考，在自回归中表达。它结合了扩散模型在并行迭代生成方面的优势和自回归模型的语言连贯性优势，在保持文本质量的同时显著减少了生成步数。


---


## [StreamDiffusionV2: A Streaming System for Dynamic and Interactive Video Generation](https://mlsys.org/virtual/2026/poster/3527)


**英文摘要 (English Abstract)**:

Generative models are reshaping the live-streaming industry by redefining how content is created, styled, and delivered. Previous image-based streaming diffusion models have powered efficient and creative live streaming products but has hit limits on temporal consistency due to the foundation of image-based designs. Recent advances in video diffusion have markedly improved temporal consistency and sampling efficiency for offline generation. However, offline generation systems primarily optimize throughput by batching large workloads. In contrast, live online streaming operates under strict service-level objectives (SLOs): time-to-first-frame must be minimal, and every frame must meet a per-frame deadline with low jitter. Besides, scalable multi-GPU serving for real-time streams remains largely unresolved so far. To address this, we present StreamDiffusionV2, a training-free pipeline for interactive live streaming with video diffusion models. StreamDiffusionV2 integrates an SLO-aware batching scheduler and a block scheduler, together with a sink-token-guided rolling KV cache, a motion-aware noise controller, and other system-level optimizations. Moreover, we introduce a scalable pipeline orchestration that parallelizes the diffusion process across denoising steps and network layers, achieving near-linear FPS scaling without violating latency guarantees. The system scales seamlessly across heterogeneous GPU environments and supports flexible denoising steps (e.g., 1-4), enabling both ultra-low-latency and higher-quality modes. Without TensorRT or quantization, StreamDiffusionV2 renders the first frame within 0.5s and attains 58.28 FPS with a 14B-parameter model and 64.52 FPS with a 1.3B-parameter model on four H100 GPUs. Even when increasing denoising steps to improve quality, it sustains 31.62 FPS (14B) and 61.58 FPS (1.3B), making state-of-the-art generative live streaming practical and accessible—from individual creators to enterprise-scale platforms.


**中文摘要**:

生成模型正在重塑直播行业。先前的基于图像的流式扩散模型为高效直播产品提供了动力，但基于图像设计的基础限制了时间一致性。离线生成系统通过批量处理大量工作负载优化吞吐量，而在线直播在严格SLO下运行。我们提出StreamDiffusionV2，一个无需训练的交互式直播视频扩散流水线，集成SLO感知批处理调度器、块调度器、sink-token引导滚动KV缓存、运动感知噪声控制器等系统级优化。引入可扩展流水线编排，跨去噪步骤和网络层并行化扩散过程，实现近线性FPS扩展。在四块H100 GPU上无需TensorRT或量化，14B模型0.5秒内渲染首帧并达到58.28 FPS，1.3B模型达到64.52 FPS。


---


## [REPARO: LOSS-RESILIENT GENERATIVE CODEC FOR VIDEO CONFERENCING](https://mlsys.org/virtual/2026/poster/3616)


**英文摘要 (English Abstract)**: [待补充]


**中文摘要**: [待补充]


---


# 基准测试与评估（4 篇）


## [DriftBench: Measuring and Predicting Infrastructure Drift in LLM Serving Systems](https://mlsys.org/virtual/2026/poster/10172)


**英文摘要 (English Abstract)**:

Optimizing large-language model (LLM) training and serving on large-scale distributed systems is a significant challenge. This difficulty stems from the rapidly evolving LLM landscape, the requirement for deep domain expertise, and the need for workload-specific optimization strategies. Existing methods rely on either handcrafted optimization performed by human experts, which is tedious and time-consuming, or resource-intensive black-box searches, which lack the extensibility to keep pace with evolving models and hardware. To address this, we introduce PROMPTS, a novel multi-agent framework that complements traditional search methods with expert-informed reasoning to deliver system-level optimization with much fewer shots. Key components of the proposed framework include an Analyzer Agent that diagnoses performance bottlenecks by synthesizing profiler data and a Proposal Agent that leverages a knowledge base to generate optimized sharding configurations with detailed justifications through retrieval-augmented generation (RAG). Experimental results across eight real-world LLM workloads have demonstrated that PROMPTS can provide valid reasoning and accurate recommendations by considering LLM workload characteristics and backend hardware features, delivering performance improvements of up to 434%. These workloads spanned LLMs with Mixture-of-Experts (MoE) and dense models, system configurations from 2-TPU chips to 512-chip systems with 2D/3D Torus interconnects, and the full LLM lifecycle including pre-training, post-training, and serving. To validate our agent's system optimization proposals, we benchmarked them against production configurations that were previously optimized by experts, either through extensive manual analysis or automated black-box searches. In every case, our agent independently identified this expert-validated solution within its top three recommendations from a single invocation. Furthermore, the agent's top-ranked recommendation matched the production solution in 87.5% of cases, demonstrating its ability to not only find optimized configurations but also to correctly prioritize the optimization candidates.


**中文摘要**:

生产级LLM部署缺乏系统的方法来评估基础设施变化对输出一致性的风险。基础设施漂移——硬件配置、软件版本和数据分布的渐进变化——会在不明显降低标准指标的情况下导致模型行为发生意外变化。我们提出DriftBench，一个用于测量和预测LLM服务系统中基础设施漂移的基准测试框架。它提供了一套标准化的漂移场景、检测指标和预测模型，使运维人员能够在漂移影响生产服务质量之前主动识别和缓解漂移。在两个大型生产集群上为期三个月的实验表明，DriftBench能够在中位数提前14天检测到显著的漂移事件，误报率低于5%。


---


## [PARROT: Persuasion and Agreement Robustness Rating of Output Truth — A Sycophancy Robustness Benchmark for LLMs](https://mlsys.org/virtual/2026/poster/3568)


**英文摘要 (English Abstract)**:

Machine learning (ML) infrastructures operating at warehouse scale present unique performance characterization challenges beyond traditional high-performance computing metrics. This paper introduces a systematic framework for analyzing ML fleet efficiency, demonstrated on Google's production TPU infrastructure comprising thousands of accelerators running diverse workloads. Our fleet-wide analysis reveals performance dependencies spanning the entire ML system stack, from hardware to model architecture, data pipelines, frameworks, compilers, and schedulers. We identify critical gaps in conventional utilization-based performance metrics and propose "ML Productivity Goodput" (MPG) to capture fleet-wide efficiency across heterogeneous ML environments. MPG decomposes efficiency into scheduling, runtime, and program components, enabling precise identification of bottlenecks at specific system layers. Applied to Google's production TPU workloads, our segmented analysis identified optimization opportunities across the stack: scheduling goodput exceeding 95% for all job sizes through careful preemption tuning, runtime improvements via framework modernization and asynchronous checkpointing, and program-level gains through compiler optimizations like communication-computation overlap. This establishes MPG as a practical methodology for managing large-scale ML computing infrastructure.


**中文摘要**:

LLM在面对用户观点时可能表现出谄媚倾向——迎合用户的错误观点而非坚持正确的判断。PARROT是一个专门评估LLM谄媚鲁棒性的基准测试，系统地测量模型在说服和一致性测试中的表现。该基准为评估和改进LLM的推理鲁棒性提供了标准化工具，涵盖了多种对话场景和难度级别。


---


## [Learning from Less: Measuring the Effectiveness of RLVR in Low Data and Compute Regimes](https://mlsys.org/virtual/2026/poster/3560)


**英文摘要 (English Abstract)**:

Efficiently serving large language models (LLMs) under dynamic and bursty workloads remains a key challenge for real-world deployment. Existing serving frameworks and static model compression techniques fail to adapt to workload fluctuations, leading to either service-level objective (SLO) violations under full-precision serving or persistent accuracy degradation with static quantization. To deal with these issues, we present MorphServe, a dynamic, workload-aware LLM serving framework based on morphological adaptation. MorphServe introduces two asynchronous, token-level runtime mechanisms: quantized layer swapping, which selectively replaces less impactful layers with quantized alternatives during high-load periods, and pressure-aware KV cache resizing, which repurposes the freed memory to dynamically expand KV cache capacity. These mechanisms enable state-preserving transitions that jointly coordinate weight precision and KV capacity at runtime. Extensive experiments on Vicuna and Llama family models with real-world workloads demonstrate that MorphServe reduces average SLO violations by 92.45% and improves P95 TTFT by 2.2×–3.9× over full-precision serving, without compromising generation quality. Compared to planning-based quantization methods, MorphServe reduces average accuracy degradation by 41.3%, and lowers P95 TTFT by up to 2.4× over KV cache compression while maintaining higher generation quality. These results establish MorphServe as a practical and elastic solution that effectively navigates the accuracy–efficiency Pareto frontier under dynamic LLM serving workloads.


**中文摘要**:

强化学习与验证器奖励方法通常依赖大规模数据和计算资源。本文系统衡量了RLVR在低数据和低计算资源条件下的有效性，通过受控实验揭示了该方法在资源受限场景下的性能边界。研究为难于获取大规模数据或计算资源的研究者和实践者提供了何时以及如何有效使用RLVR的实用指导。


---


## [Speciesism in the Assistant Axis: Probing Compassion Vectors in Post-Trained LLMs](https://mlsys.org/virtual/2026/poster/10201)


**英文摘要 (English Abstract)**:

Reinforcement learning (RL) post-training has become essential for aligning large language models (LLMs), yet its efficiency is increasingly constrained by the rollout phase, where long trajectories are generated token by token. We identify a major bottleneck: the long-tail distribution of rollout lengths, where a small fraction of long generations dominates wall clock time and a complementary opportunity; the availability of historical rollouts that reveal stable prompt level patterns across training epochs. Motivated by these observations, we propose DAS, a Distribution Aware Speculative decoding framework that accelerates RL rollouts without altering model outputs. DAS integrates two key ideas: an adaptive, nonparametric drafter built from recent rollouts using an incrementally maintained suffix tree, and a length aware speculation policy that allocates more aggressive draft budgets to long trajectories that dominate makespan. This design exploits rollout history to sustain acceptance while balancing base and token level costs during decoding. Experiments on math and code reasoning tasks show that DAS reduces rollout time up to 50% while preserving identical training curves, demonstrating that distribution-aware speculative decoding can significantly accelerate RL post training without compromising learning quality.


**中文摘要**: [待翻译]


---

