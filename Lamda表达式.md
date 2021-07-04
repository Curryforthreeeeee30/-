# Lamda表达式

### Why Lambda?



![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202020-09-26%20200706.png)

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202020-09-26%20200739.png)

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202020-09-26%20200806.png)

```
package com.kuang.Lambda;

public class TestLambda {

    //3.静态内部类
    static class Like2 implements ILike{

        @Override
        public void Lambda() {
            System.out.println("I like Lambda2");
        }
    }

    public static void main(String[] args) {


        ILike like = new Like();
        like.Lambda();

        like = new Like2();
        like.Lambda();

        //4.局部内部类
        class Like3 implements ILike{

            @Override
            public void Lambda() {
                System.out.println("I like Lambda3");
            }
        }
        like = new Like3();
        like.Lambda();

        //5.匿名内部类
        like = new ILike() {
            @Override
            public void Lambda() {
                System.out.println("I like Lambda4");
            }
        };
        like.Lambda();

        //6.用lambda表达式简化

        like = () -> {
            System.out.println("I like Lambda5");
        };
        like.Lambda();
    };

}


//1.函数式接口
interface ILike{

    public abstract void Lambda();//也可以不加public abstract

}

//2.实现类
class Like implements ILike{

    @Override
    public void Lambda() {
        System.out.println("I like Lambda1");
    }
}
package com.kuang.Lambda;

public class TestLambda02 {

    public static void main(String[] args) {

        ILove love = null;

        //lambda标准表达式
        love = (int a, int b) -> {
            System.out.println("I love you! -->" + a);
            System.out.println("I love you! -->" + b);
        };
        love.love(520, 502);

        //简化参数类型
        love = (a, b) -> {
            System.out.println("I love you! -->" + a);
            System.out.println("I love you! -->" + b);
        };
        love.love(520, 502);
        //总结：
        /*
        * 只有当参数为一个并且代码行数只有一行时，才可以去掉花括号，如果有多行，必须用代码块包裹
        * 前提是接口必须为函数式接口
        * 多个参数也可以去掉参数类型，要去掉就都去掉，必须加上括号
        * */

    }

}



interface ILove{
    void love(int a, int b);
}
```