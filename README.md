# Awesome-schedulers
Records of some awesome resource scheduling papers.🚀🚀🚀

I am a Phd in Chongqing University and my research topic is AIsys, resource scheduler(Job & Communication), computer vision(semi-supervised Learning).

😎 I am actively maintaining this list. 💪
## Resource Scheduler
### Scheduling for DL Training Workloads
#### 2024

* Blox: A Modular Toolkit for Deep Learning Schedulers (EuroSys 2024) [[arXiv](https://arxiv.org/pdf/2312.12621)]  [[Code](https://github.com/msr-fiddle/blox)]

* Heet: Accelerating Elastic Training in Heterogeneous  Deep Learning Clusters (ASPLOS 2024) [[Paper](https://dl.acm.org/doi/10.1145/3620665.3640375)]

#### 2023
* GPU Cluster Scheduling for Network-Sensitive Deep Learning (arXiv 2024) [[arXiv](https://arxiv.org/abs/2401.16492)]

* Sia: Heterogeneity-aware, goodput-optimized ML-cluster scheduling (SOSP 2023) [[Paper](https://dl.acm.org/doi/10.1145/3600006.3613175)]
  - <details>  
    <summary>[Personal Notes]</summary>
    
    # Background
    Sia categorizes the existing schedulers as follows:
    
    (1) Heterogeneity-aware Schedulers: Focus on the heterogeneity of resources, considering the computational performance differences between different GPUs.
    
    (2) Adaptivity-aware Schedulers: **Focus on the elasticity of tasks**, which can adjust the number of GPU allocations according to the resource status of the cluster, such as dynamically adjusting the mini-batch size, automatically increasing or decreasing GPU resources.
    
    (3) Traditional Static Schedulers: Adopt **fixed resource allocation strategies**, such as specifying GPU requirements at the time of task submission, which cannot be adjusted adaptively according to the cluster load.
    
    The existing scheduler cannot optimize simultaneously:
    
    1) Utilization of heterogeneous GPU resources
    
       2) Dynamic adaptation capability of tasks
    
       3) Overall throughput/goodput
    
    For example:
    
    Gavel, when the load is high, due to the inability to adjust the scale of tasks, can lead to inefficient utilization of GPU resources.
    
    Pollux cannot effectively match tasks with GPUs in heterogeneous clusters, causing some tasks to run on **inappropriate GPUs**, affecting training efficiency.
        
    # Innovations  
    (1) At the same time, optimize GPU resource heterogeneity and task elasticity
    
    (2) Low-overhead Throughput Modeling Method
    
    - Existing schedulers require a large amount of experimental data to measure the throughput of different tasks on different GPU resources before scheduling, which leads to:
    
      - **High data collection costs** (requires running a large number of benchmark tests in advance).
    
      - **Low scheduling efficiency for new tasks** (requires waiting for sufficient test data).
    
      The throughput of GPU tasks is affected by various factors such as **GPU type, the computational characteristics of the task itself, and the number of GPUs**. Traditional methods need to **completely traverse all possible GPU combinations**, resulting in excessive computational overhead.
    
    **Sia adopts a "Bootstrap Throughput Modeling" method**, with the core idea being:
    
    - When a task is submitted, **only the minimum test is performed on a single GPU** to obtain basic throughput data.
    
      - A simple **ratio model** (ratio model) is used to predict the throughput on different GPU types:
    
        - For example, if the throughput of a task on a T4 GPU is X, and the standard throughput on an A100 is 2X, it is inferred that the throughput on the A100 is also 2X.
    
    (3) Introduction of Integer Linear Programming (ILP) Scheduling Optimization Framework
    
    Most existing methods adopt **heuristic scheduling algorithms**, leading to:
    
    - **Too large search space**: For a large GPU cluster, there may be thousands or even tens of thousands of GPU task allocation schemes, and simple heuristic search is difficult to find the global optimal solution.
    
      - **Poor adaptability**: When task load changes dynamically, heuristic methods cannot quickly adjust the matching of tasks and resources, leading to a decrease in scheduling efficiency.
    
    Pollux uses **Genetic Algorithm (GA)** for task allocation, but this method has **high computational cost and poor scalability**, and when the GPU scale reaches 1000+, the scheduling time may exceed 10 minutes.
    
    Integer Linear Programming (ILP) is more suitable for complex GPU task scheduling problems than traditional heuristic methods.
    
    - **Sia uses ILP for global optimization, which can optimize multiple factors simultaneously, such as task throughput, GPU type matching, and task fairness.**
    
      - ILP ensures through constraint conditions:
    
        - **Tasks are not allocated to overloaded GPUs**.
    
        - **The allocation of GPU resources for tasks can be dynamically adjusted according to the load**.
    
        - **Resource allocation between different tasks is fair** (i.e., no task will occupy a large amount of GPU resources for a long time).
    
      - **Sia's ILP scheduling method can complete optimization calculations in a few seconds, allowing it to scale to large clusters with 2000+ GPUs.**

    (4) Scalable Phased Scheduling Strategy
    
    Existing schedulers typically use **single-phase scheduling**, which means deciding the GPU allocation for all tasks simultaneously in each scheduling round. However, this method has the following issues:
    
    - **High computational cost**: In large-scale GPU clusters, each scheduling round requires searching through a large number of GPU combinations, resulting in high computational complexity.
    
      - **Poor adaptability**: During task execution, GPU resources may change dynamically (such as task completion or new tasks joining), and single-phase scheduling cannot adjust quickly.
    
      - **GPU resource fragmentation**: Tasks may be randomly assigned to GPUs, leading to underutilization of GPU resources.
    
    **Sia adopts a "two-phase scheduling" strategy:**
    
    1. **Resource Allocation**: Decide the GPU type and quantity for tasks first to maximize throughput.
    
       2. **Resource Mapping**: Then, based on the allocation results, find the optimal GPU combination in the physical cluster to reduce GPU migration costs.
    
    (5) Optimizing Fairness and GPU Task Scheduling Strategy
    
    Existing methods (such as Shockwave, Pollux) cannot achieve the best balance between fairness and throughput:
    
    - Shockwave emphasizes fairness too much, leading to a decrease in overall throughput.
    
      - Pollux tends to maximize throughput, resulting in some tasks not receiving GPU resources for a long time.
    
      - **Sia achieves scheduling optimization through "Fairness Parameter":**
    
        - **The GPU allocation for tasks can be adjusted according to different priorities**, ensuring that all tasks have a chance to obtain GPU resources.
    
        - **The scheduler can adjust the fairness parameter to find the best balance point between throughput and fairness**.
    
        - **Compared to Pollux, Sia increases throughput while reducing the waiting time for tasks, improving the overall efficiency of the cluster.**

      </details>
  * Lyra: Elastic Scheduling for Deep Learning Clusters (EuroSys 2023) [[Paper](https://dl.acm.org/doi/10.1145/3552326.3587445)]

  * Shockwave: Fair and Efficient Cluster Scheduling for Dynamic Adaptation in Machine Learning (NSDI 2023) [[Paper](https://www.usenix.org/conference/nsdi23/presentation/zheng)]  [[Code](https://github.com/uw-mad-dash/shockwave)]

  * Lucid: A Non-intrusive, Scalable and Interpretable Scheduler for Deep Learning Training Jobs (ASPLOS 2023) [[Paper](https://dl.acm.org/doi/10.1145/3575693.3575705)] [[Code](https://github.com/S-Lab-System-Group/Lucid)]
    - Code may invalid...

  * ElasticFlow: An Elastic Serverless Training Platform for Distributed Deep Learning (ASPLOS 2023) [[Paper](https://dl.acm.org/doi/10.1145/3575693.3575721)]

#### 2022
* Looking Beyond GPUs for DNN Scheduling on Multi-Tenant Clusters (OSDI 2022) [[Paper](https://www.usenix.org/conference/osdi22/presentation/mohan)] [[Code](https://github.com/msr-fiddle/synergy) ]

* Multi-Resource Interleaving for Deep Learning Training (SIGCOMM 2022) [[Paper](http://yibozhu.com/doc/muri-sigcomm22.pdf)] [[Code](https://github.com/Rivendile/Muri)]

#### 2021
* Pollux: Co-adaptive Cluster Scheduling for Goodput-Optimized Deep Learning (OSDI 2021) [[Paper](https://www.usenix.org/conference/osdi21/presentation/qiao)] [[Code](https://github.com/petuum/adaptdl)] 
  - <details>  
    <summary>[Personal Notes]</summary>  
  
      # Problem Statement  
      The elastic scheduler can dynamically select the number of resources but ignores adjustments to model hyperparameters (batch size & learning rate).  
    
      # Innovations  
      1. **Elastic and Resource-Adaptive DLT Job Scheduler**: A novel scheduler that adapts to resource availability.  
      2. **Balancing Throughput and Statistical Efficiency**: DL jobs should strike a balance between system throughput and statistical efficiency.  
      3. **Goodput Definition**: $\( \text{goodput} = \text{throughput} \times \text{statistical efficiency} \)  $
      4. **Dynamic Adjustment of Batch Size and Learning Rate**: At the job level, Pollux dynamically adjusts batch size and learning rate to optimally utilize allocated resources based on goodput.  
      5. **Dynamic Resource Reallocation**: Resources are dynamically (re)allocated based on the throughput of jobs across the shared cluster, including objectives like fairness and job completion time, according to the Speedup Function.  
      6. **Multi-Objective Optimization Problem Modeling**: The problem is modeled as a multi-objective optimization issue, solved using genetic algorithms.  
    
      # Limitations Analysis  
      1. **Large Solution Space**: The coupling of resource allocation and job placement leads to a large solution space, resulting in slow solving speeds and difficulties in scaling to large clusters (Sia).  
      2. **Impact on Model Accuracy**: Dynamically adjusting batch size may reduce the accuracy of model tasks.  
    </details> 

* MAPA: Multi-Accelerator Pattern Allocation Policy for Multi-Tenant GPU Servers (SC 2021)[[Paper](https://dl.acm.org/doi/pdf/10.1145/3458817.3480853)]  [[Code](https://github.com/socal-ucr/MAPA)] 
  - <details>
      <summary>[Personal Notes]</summary> 
    
      # Problem Statement 
      The existing resource allocation strategies are unable to effectively address the communication patterns between complex topological interconnections and diverse ML workloads, resulting in fragmentation.
  
      # Motivations
      1. The heterogeneous connection methods (NVLink, PCIe) have different bandwidths, and the connection of accelerators is not uniform, which can be affected by the low-bandwidth PCIe links.
      2. The co-located placement method poses challenges for high-performance workloads, affecting both performance and security.
      3. There are differences in fragmentation impact and the bandwidth sensitivity of ML tasks.
  
      # Innovations 
      1. **Abstract Graph**: Abstract multiple accelerator applications and servers into smaller application graphs and larger hardware graphs. The application graph captures the demands of computational accelerators and the communication topology of workloads among accelerators (communication patterns between GPUs); the hardware graph captures the topology of the accelerator system (vertices represent computational accelerators such as GPUs, while edges represent the available hardware connections on the server, such as NVLink and PCIe).
      2. Consider fragmentation and application bandwidth sensitivity during resource allocation.
      3. Employ a graph pattern matching approach to quantify the quality of resource allocation using fractions.
  
      # Summary
      This article has provided me with some insights regarding "predicting the bandwidth required for communication." For elastic scheduling, when tasks are adaptive, the effBW method (from this article) can be used to predict the bandwidth needed for communication based on different resource allocation schemes. 

      Additionally, the author's analysis of the scheduling process has also inspired me. To maximize the overall performance of scheduled jobs, the pattern selection strategy must consider: 
      1.  The effective bandwidth allocated.
      2.  The bandwidth sensitivity of the jobs (using known bandwidth sensitivity, as shown in Figure 6, primarily through analyzing the relationship between execution time and the allocated link). 
      3.  Avoiding the situation where future bandwidth-sensitive jobs lack effective bandwidth.
  
</details> 

#### 2020
* KungFu: Making Training in Distributed Machine Learning Adaptive (OSDI 2020) [[Paper](https://www.usenix.org/conference/osdi20/presentation/mai)]
  
* Themis: Fair and Efficient GPU Cluster Scheduling (EuroSys 2020) [[Paper](https://www.usenix.org/conference/nsdi20/presentation/mahajan)]

* AntMan: Dynamic Scaling on GPU Clusters for Deep Learning [[Paper](https://www.usenix.org/system/files/osdi20-xiao.pdf)]
  - <details>
    <summary>[Personal Notes]</summary> 
    
    I got a scholar's summary of this paper on Zhihu, and I would like to share it with you here. [[Summary](https://zhuanlan.zhihu.com/p/451238714)]
    Especially Section 2.3, I will quote the content here.
    
    # Challenges & Solutions
    The design of the Local Coordinator incorporates considerations for dynamic allocation of display memory and computing resources, mainly addressing the following three issues:
    
    - Q1:How to ensure the performance of the resource-guarantee tasks?
    
    - A1: For the first question, AntMan's approach is to first ensure the stable execution of the resource-guarantee tasks; then allocate GPU memory and computational units to opportunistic tasks; finally, observe whether the performance of the resource-guarantee tasks has been affected. The method to judge whether the performance has been affected is to observe the execution time of the mini-batch.
    
    - Q2:How to handle the surge in demand for resource-guarantee tasks?
    
    - A2: If it is a memory mutation situation, first use host memory as temporary storage to reduce the use of GPU memory for opportunistic tasks; then increase the GPU memory allocation for resource-guarantee tasks. The same method applies to a surge in demand for computational units.
    
    - Q3:How to use a greedy method to maximize the performance of opportunistic tasks?

    - A3: The scenario of the last question is when multi-GPU tasks are waiting for GPU resources, the situation of GPU idle resources that have already been allocated. For this problem, AntMan's solution is to use a greedy algorithm to maximize the efficiency of GPU VRAM usage. "Figure 10" shows the practical basis for using a greedy algorithm—the performance gap perceived in terms of VRAM limitations of different models is very large, for example, reducing the SR model's 90% VRAM allocation only results in a 25% performance loss, while reducing the ResNet model's 10% VRAM causes a 60% performance loss. Therefore, AntMan prioritizes allocating GPUs to tasks that can improve performance in the opportunistic task competition scenario.
    </details> 
    
#### 2019
* Tiresias: A GPU Cluster Manager for Distributed Deep Learning (NSDI 2019) [[Paper](https://www.usenix.org/conference/nsdi19/presentation/gu)] [[Code](https://github.com/SymbioticLab/Tiresias)] Simulator

#### 2018
* Gandiva: Introspective Cluster Scheduling for Deep Learning (OSDI 2018) [[Paper](https://www.usenix.org/conference/osdi18/presentation/xiao)]


* Optimus: An Efficient Dynamic Resource Scheduler for Deep Learning Clusters (EuroSys 2018) [[Paper](https://dl.acm.org/doi/10.1145/3190508.3190517) ][[Code](https://github.com/pengyanghua/optimus)]



## Communication Scheduler
### Inter-job Communication Contention
#### 2024
* CASSINI: Network-Aware Job Scheduling in Machine Learning Clusters(NSDI 2024) [[Paper](https://www.usenix.org/conference/nsdi24/presentation/rajasekaran) ]
  - <details>
    <summary>[Personal Notes]</summary> 
    
    # Background
    In large-scale GPU training tasks, **communication overhead accounts for a significant proportion of the total training time**. However, existing schedulers (such as Themis and Pollux) mainly focus on the allocation of computing resources, while **ignoring the optimization of network communication resources**.
    
    # Challenges
    1. Current machine learning schedulers ignore the communication patterns between jobs when allocating GPU tasks, which leads to communication bottlenecks affecting training speed.

    2. How to optimize the network scheduling of distributed training jobs without modifying the underlying network protocols (such as ECN marking and congestion control)?

    3. How to automatically adjust the time shift (Time Shift) of jobs so that the computation and communication phases of multiple jobs overlap, thereby reducing network congestion?

    4. How to extend this method to be applicable to different machine learning models (such as VGG, ResNet, BERT, GPT-3, etc.) and different parallel training strategies (data parallelism, model parallelism, mixed parallelism)?
    
    # Motivation
    - **Geometric abstraction**:
      - The researchers proposed a "time loop" geometric model that maps the communication period of a job to a circle, so that the communication requirements of each iteration can be optimized through the rotation angle to minimize overlap.
      - By optimizing the Time-Shift of jobs, CASSINI makes the calculation and communication phases of multiple jobs staggered in time, improving network utilization.
    - **Affinity Graph**:
      - The researchers constructed a **Bipartite Graph**, in which one set of vertices represents jobs, the other set of vertices represents network links, and the weights of edges represent the communication load of jobs on the link.
      - By traversing the graph, CASSINI calculates the **optimal time offset** for all jobs, ensuring that jobs on the same network link can stagger communication phases to the greatest extent possible.
    - **Optimization method**:
      - The researchers proposed an **optimization model** to calculate the **optimal rotation angle** of the job, thereby determining the time offset value, so that the job's communication mode on the shared link achieves optimal interleaving
      </details> 

### Collective Communication 
#### 2024
* Revisiting the Time Cost Model of AllReduce (arXiv 2024)[[Paper](https://arxiv.org/pdf/2409.04202) ][[Code](https://anonymous.4open.science/r/AllreduceBenchmark-StreamEmulator-CCF4)]
  - <details>  
    <summary>[Personal Notes]</summary>  
  
      #  Background
      - AllReduce is a key communication primitive widely used in fields such as distributed machine learning (DML) and HPC, and its performance directly affects overall computational efficiency. The traditional (𝛼, 𝛽, 𝛾) model includes startup latency (𝛼), communication cost (𝛽), and computational cost (𝛾), but with the evolution of hardware and network technology, this model is difficult to accurately describe the actual time overhead of AllReduce in modern high-performance clusters.
      - (𝛼, 𝛽, 𝛾) Model: TimeCost=A×α+B×β+C×γ
        - **𝛼** represents the **startup** or **fixed delay cost**, including fixed overheads such as communication initialization and link latency.
        - **𝛽** represents the **communication cost**, which is related to the link bandwidth, i.e., the cost per unit of data transmission.
        - **𝛾** represents the **computation cost**, which is the computational overhead of processing aggregation operations (such as summation, maximum value retrieval, etc.), and is related to the computational capability of the processor.
      - Collective Communication Foundation
        - **Parameter Server**: Each processor aggregates data to a central node (parameter server), which performs the reduction operation and then broadcasts the result back to all nodes. **This method is usually less efficient because the central node is prone to become a bottleneck, and the resources of other nodes are not fully utilized.**
        - **Ring-Allreduce: (reduceScatter-allGather):** The data is divided into multiple blocks, and each node is responsible for the reduction of its local data portion only in the first phase (ReduceScatter). Subsequently, in the second phase (AllGather), each node exchanges its reduced data blocks with other nodes to complete the global reduction operation.
        - **Recursive Halving and Doubling (RHD):** In each step, processors are paired off, and they exchange half of their data to complete local reduction. The doubling phase uses a pairing strategy similar to recursive halving, but at this point, the data blocks exchanged in each step keep doubling until each processor has the complete reduced result. That is, the doubling phase propagates the reduction results in reverse, and it also requires log₂(N) steps.
      # Motivations
      - Traditional models are insufficient to meet modern cluster demands:
        - **Increased memory access and NIC bandwidth** result in memory access overhead that is no longer negligible.
        - **Incast issues caused by high concurrency communication** (a large number of nodes sending data to one or a few nodes simultaneously) lead to the target nodes being overwhelmed, which is due to network congestion or switch buffer being rapidly filled, resulting in significant increased latency.
      - Accurate Modeling to Guide Algorithm Design Issues:
        - **Constructing heuristic AllReduce scheme generation methods for tree topology**. This is because it is an NP-hard problem under any topology.
        - The generation method based on GenModel – namely **GenTree**, is a heuristic algorithm, mainly designed for automatically generating efficient AllReduce plans under tree topology, rather than simply selecting an existing AllReduce method. It generates communication plans that adapt to the current cluster characteristics by weighing the two indicators of incast and memory access, thereby improving overall communication efficiency.
      ## Theoretical Foundation Framework
      - The (𝛼, 𝛽, 𝛾) model adopted by the cutting-edge work divides the AllReduce process into three parts: initiation, communication, and computation. 
      - Based on a large number of experiments, two new cost items are added to the original model:
        - Incast Cost Item: Reflects the delay caused by data aggregation (incast) in large-scale concurrent communication. 
        - Memory Access Cost Item: As the network speed increases, the cost of memory reading and writing during the execution of computational tasks by computing devices (CPU/GPU) gradually becomes an indispensable factor.
    </details> 
