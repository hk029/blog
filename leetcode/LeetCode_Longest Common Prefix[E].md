><font size =5 color=#22aa22>我现在在做一个叫《leetbook》的开源书项目，把解题思路都同步更新到github上了，需要的同学可以去看看
地址：https://github.com/hk029/leetcode
这个是书的地址：https://hk029.gitbooks.io/leetbook/

>![这里写图片描述](http://img.blog.csdn.net/20160417165037477)

014.Longest Common Prefix[E]
---

#**问题**
<font size=4>Write a function to find the longest common prefix string amongst an array of strings.

<font size=4>Subscribe to see which companies asked this question

#**思路**
<font size=4>这个没啥思路的，怎么都要两重循环，因为是最长公共子串，随便找一个(一般是第一个作为基准)，然后拿拿的首部慢慢去匹配后面的字符串就行了。
```java
public class Solution {
    public String longestCommonPrefix(String[] strs) {
        String s = "";
        if(strs.length == 0)
            return "";
        for(int i = 0; i < strs[0].length();i++)
        {
            char c = strs[0].charAt(i);
            for(int j = 1;j < strs.length;j++)
            {
                if(i >= strs[j].length() || strs[j].charAt(i) != c)
                    return s;
            }
            s += c;
        }
        return s;
    }
}
```

