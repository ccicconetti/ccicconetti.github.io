---
title: "Software"
layout: page
---

I strongly believe that the tools used for research activities should be made publicly available to the scientific community for

1. validation through peer review, 
2. reproducibility of results, and in general 
3. the advancement of science without forcing practitioners to reimplement the wheel at the beginning of every new research project.

_Therefore, all the software that I developed which could be of interest to the research community is available under a permissive open source license (often MIT), together with the scripts to produce the experimental data published that have been included in publications._

Here is a list of open source projects grouped by topic:

- [Serverless](#serverless)
- [EDGELESS](#edgeless)
  - [ServerlessOnEdge](#serverlessonedge)
  - [ETSI MEC Mx2](#etsi-mec-mx2)
  - [ETSI MEC/QKD](#etsi-mecqkd)
  - [Uncoordinated serverless access](#uncoordinated-serverless-access)
- [Quantum networks](#quantum-networks)
  - [qperf](#qperf)
  - [NetSquid quantum routing modules](#netsquid-quantum-routing-modules)
  - [QueeR](#queer)
- [Miscellanea](#miscellanea)
  - [factorial2kr](#factorial2kr)
  - [Kafka HDD](#kafka-hdd)

You are welcome to use the software, in which case I would appreciate a citation to one of my relevant papers (as indicated below).
If you do not find sufficient documentation to use the tools, or there is some incompatibility with newer environments, please let me know.

## Serverless

## EDGELESS

[EDGELESS](https://edgeless-project.eu/) is a collaborative project
funded by the European Union under the Horizon Europe framework
programme, with the goal of developing a serverless computing
framework for decentralized resource-constrained edge nodes.

The [source code](https://github.com/edgeless-project/edgeless)
is available under a MIT license on GitHub.

The software is developed in [Rust](https://www.rust-lang.org/)
and it users [WebAssembly](https://webassembly.org/) as lightweight
run-time environment for function execution and [gRPC](https://grpc.io/)
for internal communications.

### ServerlessOnEdge

[Serverless on Edge](https://github.com/ccicconetti/serverlessonedge)
is a framework to distribute stateless tasks (a.k.a.) lambda functions
among multiple serverless platforms, with partial integration with
[Apache OpenWhisk](https://openwhisk.apache.org/) and
[faasd](https://github.com/openfaas/faasd).
It also includes an experimental support of QUIC via Facebook's
[proxygen](https://github.com/facebook/proxygen) and
[mvfst](https://github.com/facebookincubator/mvfst) libraries.

If you use the software in your research please cite this paper:

> Cicconetti, C., Conti, M., & Passarella, A. (2020).
> A Decentralized Framework for Serverless Edge Computing in the Internet of Things.
> IEEE Transactions on Network and Service Management, 18(2), 2166–2180.
> https://doi.org/10.1109/tnsm.2020.3023305

### ETSI MEC Mx2

[uiiit::etsimec](https://github.com/ccicconetti/etsimec) is a
work-in-progress implementation of the Mx2 ETSI MEC API in modern C++,
with a [gRPC](https://grpc.io/) north-bound interface.

It has the following internal dependencies:

- [uiiit::rest](https://github.com/ccicconetti/rest) wrapper of the
[REST SDK from Microsoft](https://github.com/Microsoft/cpprestsdk),
used in uiiit::etsimec
- [uiiit::support](https://github.com/ccicconetti/support) collection
of utility classes and gRPC wrappers, using in uiiit::etsimec

If you use the software in your research please cite this paper:

> Cicconetti, C., Conti, M., Passarella, A., & Sabella, D. (2020).
> Toward Distributed Computing Environments with Serverless Solutions in Edge Systems.
> IEEE Communications Magazine, 58(3), 40–46
> https://doi.org/10.1109/MCOM.001.1900498

### ETSI MEC/QKD

In [this repository](https://github.com/ccicconetti/etsi-mec-qkd) you can find an implementation of the Mx2 ETSI MEC API in Rust, developed within the Italian project QUANCOM on quantum-secure communications.
The software is intended as a starting point to write a full MEC orchestrator for the optimization of resource allocation in an edge network where some nodes are provided with Quantum Key Distribution (QKD) devices.

### Uncoordinated serverless access

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

If you use the software in your research please cite this paper:

> Cicconetti, C., Conti, M., & Passarella, A. (2020).
> Uncoordinated access to serverless computing in MEC systems for IoT.
> Computer Networks, 172, 107184.
> https://doi.org/10.1016/j.comnet.2020.107184

## Quantum networks

### qperf

A quantum link performance measurement tool, winner of the [Quantum Internet Application Challenge 2023](https://quantuminternetalliance.org/2023/11/21/qia-concludes-quantum-internet-application-challenge-2023-names-best-submission/), see reference implementation [GitHub](https://github.com/ccicconetti/qperf) implemented with [SquidASM](https://github.com/QuTech-Delft/squidasm).


### NetSquid quantum routing modules

Quantum networking experiments with [NetSquid](https://netsquid.org/) ([GitHub](https://github.com/ccicconetti/netsquid))

If you use the software in your research please cite this paper:

> Cicconetti, C., Conti, M., & Passarella, A. (2021).
> Request Scheduling in Quantum Networks.
> IEEE Transactions on Quantum Engineering, 2, 2–17.
> https://doi.org/10.1109/TQE.2021.3090532

### QueeR

[QueeR](https://github.com/ccicconetti/queer) is a quantum end-to-end entanglement routing simulator, written in C++, to evaluate the performance of networks of quantum repeaters to enable end-to-end entanglement of qubits in remote nodes (e.g., for distributed/blind quantum computing, QKD, or distributed consensus).

If you use the software in your research please cite this paper:

> C. Cicconetti, M. Conti, and A. Passarella (2023)
> Service differentiation and fair sharing in distributed quantum computing
> Elsevier Pervasive and Mobile Computing
> https://doi.org/10.1016/j.pmcj.2023.101758

## Miscellanea

### factorial2kr

[factorial2kr](https://github.com/ccicconetti/factorial2kr) is a
Python script to perform factorial 2^kr analysis.

### Kafka HDD

[kafka-hdd](https://github.com/ccicconetti/kafka-hdd) is a repository that contains scripts for the automated execution of experiments with [Kafka](https://kafka.apache.org/).
