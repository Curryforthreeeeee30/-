# CharSequence详情介绍

### 转载



[https://blog.csdn.net/taojin12/article/details/85760432?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522160171300319726892462767%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=160171300319726892462767&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_v2~rank_v28_p-3-85760432.pc_first_rank_v2_rank_v28_p&utm_term=CharSequence&spm=1018.2118.3001.4187](https://blog.csdn.net/taojin12/article/details/85760432?ops_request_misc=%7B%22request%5Fid%22%3A%22160171300319726892462767%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=160171300319726892462767&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_v2~rank_v28_p-3-85760432.pc_first_rank_v2_rank_v28_p&utm_term=CharSequence&spm=1018.2118.3001.4187)

请看一个简单例子：

```
package com.kuang;

public class TestCharSequence {
    public static void main(String[] args) {
        CharSequence charSequence = new String("abcd");
        CharSequence charSequence1 = charSequence.subSequence(0,2);
        System.out.println(charSequence1);
    }
}
```