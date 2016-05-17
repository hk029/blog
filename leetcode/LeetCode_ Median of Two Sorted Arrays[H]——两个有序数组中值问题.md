><font size =5 color=#22aa22>我现在在做一个叫《leetbook》的开源书项目，把解题思路都同步更新到github上了，需要的同学可以去看看
地址：https://github.com/hk029/leetcode
这个是书的地址：https://hk029.gitbooks.io/leetbook/

>![这里写图片描述](http://img.blog.csdn.net/20160417165037477)

004. Median of Two Sorted Arrays[H]
---


#**题目**
There are two sorted arrays nums1 and nums2 of size m and n respectively. Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

#**分析**
这个题目是非常的常见，而且有特别多的变形。特别是在当前大数据的环境下，如何快速查找第i个元素有很现实的意义。如果想看分治的思路，建议直接看这个文章：[【分步详解】两个有序数组中的中位数和Top K问题](http://blog.csdn.net/hk2291976/article/details/51107778)
##**思路1——遍历合并数组**
很简单的思路：就是遍历两个数组，在里面找到第i个大元素，这个应该还是比较简单的，时间复杂度O(m+n)。

用2个变量分别指向两个数组，每次取较小的一个，然后将其指针后移动。但是这里有个问题，就是奇偶判断，如果是奇数，中位数是num[mid]，但是如果是偶数，是(num[mid]+num[mid-1])/2。这里我的做法是把num[mid]看作(num[mid]+num[mid])/2。如果是偶数-1,奇数-0。

```c++
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        if(nums1.size() == 0)
            return MedofArray(nums2);
        if(nums2.size() == 0)
            return MedofArray(nums1);    
        vector<int> num3;
        int size = (nums1.size()+nums2.size());
        int mid = size/2;
        int flag = !(size%2);
        int i,m1,m2,cur;
        double a,b;
        for(i = m1 = m2 = 0;i < size;i++)
        {   
            a = m1 < nums1.size()?nums1[m1]:INT_MAX;//过界处理
            b = m2 < nums2.size()?nums2[m2]:INT_MAX;//过界处理
            //cout<<i<<" a "<<a<<" b "<<b<<endl;
            if(a < b)
            {
                num3.push_back(nums1[m1]);
                m1++;
            }
            else
            {
                num3.push_back(nums2[m2]);
                m2++;
            }
            if(i == mid)
                break;
        }
        return (num3[mid]+num3[mid-flag])/2.0;
    }
    double MedofArray(vector<int>& nums)
    {
        int mid = nums.size()/2;
        int flag = !(nums.size()%2);
        return (nums[mid]+nums[mid-flag])/2.0;
    }
};
```


##**思路2——分治 ***
<font color=orange>重点来了!!</font>
这是一个很经典的Divide & Conquer的题目，关键就在如何划分。这里引用stellari 的高分答案，觉得他这个讲的特别好：
由于篇幅很长，我把这个移动到了这篇文章: [【分步详解】两个有序数组中的中位数和Top K问题](http://blog.csdn.net/hk2291976/article/details/51107778)


###**代码**
```c++
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int n = nums1.size();
        int m = nums2.size();
        if(n > m)   //保证数组1一定最短
            return findMedianSortedArrays(nums2,nums1);
        int L1,L2,R1,R2,c1,c2,lo = 0, hi = 2*n;  //我们目前是虚拟加了'#'所以数组1是2*n长度
        while(lo <= hi)   //二分
        {
            c1 = (lo+hi)/2;  //c1是二分的结果
            c2 = m+n- c1;
            L1 = (c1 == 0)?INT_MIN:nums1[(c1-1)/2];   //map to original element
            R1 = (c1 == 2*n)?INT_MAX:nums1[c1/2];
            L2 = (c2 == 0)?INT_MIN:nums2[(c2-1)/2];
            R2 = (c2 == 2*m)?INT_MAX:nums2[c2/2];

            if(L1 > R2)
                hi = c1-1;
            else if(L2 > R1)
                lo = c1+1;
            else
                break;
        }
        return (max(L1,L2)+ min(R1,R2))/2.0;
    }
};
```


