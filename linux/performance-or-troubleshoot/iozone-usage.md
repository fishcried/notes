iozone是一个文件系统的benchmark工具，可以测试不同的操作系统中文件系统的读写性能。可以测试Read, write, re-read,re-write, read backwards, read strided, fread, fwrite, random read,pread, mmap, aio\_read, aio_write等等不同的模式下的硬盘的性能.

![](/img/iozone_overview.png)

**特性**

- ANSII C source
- POSIX async I/O
- Mmap() file I/O
- Normal file I/O
- Single stream measurement
- Multiple stream measurement
- Distributed fileserver measurements (Cluster)
- POSIX pthreads
- Multi-process measurement
- Excel importable output for graph generation
- Latency plots
- 64bit compatible source
- Large file compatible
- Stonewalling in throughput tests to eliminate straggler effects
- Processor cache size configurable
- Selectable measurements with fsync, O_SYNC
- Builds for: AIX, BSDI, HP-UX, IRIX, FreeBSD, Linux, OpenBSD, NetBSD, OSFV3, OSFV4, OSFV5, SCO OpenServer, Solaris, MAC OS X, Windows (95/98/Me/NT/2K/XP

**读写模式说明**

- Write: 测试向一个新文件写入的性能。当一个新文件被写入时，不仅仅是那些文件中的数据需要被存储，还包括那些用于定位数据存储在存储介质的具体位置的额外信息。这些额外信息被称作“元数据”。它包括目录信息，所分配的空间和一些与该文件有关但又并非该文件所含数据的其他数据。拜这些额外信息所赐，Write的性能通常会比Re-write的性能低。
- Re-write: 测试向一个已存在的文件写入的性能。当一个已存在的文件被写入时，所需工作量较少，因为此时元数据已经存在。Re-write的性能通常比Write的性能高。
- Read: 测试读一个已存在的文件的性能。
- Re-Read: 测试读一个最 近读过的文件的性能。Re-Read性能会高些，因为操作系统通常会缓存最 近读过的文件数据。这个缓存可以被用于读以提高性能。
- Random Read: 测试读一个文件中的随机偏移量的性能。许多因素都可能影响这种情况下的系统性能，例如：操作系统缓存的大小，磁盘数量，寻道延迟和其他。
- Random Write: 测试写一个文件中的随机偏移量的性能。同样，有许多因素可能影响这种情况下的系统性能，例如：操作系统缓存的大小，磁盘数量，寻道延迟和其他。
- Random Mix: 测试读写一个文件中的随机偏移量的性能。许多因素可能影响这种情况下的系统性能运作，例如：操作系统缓存的大小，磁盘数量，寻道延迟和其他。这个测试只有在吞吐量测试模式下才能进行。每个线程/进程运行读或写测试。这种分布式读/写测试是基于round robin 模式的。最好使用多于一个线程/进程执行此测试。
- Backwards Read: 测试使用倒序读一个文件的性能。这种读文件方法可能看起来很可笑，事实上，有些应用确实这么干。MSC Nastran是一个使用倒序读文件的应用程序的一个例子。它所读的文件都十分大（大小从G级别到T级别）。尽管许多操作系统使用一些特殊实现来优化顺序读文件的速度，很少有操作系统注意到并增强倒序读文件的性能。
- Record Rewrite: 测试写与覆盖写一个文件中的特定块的性能。这个块可能会发生一些很有趣的事。如果这个块足够小（比CPU数据缓存小），测出来的性能将会非常高。如果比CPU数据缓存大而比TLB小，测出来的是另一个阶段的性能。如果比此二者都大，但比操作系统缓存小，得到的性能又是一个阶段。若大到超过操作系统缓存，又是另一番结果。
- Strided Read: 测试跳跃读一个文件的性能。举例如下：在0偏移量处读4Kbytes，然后间隔200Kbytes,读4Kbytes，再间隔200Kbytes，如此反复。此时的模式是读4Kbytes，间隔200Kbytes并重复这个模式。这又是一个典型的应用行为，文件中使用了数据结构并且访问这个数据结构的特定区域的应用程序常常这样做。
许多操作系统并没注意到这种行为或者针对这种类型的访问做一些优化。同样，这种访问行为也可能导致一些有趣的性能异常。一个例子是在一个数据片化的文件系统里，应用程序的跳跃导致某一个特定的磁盘成为性能瓶颈。
- Fwrite: 测试调用库函数fwrite()来写文件的性能。这是一个执行缓存与阻塞写操作的库例程。缓存在用户空间之内。如果一个应用程序想要写很小的传输块，fwrite()函数中的缓存与阻塞I/O功能能通过减少实际操作系统调用并在操作系统调用时增加传输块的大小来增强应用程序的性能。
这个测试是写一个新文件，所以元数据的写入也是要的。
- Frewrite:测试调用库函数fwrite()来写文件的性能。这也是一个执行缓存与阻塞写操作的库例程。是缓存在用户空间之内。如果一个应用程序想要写很小的传输块，fwrite()函数中的缓存与阻塞I/O功能可以通过减少实际操作系统调用并在操作系统调用时增加传输块的大小来增强应用程序的性能。
这个测试是写入一个已存在的文件，由于无元数据操作，测试的性能会高些。
- Fread:测试调用库函数fread()来读文件的性能。这是一个执行缓存与阻塞读操作的库例程。缓存在用户空间之内。如果一个应用程序想要读很小的传输块，fwrite()函数中的缓存与阻塞I/O功能能通过减少实际操作系统调用并在操作系统调用时增加传输块的大小从而增强应用程序的性能。
- Mmap:许多操作系统支持mmap()的使用来映射一个文件到用户地址空间。映射之后,对内存的读写将同步到文件中去。这对一些希望将文件当作内存块来使用的应用程序来说很方便。一个例子是内存中的一块将同时作为一个文件保存在于文件系统中


**常用选项**

- -a 全面测试，比如块大小它会自动加
- -i N 用来选择测试项, 比如Read/Write/Random 比较常用的是0 1 2,可以指定成-i 0 -i 1 -i2.这些别的详细内容请查man
  - 0=write/rewrite
  - 1=read/re-read
  - 2=random-read/write
  - 3=Read-backwards
  - 4=Re-write-record
  - 5=stride-read
  - 6=fwrite/re-fwrite
  - 7=fread/Re-fread
  - 8=random mix
  - 9=pwrite/Re-pwrite
  - 10=pread/Re-pread
  - 11=pwritev/Re-pwritev
  - 12=preadv/Re-preadv
- 大小控制
  - -r block size 指定一次写入/读出的块大小，貌似不能和-g一起使用
  - -s file size 指定测试文件的大小  该文件的大小一般要大于-r的大小，否则报错，除非使用了-t这个参数
- -f filename 指定测试文件的名字,完成后会自动删除(这个文件必须指定你要测试的那个硬盘中)
- -F file1 file2... 指定多线程下测试的文件名
- -t 单节点时指线程数，集群时指节点数
- -Rb 指输出xls格式的结果
- -G 同步模式，一般同-B -o一起使用
- -D 异步模式，一般同-B -o一起使用
- -n 测试的文件最小大小
- -g 测试的文件最大大小，一般要求是系统内存的2倍及以上，使用-g的时候最好和-a一起使用

# 安装(linux下)

```
wget  http://www.iozone.org/src/current/iozone3_430.tar
tar -xf iozone3_430.tar  && cd iozone_3_430/src/current
make linux
```

# 举例

```
#测试往/mnt/iozone下面写和读4g大小文件的性能，并把测试结果输出到当前目录的test1.txt文件中  
./iozone -s 4G -r 1m  -i 0 -i 1 /mnt/iozone/test.rar ./test1.txt   

#相比上一个测试，下面的测试输出的结果文件是xls格式的文件   
./iozone -s 4G -r 1m  -i 0 -i 1 /mnt/iozone/test.rar -Rb ./test1.xls                                                            #从512M的文件开始一直测试到4G的文件      
./iozone -a -n 512m -g 4G  -i 0  /mnt/iozone -Rb ./test1.xls  
```

# io优化因素

- journaling
- 调度算法
- io参数调整
- 文件系统


# 参考资料

1. [Linux性能优化之IO子系统](http://liaoph.com/linux-system-io/)
