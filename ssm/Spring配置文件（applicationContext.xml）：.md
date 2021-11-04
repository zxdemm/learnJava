Spring配置文件（applicationContext.xml）：

在bean中有一个属性叫scope。

<img src="C:\Users\HDULAB601\AppData\Roaming\Typora\typora-user-images\image-20211103162947613.png" alt="image-20211103162947613" style="zoom:67%;" />

默认为singleton，说明每次spring从容器中拿出的都是同一个对象

prototype说明每次拿出的对象都是new出来的

```java
配置文件中的scope="prototype"
<bean id="userDao" class="second.dao.impl.UserDaoimpl.UserDaoimpl" scope="prototype"></bean>

//输出为false
 ApplicationContext app = new ClassPathXmlApplicationContext("applicationContext.xml");
        UserDao userDao1 = (UserDao) app.getBean("userDao");
        UserDao userDao2 = (UserDao) app.getBean("userDao");
        System.out.println(userDao1);
        System.out.println(userDao2);
        System.out.println(userDao1 == userDao2);
```

当属性为singleton时，bean中的对象是在加载配置文件时就会创建。

```java
执行这步的时候就会生成userDao这个对象
ApplicationContext app = new ClassPathXmlApplicationContext("applicationContext.xml");
```

当属性为prototype时，只有app.getBean时才会创建一个对象

<img src="C:\Users\HDULAB601\AppData\Roaming\Typora\typora-user-images\image-20211103164651074.png" alt="image-20211103164651074" style="zoom:67%;" />

<img src="C:\Users\HDULAB601\AppData\Roaming\Typora\typora-user-images\image-20211103165552897.png" alt="image-20211103165552897" style="zoom:67%;" />