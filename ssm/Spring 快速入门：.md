Spring 快速入门：

Spring程序开发步骤：

<img src="C:\Users\HDULAB601\AppData\Roaming\Typora\typora-user-images\image-20211029163839872.png" alt="image-20211029163839872" style="zoom: 80%;" />

在Service实现层不再用new 对象了，而是通过向Spring来要一个。而且对于DaoImpl来说，利用xml来标识DaoImpl了。可以对原来的项目进行解耦

文字描述：

![image-20211029164304439](C:\Users\HDULAB601\AppData\Roaming\Typora\typora-user-images\image-20211029164304439.png)

<img src="C:\Users\HDULAB601\AppData\Roaming\Typora\typora-user-images\image-20211103161227920.png" alt="image-20211103161227920" style="zoom:67%;" />

UserDao里放的是接口

```java
public interface UserDao {
    public void save();
}
```

UserDaoimpl里是接口的实现类

```java
public class UserDaoimpl implements UserDao {
    @Override
    public void save() {
        System.out.println("savesdkafh");
    }
}
```

applicationContext.xml里是配置文件

```
id是可以随便取的，class是对应的实现类
<bean id="userDao" class="second.dao.impl.UserDaoimpl.UserDaoimpl"></bean>
```

找个测试类：

```java
public class Test {
    public static void main(String[] args) {
        ApplicationContext app = new ClassPathXmlApplicationContext("applicationContext.xml");
        UserDao userDao = (UserDao) app.getBean("userDao");
        userDao.save();

    }
}
```

