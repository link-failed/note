### LSched: A Workload-Aware Learned Query Scheduler for Analytical Database Systems

#### motivation

* impact of query scheduling:

  1. query latency
  2. query throughput

* existing approaches:

  1. **commonly used scheduling algorithms which based on heuristics:**

     * pro: easy to complement, transparent (understanable)
     * con: not optimal
     * heuristics: with simplifying assumptions, hard to consider more complex system behavior
     * e.g., FIFO, fair scheduling, short job first (SJF), highest priority first (HPF), packing, approximation algorithms

  2. **reinforcement learning for scheduling policies:**

     * attempt: Decima

       result: cannot consider database's characteristics

       e.g.,  query structure, different operators , pipelining opportunities

       treat task as black box (cannot optimize by considering the task's details and relationships with other ones)

     * use reinforcement learning for specific scheduling

     * how using the proper degree of pipelining could affect the scheduling quality:

       ![image-20220712133828980](/home/ceci/Desktop/note/papers.assets/image-20220712133828980.png)

       1. typical critical path pipelining

          a heuristic that runs the pipeline containing more aggregate work first 

       2. Decima 

          graph convolution networks (GCN)

       3. proposed learned scheduler

  3. **lever-age machine learning**

     * Quickstep & SelfTune & ...

       * tend to use ML to predict the query or task latency to make better decisions

         doesn't try to learn an entire scheduling policy

       * the scheduling policy is still based on heuristics

         not specifically built from scratch for the input workload

       * without considering other scheduling factors (e.g., parallelism degree for each query) 

#### solution: Learned Scheduler

* pros

  1. **Employing efficient physical plan features**

     e.g., fine-grained level work orders, status of running execution threads

  2. **Efficient and accurate query encoding**

     * Encoder: a customized tree convolution technique + importance weighting mechanisms from graph attention networks (GAT) 
     * goal: learn an efficient and accurate query encoding that suits the nature of our scheduling problem

  3. **Flexible scheduling decisions**

#### concepts

* dynamic analytical workloads: 

  different queries can arrive/depart at any time