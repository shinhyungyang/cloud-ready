# Light-weight, High-resolution Profiling on Data Streams

*cloud_profiler* is a native library for profiling tuples in data streams on the Cloud. Please find the link below to get the implementation artefacts of the paper "*Scalability and States: A Critical Assessment of Big Data Stream Engine Scalability and States: A Critical Assessment of Big Data Stream Engine*", which is submitted for FGCS Special Issue on New Landscapes of the Data Stream Processing in the era of Fog Computing.

* Artefacts: http://elc.yonsei.ac.kr/cloud_profiler/index.html

# Cloud-Ready Configuration for Yahoo Streaming Benchmarks

Code licensed under the Apache 2.0 license. See LICENSE file for terms.

### Motivation
Yahoo streaming framework is the first result to create a benchmark for state-of-the-art Big Data streaming platforms. However, currently available Yahoo streaming benchmark only simulates the benchmark on a single node setup. Preparing the State and Scalability paper for [Auto-DaSP 2017](http://calvados.di.unipi.it/auto-dasp-17/), I was able to come up with a production-ready Cloud configuration for Yahoo streaming benchmark.

### Prerequisites
From Yahoo's official repository on GitHub, [the revision](https://github.com/yahoo/streaming-benchmarks/tree/b073202b04baa640840a09b206c101996c112b95) committed on Nov 23 2016 is used. This configuration requires 30 nodes on Cloud computing platform. I recommend to use [Google Compute Engine](https://cloud.google.com/compute). Each node is configured with 16 vCPUs and 24 GB main memory in my Cloud setup. Please note that each node has two properties: Instance_Name and Internal_IP. Instance_Name is specific to Google Compute Engine and is used as an alias for each node. You may want to create a Cloud node manually in order to manually allocate internal IPs. Otherwise, all occurrences of IP addresses in the provided patch files need to be replaced according to your setup, in which case refer to the table below.

### Preparing the Yahoo streaming benchmark

Clone the benchmark from the official repository:

    git clone https://github.com/yahoo/streaming-benchmarks.git

Reset to the specific revision from Nov 23 2016

    cd streaming-benchmarks
    git reset --hard b073202b04baa640840a09b206c101996c112b95

Do initial download and setup of the benchmark

    ./stream-bench.sh SETUP

Setup breaks after unsuccessful download of a package. If you encounter such problem directly download packages from archive.apache.org. E.g., have a look at the case below:

    cd download-cache
    rm flink-1.1.3-bin-hadoop27-scala_2.10.tgz spark-1.6.2-bin-hadoop2.6.tgz
    wget http://archive.apache.org/dist/flink/flink-1.1.3/flink-1.1.3-bin-hadoop27-scala_2.10.tgz
    wget http://archive.apache.org/dist/spark/spark-1.6.2/spark-1.6.2-bin-hadoop2.6.tgz
    # Continue with setup
    cd ..
    ./stream-bench.sh SETUP

### Applying Patches
You may apply a patch file to your Yahoo streaming benchmark folder of each Cloud node according to the table below:

| Instance_Name          | Patch_Name    | Internal_IP  |
| ---------------------- |:-------------:| ------------:|
| streaming-group-0-0001 | zk.patch      | 10.140.0.101 |
| streaming-group-0-0002 | zk.patch      | 10.140.0.102 |
| streaming-group-0-0003 | zk.patch      | 10.140.0.103 |
| streaming-group-0-0004 | redis.patch   | 10.140.0.104 |
| streaming-group-0-0005 | kafka-1.patch | 10.140.0.105 |
| streaming-group-0-0006 | kafka-2.patch | 10.140.0.106 |
| streaming-group-0-0007 | kafka-3.patch | 10.140.0.107 |
| streaming-group-0-0008 | kafka-4.patch | 10.140.0.108 |
| streaming-group-0-0009 | kafka-5.patch | 10.140.0.109 |
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

Once you are ready with patch files, change current path to the parent of your Yahoo streaming benchmark directory and enter below command:

    cd /path/to/your/streaming-benchmarks/..
    patch -p0 --ignore-whitespace < /path/to/your/Patch_Name

### Preparing Cloud Nodes
In order to run Kafka cluster, each Kafka broker node needs a log directory. Refer to `logs.dir` attribute of the Kafka configuration file in each of your Kafka broker nodes located at `streaming-benchmarks/kafka_2.10-0.8.2.1/config`.

### Additional Installation
As soon as I was confronted with problems from using Storm's internal dev-zookeeper for setting up Zookeeper cluster, I added standalone zookeeper of the same version. Follow the instruction to add the application to the framework:

    cd streaming-benchmarks
    wget http://archive.apache.org/dist/zookeeper/zookeeper-3.4.6/zookeeper-3.4.6.tar.gz
    tar xf zookeeper-3.4.6.tar.gz
    rm zookeeper-3.4.6.tar.gz

In order to execute the benchmark's data-generator Clojure script, download and setup lein as follows:

    mkdir ~/bin
    cd ~/bin
    wget https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein
    chmod +x ./lein

Then, modify line # 19 of your `streaming-benchmarks/stream-bench.sh` to correctly locate your copy of lein.

    LEIN="/home/your_account_name/bin/lein"

### Contact
Please open a new issue to contact the author.
