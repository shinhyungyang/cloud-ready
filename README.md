# Cloud-Ready Configuration for Yahoo Streaming Benchmarks

Code licensed under the Apache 2.0 license. See LICENSE file for terms.

### Motivation
Yahoo streaming framework is the first result to create a benchmark for state-of-the-art Big Data streaming platforms. However, currently available Yahoo streaming benchmark only runs on a single node setup. Preparing the State and Scalability paper for AutoDaSP 2017, I was able to come up with a production-ready Cloud configuration for Yahoo streaming benchmark

### Prerequisites
From Yahoo's official repository on GitHub, [the revision](https://github.com/yahoo/streaming-benchmarks/tree/b073202b04baa640840a09b206c101996c112b95) committed on Nov 23 2016 is used. This configuration requires 30 nodes on Cloud computing platform. I recommend to use [Google Compute Engine](https://cloud.google.com/compute). Each node is configured with 16 vCPUs and 24 GB main memory in my Cloud setup.

### Applying Patches
Patch files is going to be provided in this repository very soon. You may apply a patch file to the base Yahoo streaming benchmark according to the table below:

| Instance_Name          | Patch_Name    | Internal_IP  |
| ---------------------- |:-------------:| ------------:|
| streaming-group-0-0001 | zk.patch      | 10.140.0.101 |
| streaming-group-0-0002 | zk.patch      | 10.140.0.102 |
| streaming-group-0-0003 | zk.patch      | 10.140.0.103 |
| streaming-group-0-0004 | redis.patch   | 10.140.0.104 |
| streaming-group-0-0005 | kafka.patch   | 10.140.0.105 |
| streaming-group-0-0006 | kafka.patch   | 10.140.0.106 |
| streaming-group-0-0007 | kafka.patch   | 10.140.0.107 |
| streaming-group-0-0008 | kafka.patch   | 10.140.0.108 |
| streaming-group-0-0009 | kafka.patch   | 10.140.0.109 |
| streaming-group-0-0010 | master.patch  | 10.140.0.110 |
| streaming-group-0-0011 | slave.patch   | 10.140.0.111 |
| streaming-group-0-0012 | slave.patch   | 10.140.0.112 |
| streaming-group-0-0013 | slave.patch   | 10.140.0.113 |
| streaming-group-0-0014 | slave.patch   | 10.140.0.114 |
| streaming-group-0-0015 | slave.patch   | 10.140.0.115 |
| streaming-group-0-0016 | slave.patch   | 10.140.0.116 |
| streaming-group-0-0017 | slave.patch   | 10.140.0.117 |
| streaming-group-0-0018 | slave.patch   | 10.140.0.118 |
| streaming-group-0-0019 | slave.patch   | 10.140.0.119 |
| streaming-group-0-0020 | slave.patch   | 10.140.0.120 |
| streaming-group-0-0021 | dg.patch      | 10.140.0.121 |
| streaming-group-0-0022 | dg.patch      | 10.140.0.122 |
| streaming-group-0-0023 | dg.patch      | 10.140.0.123 |
| streaming-group-0-0024 | dg.patch      | 10.140.0.124 |
| streaming-group-0-0025 | dg.patch      | 10.140.0.125 |
| streaming-group-0-0026 | dg.patch      | 10.140.0.126 |
| streaming-group-0-0027 | dg.patch      | 10.140.0.127 |
| streaming-group-0-0028 | dg.patch      | 10.140.0.128 |
| streaming-group-0-0029 | dg.patch      | 10.140.0.129 |
| streaming-group-0-0030 | dg.patch      | 10.140.0.130 |

### Contact
Please open a new issue to contact the author.
