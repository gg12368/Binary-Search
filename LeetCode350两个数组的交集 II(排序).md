350. 两个数组的交集 II
给定两个数组，编写一个函数来计算它们的交集。

示例 1：
输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2,2]
示例 2:
输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[4,9]
 
说明：
输出结果中每个元素出现的次数，应与元素在两个数组中出现次数的最小值一致。
我们可以不考虑输出结果的顺序。

方法：排序
如果两个数组是有序的，则可以便捷地计算两个数组的交集。
首先对两个数组进行排序，然后使用两个指针遍历两个数组。
初始时，两个指针分别指向两个数组的头部。
每次比较两个指针指向的两个数组中的数字，如果两个数字不相等，则将指向较小数字的指针右移一位，如果两个数字相等，将该数字添加到答案，并将两个指针都右移一位。
当至少有一个指针超出数组范围时，遍历结束。


class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        int length1 = nums1.length, length2 = nums2.length;
        int[] intersection = new int[Math.min(length1, length2)];
        int index1 = 0, index2 = 0, index = 0;
        while (index1 < length1 && index2 < length2) {
            if (nums1[index1] < nums2[index2]) {
                index1++;
            } else if (nums1[index1] > nums2[index2]) {
                index2++;
            } else {
                intersection[index] = nums1[index1];
                index1++;
                index2++;
                index++;
            }
        }
        return Arrays.copyOfRange(intersection, 0, index);
    }
}
复杂度分析:
时间复杂度：O(mlogm+nlogn)，其中 m 和 n 分别是两个数组的长度。
对两个数组进行排序的时间复杂度是O(mlogm+nlogn)，遍历两个数组的时间复杂度是 O(m+n)，因此总时间复杂度是 O(mlogm+nlogn)。
空间复杂度：O(min(m,n))，其中 m 和 n 分别是两个数组的长度。为返回值创建一个数组 intersection，其长度为较短的数组的长度。
不过在 C++ 中，我们可以直接创建一个 vector，不需要把答案时一个额外的数组中，所以这种实现的空间复杂度为 O(1)。

结语:
如果nums2的元素存储在磁盘上，磁盘内存是有限的，并且你不能一次加载所有的元素到内存中。那么就无法高效地对nums2进行排序，因此推荐使用方法一而不是方法二。
在方法一中，nums2 只关系到查询操作，因此每次读取 nums2中的一部分数据，并进行处理即可。

