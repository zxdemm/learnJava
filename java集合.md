# java集合

## 1. 大纲

![img](https://img-blog.csdn.net/20180803184611883?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZlaXlhbmFmZmVjdGlvbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

![img](https://img-blog.csdn.net/20180803195348216?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZlaXlhbmFmZmVjdGlvbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

## 2.Collection接口

![img](https://img-blog.csdn.net/20180803193423722?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZlaXlhbmFmZmVjdGlvbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

当然还有一个Collections类，这个类就像Math类一样，都是静态方法，直接调用

* Collections.sort(Collection c)：参数是一个集合
* Collections.reverse（）：反转
* Collections.copy（List l1, List l2):l2的内容复制l1,而且会覆盖同一索引下的元素

### 2.1 List接口：

![img](https://img-blog.csdn.net/20180803201736883?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZlaXlhbmFmZmVjdGlvbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

1. 有序性、可重复性、按索引存取
2. 实现类：ArrayList、Vector、LinkedList
3. ArrayList：初始容量为10，每次扩大0.5倍+1个。

### 2.2 Set集合：

#### 1. HashSet：

1. 可存储null元素，底层通过HashMap实现。

2. 初始容量为16，每次扩容为一倍

3. 线程不安全，效率高

4. 元素的唯一性是靠所存储元素类型是否重写hashCode()和equals()方法来保证的

5. 它的几个常用方法：

   ```java
   add(E e):return true/false
   //该方法底层是调用hashmap的put方法，put中的<k:e, value:PRESENT>
   value是一个常量，为一个new Object。就是为了对比在map中有没有一个key是传入的参数。
   remove():return boolean
   ```

### 2. LinkHashSet：

1. 线程不安全，初始容量为16
2. 一个哈希表与链表的结合，而且是双向链表

## 2.3 Map集合：

### 1. hashmap：

put方法详解：![img](https://upload-images.jianshu.io/upload_images/18871813-be251e9d34de0d19.png)

2. put方法如果是更新了原来的值，则会返回旧的值，如果插入的是新的值，则会返回null
3. 如果table中的一个下标对应的链表的长度超过8以后就会变成红黑树，如果再次缩短到长度6则会变成链表
4. 线程不安全，性能是最好的。
5. 作为key的对象，必须实现hashcode和equals方法
6. remove():返回boolean
7. map.getOrDefault(key, value): 如果map中有这个key，则返回map中key对应的值，否则返回value这个默认值

Iterator : 迭代器，用来遍历集合

## 2.4 Comparable接口：

1. 当java中程序员自己编写的类要进行排序时，需要在该类实现comparable接口，否则会编译出错
2. 重写 int compareTo方法，这是一个泛型方法，传入的参数类型是该类的同种类型
3. 当返回值为0时，java会以为这两个对象是相同的，则不会把比较的对象放入集合； 返回值大于0时，则当前的对象即已经在集合中的对象会放到后面； 返回值小于0时，则相反。