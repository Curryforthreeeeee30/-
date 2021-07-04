# @RequestBody详解

### @RequestBody介绍



 1、@RequestBody主要***用来接收前端传递给后端的json字符串中的数据\***的（请求体中的数据）。由于***GET方式没有请求体\***，所以使用@RequestBody接受数据的时候，前端不能用GET方式提交数据，而是用***POST方式\***提交。

 2、在后端的同一个接口中，@RequestBody和@ResquestParam()可以同时使用，@RequestBody最多只能有一个，而@ResquestParam()可以有多个。

 3、@RequestBody 接收的是***请求体\***里面的数据；而@RequestParam接收的是***key-value\***里面的参数。

 4、如果参数前写了@RequestParam(xxx)，那么前端必须有对应的xxx名字才行(不管其是否有值，当然可以通过设置该注解的required属性来调节是否必须传)，如果没有xxx名的话，那么请求会出错，报400。

 5、如果参数前不写@RequestParam(xxx)的话，那么就前端可以有可以没有对应的xxx名字才行，如果有xxx名的话，那么就会自动匹配；没有的话，请求也能正确发送。

如果后端参数是一个对象，且该参数前是以@RequestBody修饰的，那么前端传递json参数时，必须满足以下要求：

- 后端@RequestBody注解对应的类在将HTTP的输入流(含请求体)装配到目标类(即：@RequestBody后面的类)时，会根据json字符串中的key来匹配对应实体类的属性。
- json字符串中，如果value为””的话，后端对应的属性如果是String类型的，那么接收到的就是””;如果后端属性是Integer、Double类型的话，后端接收到的就是null。
- json字符串中，如果value为null的话，后端对应收到的就是null。

测试：

准备工作：

1、新建一个SpringBoot项目

2、写一个pojo类：User

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-05-08_101428.png)

由于这里无需进行数据库操作，所以直接写接口：

1、@RequestBody直接用***String\***去接收前端传过来的json数据：

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-05-08_101531.png)

测试：

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-05-08_101327.png)

2、@RequestBody以***简单对象\***接收前端传过来的json数据：

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-05-08_101940.png)

测试：

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-05-08_101918.png)

3、@RequestBody以***复杂对象\***接收前端传过来的json数据：

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/20180709160616858.png)

4、@RequestBody和@RequestParam()同时使用：

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-05-08_103035.png)

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-05-08_103001.png)

5、@RequestBody接收请求体中的json数据；不加注解接收URL中的数据并组装为对象，不加注解就相当于是@RequestParam。

但是如果是@RequestParam(“token”)，那么前端一定要有对应的字段才行，否则会报错！

测试：

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-05-08_103902.png)

没带token，请求之后报错！

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-05-08_103810.png)

总结：

 后端@RequestBody注解对应的类在将HTTP的输入流(含请求体)装配到目标类(即:@RequestBody后面的类)时，会根据json字符串中的key来匹配对应实体类的属性，如果匹配一致且json中的该key对应的值 符合(或可转换为)实体类的对应属性的类型要求时，会调用实体类的setter方法将值赋给该属性。

@RequestParam:

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-05-08_105907.png)