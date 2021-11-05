# Spring 依赖注入



# IOC控制反转

传统的程序都是自己创建new对象，程序主动创建依赖的对象。ioc有专门的容器来创建对象，即有ioc控制对象的创建。

传统程序：

<img src="https://images0.cnblogs.com/blog/289233/201501/261421378318292.jpg" alt="img" style="zoom: 67%;" />

有了ioc容器后：

<img src="https://images2017.cnblogs.com/blog/1000862/201711/1000862-20171118211621093-1086644528.png" alt="img" style="zoom:67%;" />

## DI依赖注入

业务层会调用持久层的方法，那么业务层与持久层有依赖关系。这种依赖关系交给Spring来维护。就是等待Spring将持久层对象传入业务层，用户不再去自己获取了











## 如何使用依赖注入

1. 使用set方法注入时，一定要给这个类有一个无参构造方法

   ```java
   首先在userServiceimpl中改成如下代码
   public class UserServiceimpl implements UserService {
   
       
       UserDao userDao;
       //setUserdao中的参数userDao是框架生成的
       public void setUserDao(UserDao userDao){
           this.userDao = userDao;
       }
       @Override
       public void save(){
           userDao.save();
       }
   }
   ```

   然后在配置文件中加入以下

   ```
   <bean id="userDao" class="second.dao.impl.UserDaoimpl.UserDaoimpl" ></bean>
          <bean id = "userService" class="second.service.impl.UserServiceimpl">
                 <property name="userDao" ref="userDao"></property>
                 //name中的值是setUserDao后半部分的小写：userDao
                 //ref的值就是要自动注入的对象，取得是配置文件中的id=“userDao”
          </
          bean>
   ```
   
2. 有参构造方法，不用set方法了

   ```java
   首先在userService中加入带UserDao的参数的构造函数
   public class UserServiceimpl implements UserService {
   
       UserDao userDao;
   
   
       public UserServiceimpl() {
       }
   
       public UserServiceimpl(UserDao userDao) {
           this.userDao = userDao;
       }
   
       @Override
       public void save(){
           userDao.save();
       }
   }
   ```

   在配置文件中配置以下

   ```java
   首先就是写这个bean
   <bean id="userDao" class="second.dao.impl.UserDaoimpl.UserDaoimpl" ></bean>
   <!--       使用有参构造来实现-->
          <bean id = "userService" class="second.service.impl.UserServiceimpl">
                 <constructor-arg name="userDao" ref="userDao"></constructor-arg>
          </bean>
          constructor-arg来表示使用带参的。name的值指的是public UserServiceimpl(UserDao userDao)参数的变量， ref指的是容器中id为userDao的bean
   ```

   

## 注入的不同的类型

1. 普通的类型：int、string等

   首先在userDaoimpl中加入set方法，以及对应的变量

   ```
   public class UserDaoimpl implements UserDao {
       private  String username;
       private  int age;
       public UserDaoimpl(){
           System.out.println("创建一个对象");
       }
   
       public String getUsername() {
           return username;
       }
   
       public int getAge() {
           return age;
       }
   
       public void setUsername(String username) {
           this.username = username;
       }
   
       public void setAge(int age) {
           this.age = age;
       }
   
       public void init(){
           System.out.println("初始化");
       }
       public void destory(){
           System.out.println("销毁");
       }
       @Override
       public void save() {
           System.out.println(username + "    " + age);
           System.out.println("userDao保存了");
       }
   }
   ```

   在配置文件里

   ```java
   <bean id = "userService" class="second.service.impl.UserServiceimpl">
                 <constructor-arg name="userDao" ref="userDao"></constructor-arg>
          </bean>
          <bean id="userDao" class="second.dao.impl.UserDaoimpl.UserDaoimpl" >
                 //这里会调用set方法，给参数name对应的值赋值
                 <property name="username" value="我"></property>
                 <property name="age" value="24"></property>
           </bean>
              
              
              
   ```

2. 给集合注入

   ```java
         <bean id = "userService" class="second.service.impl.UserServiceimpl">
                 <constructor-arg name="userDao" ref="userDao"></constructor-arg>
          </bean>
          <bean id="userDao" class="second.dao.impl.UserDaoimpl.UserDaoimpl" >
                 <property name="list">
                        <list>
                               <value>a aaa</value>
                               <value>bbb</value>
                               <value>ccc</value>
                        </list>
                 </property>
                 <property name="map">
                        <map>
                               <entry key="user1111" value-ref="user1"></entry>
                               <entry key="user2222" value-ref="user2"></entry>
                        </map>
                 </property>
           </bean>
           
           在这里创建两个user的bean，在项目中创建一个User类，用set方法注入，一定要有无参构造方法
          <bean id="user1" class="second.domain.User" >
                 <property name="username" value="zx"></property>
                 <property name="age" value="24"></property>
          </bean>
          <bean id="user2" class="second.domain.User">
                 <property name="username" value="zxdemm" ></property>
                 <property name="age" value="24"></property>
          </bean>
   ```

   

