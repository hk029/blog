><font size =5 color=#22aa22>我现在在做一个叫《leetbook》的开源书项目，把解题思路都同步更新到github上了，需要的同学可以去看看
地址：https://github.com/hk029/leetcode
这个是书的地址：https://hk029.gitbooks.io/leetbook/

>![这里写图片描述](http://img.blog.csdn.net/20160417165037477)

012. Integer to Roman[M]
---

#<font style="font-weight:bold" color=#00AEAE >**问题**
<font size=4>Given an integer, convert it to a roman numeral.

Input is guaranteed to be within the range from 1 to 3999.

#<font style="font-weight:bold" color=#00AEAE>**思路**
<font size=4>分析罗马数字的规律：
|Symbol |Value|
|-|-|
|I |	1|
|V |	5
|X 	|10
|L 	|50
|C |	100
|D| 	500
|M| 	1,000

<font size=4>上面是罗马数字所有的符号。
<font size=4>罗马数字的规则：
<font size=4>一般情况下，从左到右从大到小排，字母代表的数字累加。
<font size=4>比如：
><font size=4>XII = 12
>MDCCLXVI= 1000+500+100+100+50+10+5+1 

<font size=4>但是有特殊情况，就是，如果数字的范围在大数减小数的范围内，则会出现小数在大数前面的情况，代表（大数-小数）
><font size=4>IV = 5-1
IX= 10 - <font size=4>1 = 9
<font size=4>XL = 50-10 = 40

|Symbol |Value|
|-|-|
|IV |	4|
|IX |	9
|XL 	|40
|XC 	|90
|CD |	400
|CM| 	900


##<font color=#9393FF size=6>**思路1——循环**
<font size=4>一旦把所有可能的情况符号情况都列举出来了，就好做了。
<font size=4>我们现在拿到一个数N

1. <font size=4> 我们就去表里面找不超过它的最大的数x，
2. <font size=4> 然后把它入我们的输出字符串中，然后将数N-=x，
3. <font size=4> 继续执行这个操作，直到N=0

```java
public class Solution {
    public String intToRoman(int num) {
        int list[] = {1000,900,500,400,100,90,50,40,10,9,5,4,1};
        String chars[] = {"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};
        int i = 0;
        String out="";
        while(num > 0)
        {
            for(;i < list.length;i++)
                if(num >= list[i])
                    break;
            out+=chars[i];
            num -= list[i];
        }
        return out;
    }
}
```


##<font color=#9393FF size=6>**思路2——查表**
<font size=4>还有个更极端的方案，就是，把每位上可能出现的情况都列举出来，剩下的，只用查表就行了。


```java
public class Solution {
  public static String intToRoman(int num) {
        String M[] = {"", "M", "MM", "MMM"};
        String C[] = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
        String X[] = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
        String I[] = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};
        return M[num/1000] + C[(num%1000)/100] + X[(num%100)/10] + I[num%10];
    }
}

```

