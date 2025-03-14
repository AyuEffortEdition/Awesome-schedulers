# Awesome-schedulers
Records of some awesome resource scheduling papers.

I am a Phd in Chongqing University and my research topic is MLsys, resource scheduler(Job & Communication), computer vision(semi-supervised Learning).

😎 I am actively maintaining this list. 💪
## Resource Scheduler
### Scheduling for DL Training Workloads
#### 2024
* CASSINI: Network-Aware Job Scheduling in Machine Learning Clusters(NSDI 2024) [[Paper](https://www.usenix.org/conference/nsdi24/presentation/rajasekaran) ]

* Blox: A Modular Toolkit for Deep Learning Schedulers (EuroSys 2024) [[arXiv](https://arxiv.org/pdf/2312.12621)]  [[Code](https://github.com/msr-fiddle/blox)]

* Heet: Accelerating Elastic Training in Heterogeneous  Deep Learning Clusters (ASPLOS 2024) [[Paper](https://dl.acm.org/doi/10.1145/3620665.3640375)]

#### 2023
* GPU Cluster Scheduling for Network-Sensitive Deep Learning (arXiv 2024) [[arXiv](https://arxiv.org/abs/2401.16492)]

* Sia: Heterogeneity-aware, goodput-optimized ML-cluster scheduling (SOSP 2023) [[Paper](https://dl.acm.org/doi/10.1145/3600006.3613175)]


* Lyra: Elastic Scheduling for Deep Learning Clusters (EuroSys 2023) [[Paper](https://dl.acm.org/doi/10.1145/3552326.3587445)]

* Shockwave: Fair and Efficient Cluster Scheduling for Dynamic Adaptation in Machine Learning (NSDI 2023) [[Paper](https://www.usenix.org/conference/nsdi23/presentation/zheng)]  [[Code](https://github.com/uw-mad-dash/shockwave)]

* Lucid: A Non-intrusive, Scalable and Interpretable Scheduler for Deep Learning Training Jobs (ASPLOS 2023) [[Paper](https://dl.acm.org/doi/10.1145/3575693.3575705)] [[Code](https://github.com/S-Lab-System-Group/Lucid)]
  - Code may invalid...

* ElasticFlow: An Elastic Serverless Training Platform for Distributed Deep Learning (ASPLOS 2023) [[Paper](https://dl.acm.org/doi/10.1145/3575693.3575721)]

#### 2022
* Looking Beyond GPUs for DNN Scheduling on Multi-Tenant Clusters (OSDI 2022) [[Paper](https://www.usenix.org/conference/osdi22/presentation/mohan)] [[Code](https://github.com/msr-fiddle/synergy) ]

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

#### 2019
* Tiresias: A GPU Cluster Manager for Distributed Deep Learning (NSDI 2019) [[Paper](https://www.usenix.org/conference/nsdi19/presentation/gu)] [[Code](https://github.com/SymbioticLab/Tiresias)] Simulator

#### 2018
* Gandiva: Introspective Cluster Scheduling for Deep Learning (OSDI 2018) [[Paper](https://www.usenix.org/conference/osdi18/presentation/xiao)]


* Optimus: An Efficient Dynamic Resource Scheduler for Deep Learning Clusters (EuroSys 2018) [[Paper](https://dl.acm.org/doi/10.1145/3190508.3190517) ][[Code](https://github.com/pengyanghua/optimus)]



## Communication Scheduler
### Collective Communication 
* Revisiting the Time Cost Model of AllReduce (arXiv 2024)[[Paper](https://arxiv.org/pdf/2409.04202) ]
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