---
title: "An Architectural Framework for Serverless Edge Computing: Design and Emulation Tools"
layout: page
---

Presented at [IEEE CloudCom 2018](http://cyprusconferences.org/cloudcom2018/), full paper on [IEEEXplore](https://ieeexplore.ieee.org/document/8590993), slides [here](https://www.slideshare.net/cicconetti/design-and-emulation-tools-for-serverless-edge-computing), BibTeX [here](bib/cloudcom2018.bib).

DOI: [10.1109/CloudCom2018.2018.00024](https://doi.org/10.1109/CloudCom2018.2018.00024)

### Topics

- Edge computing
- Serverless / Function-as-a-Service (FaaS)
- Simulation and modelling

### Challenge

How to enable lightweight routing of lambda functions in an edge computing domain.

### Key contribution

Our system model consists of clients in an edge computing domain wishing to perform computation offloading of their applications using a serverless paradigm.
This means that the applications consist of a sequence of remote procedure invocations, called lambda functions, that do not require a state to be installed and maintained on the remote side.
Serverless platforms are typically deployed in data centres, which means that:

1. communication between servers is fast, cheap, and reliable
2. computation resources can be easily scaled up/down with state-of-the-art technology (e.g., [kubernetes](https://kubernetes.io))

Unfortunately, in an edge network both such assumptions fail miserably:

1. communication between edge nodes may happen through (wireless) access network technologies, which have limited bandwidth and, may incur significant transfer delays
2. since the edge devices are not (anywhere) as powerful as the application servers in a data centre and there is a (potentially) high communication overhead for synchronisation, scaling the virtual machines/containers required for the execution of lambda functions is complex and expensive

**The scientific challenge is: realising a lightweight dispatch of lambda function requests in a network made of devices with limited computational capabilities and connectivity.**

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

Furthermore, if the underlying network supports Software Defined Networking (SDN)  XXX

### Main findings

### Validation methodology

We have defined three policies that can be implemented in an e-router for destination selection:

- Random proportional: next destination is selected inversely proportional to the estimated latency

- Least Impedance: send the lamdba function to the e-computer that has the smallest estimated latency

- Round Robin: serve the e-computers in a weight round robin manner, where the weight is the inverse of the stimate latency

[Short demo on YouTube](https://www.youtube.com/watch?v=pHryny2P864&t=).
