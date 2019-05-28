# OOM-Demo
一些OOM异常测试Demo

对于堆溢出，没有什么需要特别交代的，主要就是对象的创建问题。
需要注意的是栈和永久代、元空间的异常情况。

对于栈来说，分为栈深和新建线程导致空间不足的问题。
栈深可以理解为分配好的线程，递归调用导致线程内存不足，此时会报SStackOverflowError。
栈空间不足，无法新建线程时，则会报OutOfMemoryError: unable to create new native thread。

重点需要区分的是永久代和元空间。

对于JVM1.7来说，常量池是属于永久代的一部分，而整个永久代其实共享的是JVM虚拟机中的内存。

因为一些历史原因，Oracle需要考虑HotSpot和JRockit的统一，以及解决永久代的溢出问题，所以，JVM1.8将永久代废弃，
改用元空间。

对于jvm1.8来说，常量池从永久代移到了堆中，其余部分（如静态变量、类信息等）则转移至元空间。

注意永久代和元空间不仅仅是常量池的区别，永久代使用的JVM虚拟机的内存，而元空间占用的则是直接内存。
并且，元空间还有自由扩展的属性(在每次GC后，如元空间不足，会自动加大内存)。







