# Lambda表达式

如果有一个接口只有一个抽象方法，那它就是一个函数式接口。

当你要实现的这个类实现这个接口时，而且用一次而已，那就可以用Lambda表达式

```java
public class Lambda {
    public static void main(String[] args) {
        //用实现类
        ILikeAble like = new Like();
        like.like();

        //用Lambda实现
        like = ()->{
            System.out.println("i like Lambda");
        };
        like.like();
    }

}
//函数式接口
interface ILikeAble {
    public abstract void like();
}
//实现类
class Like implements ILikeAble{
    @Override
    public void like(){
        System.out.println("i like 实现类");
    }
}
```

