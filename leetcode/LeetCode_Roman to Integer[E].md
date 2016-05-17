><font size =5 color=#22aa22>我现在在做一个叫《leetbook》的开源书项目，把解题思路都同步更新到github上了，需要的同学可以去看看
地址：https://github.com/hk029/leetcode
这个是书的地址：https://hk029.gitbooks.io/leetbook/

>![这里写图片描述](http://img.blog.csdn.net/20160417165037477)

013. Roman to Integer
---

#**问题**
<font size=4>Given a roman numeral, convert it to an integer.

<font size=4>Input is guaranteed to be within the range from 1 to 3999.


<font size=4>Subscribe to see which companies asked this question

#**思路**
<font size=4>首先要知道罗马数字的规律：
|Symbol |Value|
|-|-|
|I |	1|
|V |	5
|X 	|10
|L 	|50
|C |	100
|D| 	500
|M| 	1,000

<font size=4>然后还有一个规则是，罗马数字从左自右相加，但是如果小数字A在大数字B之前，表示B-A

<font size=4>VI = 5+1 = 6
<font size=4>IV = 5-1 = 4

<font size=4>因此，利用2个变量保存当前数字和之前的数字就行了。因为这题很简单，用python比较方便，我就用python做的

```python
class Solution(object):
    def romanToInt(self, s):
        sum=0
        pre = 2000
        cur = 0
        Map = {'I':1,'V':5,'X':10,'L':50,'C':100,'D':500,'M':1000}
        for i in range(len(s)):
            cur = Map[s[i]]
            sum = sum+Map[s[i]]
            if cur > pre :
                sum = sum-2*pre
            pre = cur
        return sum
```


