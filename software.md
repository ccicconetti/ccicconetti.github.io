---
title: "Software"
layout: page
---

## Serverless On Edge (NEW)

[Serverless on Edge](https://github.com/ccicconetti/serverlessonedge) is a framework to distribute stateless tasks (a.k.a.) lambda functions among multiple serverless platforms, with partial integration with [Apache OpenWhisk](https://openwhisk.apache.org/).

It has been developed as part of the research activities that have produced the following scientific articles:

- [Architecture and performance evaluation of distributed computation offloading in edge computing](simpat.md) in _Simulation Modelling Practice and Theory (Elsevier)_
- [Low-latency distributed computation offloading for pervasive environments](percom2019.md) presented at _IEEE PerCom 2019_
- [An architectural framework for serverless edge computing: Design and emulation tools](cloudcom2018.md) presented at _IEEE CloudCom 2018_

## uiiit::etsimec

[uiiit::etsimec](https://github.com/ccicconetti/etsimec) is a
work-in-progress implementation of ETSI MEC APIs in modern C++,
with a [gRPC](https://grpc.io/) north-bound interface.

It has the following internal dependencies:

- [uiiit::rest](https://github.com/ccicconetti/rest) wrapper of the
[REST SDK from Microsoft](https://github.com/Microsoft/cpprestsdk),
used in uiiit::etsimec
- [uiiit::support](https://github.com/ccicconetti/support) collection
of utility classes and gRPC wrappers, using in uiiit::etsimec

## factorial2kr

[factorial2kr](https://github.com/ccicconetti/factorial2kr) is a
Python script to perform factorial 2^kr analysis.

## uncoordinated serverless access

A [numerical tool](https://github.com/ccicconetti/markovsim/) to
compute the steady-state average delay of clients in a serverless
environment, where the servers behave as M/M/1 processes with
Processor Sharing policy.

The simulator assumes that every client is associated to exactly
two servers, called primary and secondary.  While using the primary
for its lambda function calls, it probes the secondary with a given
probability: if the secondary is found to response faster, then it
becomes the new primary.

The software is written for Python 2.7 and it requires
[numpy](https://numpy.org/) and [scipy](https://www.scipy.org/).
