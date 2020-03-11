# benchmark-asprilo-golog

## Introduction

This repository contains the data I collected for my bachelor thesis as well as the tools to replicate that data.

## Replicating the data

To replicate the results you have to make sure you installed [clingo 5.4](https://github.com/potassco/clingo) on a cluster of your choice (I ran the benchmarks on a cluster with Linux, Intel Xeon E5-2650v4 processors with 2.20GHz and 64 GB memory).

The folder `benchmark-tool` contains the test instances as well as the necessary configuration files. The test instances are located in the folder `benchmark-tool/benchmarks/`. Configuration files can be found in `benchmark-tool/runscripts/`.

### Running benchmarks

There are in total four benchmarks (see the configuration files in `benchmark-tool/runscripts/`) that have to be started one after another. Upload the folder `benchmark-tool` to the cluster and execute on of the following command per instance:

```shell
./bgen runscripts/runscript-asprilo-r2-golog.xml OR
./bgen runscripts/runscript-asprilo-r2-nogolog.xml OR
./bgen runscripts/runscript-asprilo-r5-golog.xml OR
./bgen runscripts/runscript-asprilo-r5-nogolog.xml
```

This creates a folder `output-asprilo-r{2,5}-{golog,nogolog}` that contains a shell script which will start the benchmark. Enter:

```shell
./output-asprilo-r{2,5}-{golog,nogolog}/asprilo-bmarks/zuse/start.sh
``` 

For more information about the used benchmark tool check out the corresponding [repository](https://github.com/potassco/benchmark-tool).

## Collecting the data

Download the following folder from the cluster:

```shell
benchmark-tool/output-asprilo-r{2,5}-{golog,nogolog}/asprilo-bmarks/zuse/results/ALL/asprilo-pmork-Base/
```

It contains the results of each test instance. The Python script `create-csv.py` (requires Python v3.x) extracts these informations and generates a csv file:

```shell
python3 create-csv.py ./asprilo-pmork-Base/ [OUTPUT_FILE_NAME] 100
```