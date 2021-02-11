---
title: "Serverless ETSI MEC"
layout: page
---

This project within the [Ubiquitous Internet research group](http://cnd.iit.cnr.it/) is aimed at providing an open source ([MIT license](https://en.wikipedia.org/wiki/MIT_License)) implementation of serverless services in an ETSI MEC compliant edge computing domain.

Serverless computing, also called Function-as-a-Service, is an emerging paradigm where clients request the remote execution of code in a stateless manner.

Edge computing is a networked system design approach where the computation elements, traditionally located in a centralized core network or in a remote data centre, are deployed close to the users, e.g., co-located in cellular network base stations or WiFi access points.

The [ETSI MEC](https://www.etsi.org/technologies/multi-access-edge-computing) is a reference architecture and set of standard interfaces to realize a vendor-neutral interoperable edge computing network.

GitHub repositories:

- [uiiit::etsimec](https://github.com/ccicconetti/etsimec) work-in-progress implementation of ETSI MEC APIs in modern C++, with a [gRPC](https://grpc.io/) north-bound interface
- [uiiit::rest](https://github.com/ccicconetti/rest) wrapper of the [REST SDK from Microsoft](https://github.com/Microsoft/cpprestsdk), used in uiiit::etsimec
- [uiiit::support](https://github.com/ccicconetti/support) collection of utility classes and gRPC wrappers, using in uiiit::etsimec
