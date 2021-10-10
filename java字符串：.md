# java字符串：

1. 字符串＋数字：也是字符串

2. 字符串 + 数字a+ 数字b：字符串ab，a+b是不会运行的

3. 数字a+ 数字b + 字符串：先a+b = c ，输出a字符串

   * 当“+”操作出现在字符串中时，这个符号是拼接作用，而不是加法作用。

4. 当字符串怎么转化成数字时：

   ```
   “1” -> 1 :用Integer.valueof()方法
   其实每一个大的封装类都有这个valueOf方法来对它们进行转换
   ```

5. +=这个运算符默认有强制转换

6. 字符串s转换为char数组用s.toCharArray()

7. 字符串equals()方法原理需要了解

   * 先判断==，是否指向同一个内存地址
   * 变成char数组，一个个比较过去

8. java为了方便，会将直接赋值的string放到常量池中，之后其他直接赋值的string全都指向同一个内存地址，除非new一个新的string

   # StringBuilder

   1. 该类被final修饰，不能在被继承
   2. 继承自AbstractStringBuilder
   3. 自带的变量为value数组，存放字符，count存放字符的个数
   4. 最牛逼的是append方法，当传入的是null、true、false，这些全部变成“null”等字符串的形式，直接加到value数组的末尾
   5. 初始化时，value数组默认大小为16
   6. 与StringBuffer的区别：StringBuffer比较安全，单线程操作，StringBuilder效率高，多线程操作，可能会导致出错

   # AbstractStringBuilder

   1. append方法创始人，
   2. 有一个expandCapacity的方法来扩容，扩容之后会用Arrays.copy的方法来赋值
   3. delete（int start，int end）:从开始到结束，end大于count时，end变成count
   4. replace（int start， int end， string str）：把该对象中的开始位置到end-1的位置替换为str，且不管str有多长，str会全部加入进去
   5. 