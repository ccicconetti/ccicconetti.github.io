---
title: "Stateful FaaS at the edge"
layout: page
---

C. Cicconetti, M. Conti, and A. Passarella,
_On Realizing Stateful FaaS in Serverless Edge Networks: State Propagation_,
IEEE International Conference on Smart Computing 2021 (SMARTCOMP'21).

### Resources

- conference presentation on [YouTube](https://youtu.be/gc1pQ56UMAA)
- source code and artifacts on [GitHub](https://github.com/ccicconetti/serverlessonedge/tree/master/StateSim)

### Topics

- edge computing
- serverless / Function-as-a-Service
- stateful applications

### Summary

Function-as-a-Service (FaaS) is a new programming model where a developer only writes _functions_.
They are then deployed in a run-time environment managed by a serverless platform in the cloud, which takes care of the auto-scaling of the containers that are used to execute the functions based on the instantaneous user demands.
This enables, at least in principle, infinite scalability with no burden on the developer or service provider.

![](pictures/statefulfaas-1.png)

FaaS implicitly assumes that all functions are stateless (= the output only depends on the input provided by the users), which is key to allow the serverless platform to scale up/down the number of containers dedicated to a given function.
Since not all services can be made of pure stateless functions only, the typical architecture used in serverless production systems also involves a storage system that is used to keep the applications' states: when a container is activated to execute a given stateful function, it first retrieves the state from the storage system, then it runs the function, and finally it updates the state in the storage system (if modified).

![](pictures/statefulfaas-2.png)

However, the architecture above does not suit well the structure of a typical edge network, since both compute resources on edge nodes _and_ users are distributed over the network, which may cover a large area and be made of unreliable or slow connection links.

![](pictures/statefulfaas-3.png)

Therefore, **we propose that the state of an application should remain in the edge network**.

![](pictures/statefulfaas-4.png)

To this aim, we have proposed three strategies:

1. _Pure FaaS_: State is embedded into function arguments and return value.
2. _State propagation_: State is propagated along the chain of function invocations.
3. _State local_: State is stored by the edge nodes and retrieved as needed during the function execution.

### Main findings

We have performed a large number of numerical simulations using a Monte Carlo method with artificial network topologies (generated using [Ether - Edge topology synthesizer](https://github.com/edgerun/ether)) and workloads (created with [Spar: Cluster trace generator](https://github.com/All-less/trace-generator)) to compare the three strategies proposed, and we have found that:

- State local requires the least amount of network traffic to serve the same workload. This leads to significant end-to-end response time reduction, especially at high percentiles.
- With state local, the performance of chains of function invocations is more stable as the chain size increases, whereas longer chains incur signicant degradation with the other strategies.
- A pure FaaS approach produces the worst result according to all the performance indices considered.

### Future research directions

We need to better understand the implications of the different strategies in terms of:

- the programming model and developers' APIs;
- the run-time optimization opportunities that can be exploited at a platform level.
