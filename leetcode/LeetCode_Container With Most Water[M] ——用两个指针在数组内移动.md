><font size =5 color=#22aa22>我现在在做一个叫《leetbook》的开源书项目，把解题思路都同步更新到github上了，需要的同学可以去看看
地址：https://github.com/hk029/leetcode
这个是书的地址：https://hk029.gitbooks.io/leetbook/

>![这里写图片描述](http://img.blog.csdn.net/20160417165037477)

011. Container With Most Water[M]
---

#**问题**
<font size=4>Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

<font size=4>Note: You may not slant the container. 

#**思路**
<font size=4>首先要明确一个我之前一直理解错的，它的题目是<font color=red>随意找2个木板构成木桶，容量最大，</font>我之前以为是所有的木板已经在它的位置上了，然后找其中容量最大的——你加的水是可以漫过中间比较短的板子的。

<font size=4>如果按题意来，就简单了。

<font size=4>我们用两个指针来限定一个水桶，left,right。
<font size=4>h[i]表示i木板高度。
<font size=4>Vol_max表示木桶容量最大值
><font size=4>由于桶的容量由最短的那个木板决定：
	Vol = min(h[left],h[right]) * (right - left)

- <font size=4>left和right分别指向两端的木板。
- <font size=4>left和right都向中央移动，每次移动left和Right中间高度较小的（因为反正都是移动一次，宽度肯定缩小1，这时候只能指望高度增加来增加容量，肯定是替换掉高度较小的，才有可能找到更大的容量。）
- <font size=4>看新桶子的容量是不是大于Vol_max，直到left和right相交。


<font size=4>代码如下：
```java
public class Solution {
    public int maxArea(int[] height) {
       int l = 0,r = height.length-1;
       int i = height[l] > height[r] ? r:l;
       int vol,vol_max = height[i]*(r-l);
       while(l < r)
       {
           if(height[l] < height[r])  l++;
           else r--;
           vol = Math.min(height[l],height[r]) * (r - l);
           if(vol > vol_max)     vol_max = vol;
       }
       return vol_max;
    }
}

```


