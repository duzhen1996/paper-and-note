# 看的论文以及对应的笔记

《Tachyon Memory Throughput IO for Cluster Computing Frameworks》

> 讲述了一个基于内存文件系统的计算框架，在用户程序外面再包一层程序，把整个计算过程映射到分布式的内存文件系统之上，大幅提高计算速度。并且为了保证存储的可靠性，没有使用多副本的冗余备份，而是将数据文件的变化过程记录下来，对于丢失文件，使用已有文件+用户用于数据处理的程序来进行恢复。

《Tachyon: Reliable, Memory Speed Storage for Cluster Computing Frameworks》

>这个文章是对于Tachyon的一个完整的设计与实现，非常具体。从这篇文章中我们可以知道Tachyon是一个另起炉灶的结果，他的目标就是取代现有的存储层（虽然Tachyon的持久层可能使用的还是现有的文件系统）。所有的文件一开始都会放在内存中，这些文件会定期或者在内存快满的时候从内存checkpoint到持久化存储中。当上层计算框架获取不到内存中的文件的时候就会根据checkpoint+文件谱系关系将文件恢复出来。因为一开始文件都是放在内存中，所以就实现了高吞吐量，特别是在文件录入的时候。