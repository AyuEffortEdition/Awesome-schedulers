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

* Lucid: A Non-intrusive, Scalable and Interpretable Scheduler for Deep Learning Training Jobs (ASPLOS 2023) [[Paper](https://dl.acm.org/doi/10.1145/3575693.3575705)] [[Code](https://github.com/S-Lab-System-Group/Lucid)] Maybe invalid...

* ElasticFlow: An Elastic Serverless Training Platform for Distributed Deep Learning (ASPLOS 2023) [[Paper](https://dl.acm.org/doi/10.1145/3575693.3575721)]

#### 2022
* Looking Beyond GPUs for DNN Scheduling on Multi-Tenant Clusters (OSDI 2022) [[Paper](https://www.usenix.org/conference/osdi22/presentation/mohan)] [[Code](https://github.com/msr-fiddle/synergy) ]

#### 2021
* Pollux: Co-adaptive Cluster Scheduling for Goodput-Optimized Deep Learning (OSDI 2021) [[Paper](https://www.usenix.org/conference/osdi21/presentation/qiao)] [[Code](https://github.com/petuum/adaptdl)]
  
* <details>  
  <summary>Personal Notes</summary>  
  
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

#### 2020
* KungFu: Making Training in Distributed Machine Learning Adaptive (OSDI 2020) [[Paper](https://www.usenix.org/conference/osdi20/presentation/mai)]
  
* Themis: Fair and Efficient GPU Cluster Scheduling (EuroSys 2020) [[Paper](https://www.usenix.org/conference/nsdi20/presentation/mahajan)]

#### 2019
* Tiresias: A GPU Cluster Manager for Distributed Deep Learning (NSDI 2019) [[Paper](https://www.usenix.org/conference/nsdi19/presentation/gu)] [[Code](https://github.com/SymbioticLab/Tiresias)] Simulator

#### 2018
* Gandiva: Introspective Cluster Scheduling for Deep Learning (OSDI 2018) [[Paper](https://www.usenix.org/conference/osdi18/presentation/xiao)]


* Optimus: An Efficient Dynamic Resource Scheduler for Deep Learning Clusters (EuroSys 2018) [[Paper](https://dl.acm.org/doi/10.1145/3190508.3190517) ][[Code](https://github.com/pengyanghua/optimus)]


