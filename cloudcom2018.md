---
title: "Serverless edge computing: multi-platform dispatching"
layout: page
---

Publications:

1. _A Decentralized Framework for Serverless Edge Computing in the Internet of Things_, IEEE Transactions on Network and Service Management, 2020, full paper on [IEEEXplore](https://ieeexplore.ieee.org/document/9193994), DOI: [10.1109/TNSM.2020.3023305](https://doi.org/10.1109/TNSM.2020.3023305), [arXiv](https://arxiv.org/abs/2110.10974).
2. _An architectural framework for serverless edge computing: Design and emulation tools_, [IEEE CloudCom 2018](http://cyprusconferences.org/cloudcom2018/), full paper on [IEEEXplore](https://ieeexplore.ieee.org/document/8590993), slides [here](https://www.slideshare.net/cicconetti/design-and-emulation-tools-for-serverless-edge-computing), BibTeX [here](bib/cloudcom2018.bib), DOI: [10.1109/CloudCom2018.2018.00024](https://doi.org/10.1109/CloudCom2018.2018.00024).

GitHub repository: [Serverless on Edge](https://github.com/ccicconetti/serverlessonedge)

Authors: C. Cicconetti, M. Conti and A. Passarella

### Topics

- Edge computing
- Serverless / Function-as-a-Service (FaaS)
- Simulation and modelling

### Challenge

**How to enable lightweight routing of lambda functions towards multiple platforms operating in an edge computing domain.**

### Key contribution

Our system model consists of clients in an edge computing domain wishing to perform computation offloading of their applications using a serverless paradigm.
This means that the applications consist of a sequence of remote procedure invocations, called lambda functions, that do not require a state to be installed and maintained on the remote side.
Serverless platforms are typically deployed in data centres, which means that:

1. communication between servers is fast, cheap, and reliable
2. computation resources can be easily scaled up/down with state-of-the-art technology (e.g., [kubernetes](https://kubernetes.io))

Unfortunately, in an edge network both such assumptions fail miserably:

1. communication between edge nodes may happen through (wireless) access network technologies, which have limited bandwidth and may incur significant transfer delays;
2. since the edge devices are not (anywhere) as powerful as the application servers in a data centre and there is a (potentially) high communication overhead for synchronisation, scaling the virtual machines/containers required for the execution of lambda functions is complex and expensive.

**The scientific challenge is: realising a lightweight & scalable dispatch of lambda function requests in a network made of devices with limited computational capabilities and connectivity.**

![Architecture](pictures/cloudcom2018.png)

We propose to achieve the above goal by inspiring from the Internet Protocol architecture.
In IP the routers are in charge of forwarding the packets from their source to the destination.
Since this operation must be performed as fast as possible, with some simplification, the routers decide the outgoing interface of every packet based on a highly-optimised local _forwarding table_.
Since the network topology may change over time, such table is subject to change based on the outcome of _routing protocols_, whose dynamics are much much slower than those of packet forwarding.

We do something similar.
In our system model we have:

- _e-routers_: the ingress points of the edge network to which clients connect;
- _e-computers_: the edge nodes offering their computational capabilities to host images for the execution of lambda functions from clients;
- _e-controller_: a logically centralised element that is aware of all the e-routers and e-computers in the edge domaing.

The e-controller installs _e-tables_ on the e-routers, which play the same role as the forwarding table in an IP router: every time an e-router receives a lambda function to be executed, it retrieves from the e-table the list of e-computers able to serve that function.
Such e-tables much slower than the rate at which the e-routers process lambda functions.
This allows the decision algorithm at every e-router to be fast and efficient, with no information being exchanged with its peers.
However, every e-router continuously estimates the average latency experience by lambda requests of any given type when forwarded to every possible e-computer, so as to select the best destination next time the same lambda function will be requested.
This is done by means of changing over time the _weights_ of destinations, as shown also in the example above.

Estimation of the latency is done on a per-lambda manner because different lambdas are served by different containers on the same host: one may be overloaded while another is idle.
However, if the _network_ to reach an e-computer is congested, then _all_ lambda functions there will experience a higher response times.
Unfortunately, by mere measuring the latency a e-routers, we cannot distinguish whether a high latency happens because of congestion of network vs. computation resources.
However, if the underlying network supports Software Defined Networking, the SDN controller (or any other component in charge of network monitoring) may help us in this: whenever there is congestion detection, it informs the e-controller, which in turns changes all the weights to infinity, i.e. that destination will not be considered for all its lambda functions offered.
Once the network congestion resolves, the weights will be reset to an initial value.

To summarise, the interaction between network monitoring and lambda function forwarding allows to _proactively_ respond to (temporary) network congestion before it affects the performance of the serverless services in use, whereas we rely on distributed passive probing and measurement on e-routers to _reactively_ respond to (temporary) overload of the computation resources of e-computers.

#### Scalability

As the number of e-computers in an edge computing domain grows, the size of the tables in the e-routers increase (linearly). This can become an issue if the e-routers are deployed on resource-limited devices, because of the delay introduced by the table lookup operation.

We have performed measurements on a Raspberry 3, which shows that the issue becomes non-neglible after a few thousands of entries, as can be seen in the following plot (which shows the number of dispatches per second an e-router can do on RPi3, full details on available in the IEEE Trans. on Netw. and Service Manag. paper):

![RPi3 scalability experiments](pictures/cloudcom2018-rpi3.png)

To overcome this possible limitation, we have proposed to use a two-tier hierarchical dispatching scheme: the e-router tables may contain entries not only towards e-computers (i.e., the final destination of a lambda function invocation) but also towards are e-routers, which will, in turn, forward to the final destination.

#### Integration with ETSI MEC

We have studied how to integrate the proposed solution within the [ETSI Multi-Access Edge Computing (MEC)](https://www.etsi.org/technologies/multi-access-edge-computing) architecture:

![ETSI MEC integration](pictures/cloudcom2018-etsimec.png)

A prototype of the implementation, currently limited to the `Mx2` interface, is available as _open source_ on GitHub as [uiiit::etsimec](https://github.com/ccicconetti/etsimec).

#### Integration with Apache OpenWhisk

We have developed proxy modules to allow [Apache OpenWhisk](https://openwhisk.apache.org/) applications to invoke lambda functions, which are then dispatched to one of multiple serverless systems in an edge computing domain, with no changes, see
[this page](https://github.com/ccicconetti/serverlessonedge/blob/master/docs/openwhisk_integration.md) in the Serverless on Edge framework.

### Validation

Methodology:

Performance evaluation on an emulated network in several topologies:

- line topology where an e-router on the far edge forwards lambdas to e-computers all along the line, with ideal vs. non-ideal communication links, and with vs. without network congestion in the middle of the chain
- pods topology, to mimic real Mobile Broadband Wireless Access (MBWA) deployments in urban scenarios, where powerful e-computers are located both in the "core" network and constrained e-computers are closed to the users
- ring-tree topology, with client sessions following an ON/OFF pattern and with background network traffic injected during the experiments
- 4x4 grid topology, clients (both Apache OpenWhisk and emulated) connected to external nodes and computation happening in the core nodes
- large-scale IoT scenario, based on a real deployment in Chicago ([Array of Things](8 https://arrayofthings.github.io/)), to show the effectiveness of the two-tier dispatching scheme

Tools used:

- C++ prototype implementation of e-computer (with simulated processing time), e-router, and e-computer, using [gRPC](https://grpc.io/) for all communications, both signalling and serverless function calls, see [GitHub repository](https://github.com/ccicconetti/serverlessonedge)
- [mininet](http://mininet.org/) for network emulation, with extensions to: generate the scenarios; retrieve throughput from the emulated switches; load activity from the real traces; compute shortest paths and install static flow tables in switches

[Short demo on YouTube](https://www.youtube.com/watch?v=pHryny2P864&t=), also showing how a real e-computer (with face/eyes detection) can be reached within the emulated mininet environment from an external serverless client.

We have implemented three policies in the e-router for destination selection, all tested in emulation experiments:

- **Random proportional**: next destination is selected inversely proportional to the estimated latency
- **Least impedance**: send the lamdba function to the e-computer that has the smallest estimated latency
- **Round robin**: serve the e-computers in a weight round robin manner, where the weight is the inverse of the stimate latency. _We have provided mathematical proof that this policy provides both short- and long-term fairness_

### Main findings

1. The proposed solution adapts well to fast changing computational load conditions.
  - In particular, the _round-robin policy_ achieves short- and long-term fairness
2. It is possible to combat temporary network congestion events y interacting with the underlying SDN controller.
3. Lambda function dispatching is lightweight enough to be implementd on resource-constrained devices, with negligible performance impact with several serverless platforms (i.e., e-computers).
  - With e-routing functions deployed on RPi3 device and several thousands of platforms there can be a non-negligible extra delay at the application layer, which can be reduced by adopting a two-tier hierarchical dispatching scheme.

### Future research directions

- Field testing, esp. with small devices
- Definition of architecture and protocols for realising full in-network processing, [Golem](https://golem.network/)-style

