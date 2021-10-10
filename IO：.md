# I/O：

## 1 I/O流：

1. 分为字节流与字符流， 也有阻塞型io和非阻塞型io，方向是单向的
2. 常见的字节流：FileInputStream、FileOutputStream、ObjectInputStream、ObjectOutputStream

### FileOutputStream

1. 这是字节流写入文件的。

   ```java
   FileOutputStream fie = new FileOutputStream("文件路径");
   //当第二个参数为true时，写入的数据是从文件末尾开始写的
   FileOutputStream fie = new FileOutputStream("文件路径", true);
   
   //在方法签名后面加上throws ，否则编译都不通过，或者用trycatch块
   //事实上在创建这个fie对象时，它会创建一个File的对象，然后以file这个对象作为参数操作，而file对象以“文件路径”作为参数。
   fie.write("abs".getBytes());//有三个参数，直接写阿斯克码，或者以byte数组，或者byte数组，起始索引，长度。
   
   fie.write("\r\n")//如何实现换行
   
       
   fie.close()//必须有这个关闭资源的方法。
   ```

   

### FileInputStream

1. 这是字节流读数据

   ```java
   FileInputStream fir = new FileInputStream("文件路径");
   fir.read();//当read返回的是-1时，说明文件已经读到末尾了
   int len = fir.read();//len表示这次读到的字符的阿斯克吗值
   byte[] by = new byte(1024);
   int len2 = fir.read(by);//返回的是这次读了多少字符值
   //当数据读完时，read返回的是-1
   //每次使用read（），都会在文件中读取一个数据
   ```


### BufferedInputStream And BufferedOutputStream

字节缓冲流：创建对象

```java
FileInputStream fir = new FileInputStream("文件路径");
BufferedInputStream buff = new BufferedInputStream(fir);
//然后用buff来对文件操作
buff.read();
buff.close();
```

利用字节缓冲流传输byte数组比较快

### OutputStreamWriter And InputStreamWriter

他们有子类：FileWriter and Filereader

字符流类：

```java
OutputStreamWriter out = new OutputStreamWriter(new FileOutputStream("文件路径", true));
out.write("哈哈哈");
out.close();
```

#### BufferedReader and BufferedWriter

字符缓冲流





在jdk7时，已经有改进方案了，不用在写close语句了

```java
    public static void ma(){
try(FileInputStream fileInputStream = new FileInputStream("文件路径")){
        }catch (IOException e){
            e.printStackTrace();
        }
    }
在try后面加入(),在括号里创建io对象，就能自动关闭io流释放资源，并且不会报错
```

jdk9更加简单

```java
    public static void ma1() throws IOException {
        FileInputStream fileInputStream = new FileInputStream("文件路径");
        FileOutputStream fileOutputStream = new FileOutputStream("文件路径");
        try (fileOutputStream; fileInputStream){
            
        }catch (IOException e){
            e.printStackTrace();
        }
    }
    虽然需要在方法声明后面抛出异常，但是try的括号里只要写io流的变量名就能自动释放资源了
```

