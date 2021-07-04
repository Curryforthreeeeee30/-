# 寻找子串java

这篇blog是来源于leetcode28题——实现strStr()（[28题题目链接](https://leetcode-cn.com/problems/implement-strstr/)）

其实可以很简单地使用java语言中的substring函数和equals函数来实现，具体代码如下：

```
class Solution{
    public int strStr(String haystack, String needle){
        int len_hay = haystack.length();
        int len_nee = needle.length();
        for(int start = 0; start < len_hay-len_nee+1; start++){
            if(haystack.substring(start, start+len_nee).equals(needle)){
                return start;
            }
        }
        return -1;
    }
}
```

仔细看看，就算needle是一个空字符串，返回值是-1，也是满足题目要求的。