# sysbench性能测试

# overview

# 安装

```
./autogen.sh

apt-get install automake libtool libmysqlclient-dev
./configure


make
make install
```

# 使用

**语法**

```
   sysbench [common-options] --test=name [test-options] command
```

| name      | 含义           |
|-----------|----------------|
| `cpu`     | cpu性能测试    |
| `threads` | 线程调度测试   |
| `memory`  | 内存性能测试   |
| `mutex`   | 互斥锁性能测试 |
| `oltp`    | OLTP测试       |
| `fileio`  | 文件I/O测试    |

| command   | 用途                                               |
|-----------|----------------------------------------------------|
| `prepare` | 进行准备工作,比如对io进行测试时,需要创建必要的文件 |
| `run`     | 真正进行测试                                       |
| `cleanup` | 清理现场,清楚垃圾文件                              |
| `help`    | 获取帮助信息                                       |

**常用参数**

| 选项             | 说明                   | 默认值
|------------------|------------------------|----------|
| `--num-threads`  | 工作线程数             | 1        |
| `--max-requests` | 请求上线,0表示不做限制 | 10000    |
| `--test`         | 执行测试项目           | 手动指定 |
| `--debug`        | 输出更多的debug信息    | off      |


**cpu**

| 参数            | 用途                 | 默认值
|-----------------|----------------------|--------|
| `cpu-max-prime` | primes generator上界 | 10000  |

```
sysbench --test=cpu --cpu-max-prime=2000 run
```


**threads**

| 参数            | 用途                  | 默认值
|-----------------|-----------------------|--------|
| `thread-yields` | 每次请求产生的线程数  | 1000   |
| `thread-locks`  | 每个线程持有的locks数 | 8      |

```
sysbench --test=threads --num-threads=64 --thread-yields=100 --thread-locks=2 run
```

**io**

| 参数                        | 用途                                                                   | 默认值
|-----------------------------|------------------------------------------------------------------------|----------|
| `--file-num=N`              | number of files to create                                              | 128      |
| `--file-block-size=N`       | block size to use in all IO operations                                 | 16384    |
| `--file-total-size=SIZE`    | total size of files to create                                          | 2G       |
| `--file-test-mode=STRING`   | test mode {seqwr, seqrewr, seqrd, rndrd, rndwr, rndrw}                 | 手动指定 |
| `--file-io-mode=STRING`     | file operations mode {sync,async,mmap}                                 | sync     |
| `--file-extra-flags=STRING` | additional flags to use on opening files {sync,dsync,direct}           | []       |
| `--file-fsync-freq=N`       | do fsync() after this number of requests (0 - don't use fsync())       | 100      |
| `--file-fsync-all=[on/off]` | do fsync() after each write operation                                  | off      |
| `--file-fsync-end=[on/off]` | do fsync() at the end of test                                          | on       |
| `--file-fsync-mode=STRING`  | which method to use for synchronization {fsync, fdatasync}             | fsync    |
| `--file-merged-requests=N`  | merge at most this number of IO requests if possible (0 - don't merge) | 0        |
| `--file-rw-ratio=N`         | reads/writes ratio for combined test                                   | 1.5      |


```
sysbench --test=fileio --num-threads=16 --file-total-size=1000M --file-test-mode=rndrw prepare
sysbench --test=fileio --num-threads=16 --file-total-size=1000M --file-test-mode=rndrw run
sysbench --test=fileio --num-threads=16 --file-total-size=1000M --file-test-mode=rndrw cleanup

sysbench --test=fileio --num-threads=1 --file-total-size=1000M --file-test-mode=rndrw prepare
sysbench --test=fileio --num-threads=1 --file-total-size=1000M --file-test-mode=rndrw run
sysbench --test=fileio --num-threads=1 --file-total-size=1000M --file-test-mode=rndrw cleanup
```

**mutex**

| 参数              | 用途                                          | 默认值
|-------------------|-----------------------------------------------|--------|
| `--mutex-num=N`   | total size of mutex array                     | 4096   |
| `--mutex-locks=N` | number of mutex locks to do per thread        | 50000  |
| `--mutex-loops=N` | number of empty loops to do inside mutex lock | 10000  |

```
sysbench --test=mutex --num-threads=16 \--mutex-num=1024 --mutex-locks=10000 --mutex-loops=5000 run
```

**memory**

| 参数                          | 用途                                          | 默认值
|-------------------------------|-----------------------------------------------|--------|
| `--memory-block-size=SIZE`    | size of memory block for test                 | 1K     |
| `--memory-total-size=SIZE`    | total size of data to transfer                | 100G   |
| `--memory-scope=STRING`       | memory access scope {global,local}            | global |
| `--memory-hugetlb=[on/off]`   | allocate memory from HugeTLB pool             | off    |
| `--memory-oper=STRING`        | type of memory operations {read, write, none} | write  |
| `--memory-access-mode=STRING` | memory access mode {seq,rnd}                  | seq    |


```
sysbench --test=memory --num-threads=512 --memory-block-size=262144 --memory-total-size=32G run
```

**oltp**

```
./sysbench --mysql-host=1.2.3.4 --mysql-port=3317 --mysql-user=tpcc --mysql-password=tpcc \
 --test=tests/db/oltp.lua --oltp_tables_count=10 --oltp-table-size=100000 --rand-init=on prepare
```


# 变更记录

| Why                       | Who       | When       |
|---------------------------|-----------|------------|
| 创建文件,提醒日后完善内容 | fishcired | 2015-04-24 |
| 对sysbench使用进行整理    | fishcired | 2015-06-16 |
