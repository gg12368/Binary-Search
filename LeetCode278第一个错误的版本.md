278. 第一个错误的版本
你是产品经理，目前正在带领一个团队开发新的产品。不幸的是，你的产品的最新版本没有通过质量检测。由于每个版本都是基于之前的版本开发的，所以错误的版本之后的所有版本都是错的。
假设你有 n 个版本 [1, 2, ..., n]，你想找出导致之后所有版本出错的第一个错误的版本。
你可以通过调用 bool isBadVersion(version) 接口来判断版本号 version 是否在单元测试中出错。实现一个函数来查找第一个错误的版本。你应该尽量减少对调用 API 的次数。

示例:
给定 n = 5，并且 version = 4 是第一个错误的版本。
调用 isBadVersion(3) -> false
调用 isBadVersion(5) -> true
调用 isBadVersion(4) -> true
所以，4 是第一个错误的版本。 

方法：二分查找 
不难看出，这道题可以用经典的二分查找算法求解。我们通过一个例子，来说明二分查找如何在每次操作中减少一半的搜索空间，以此减少时间复杂度。
场景一：isBadVersion(mid) => false
 1 2 3 4 5 6 7 8 9
 G G G G G G B B B       G = 正确版本，B = 错误版本
 |       |       |
left    mid    right
场景一中，isBadVersion(mid) 返回 false，因此我们知道 mid 左侧（包括自身）的所有版本都是正确的。
所以我们令 left=mid+1，把下一次的搜索空间变为 [mid+1,right]。
场景二：isBadVersion(mid) => true
 1 2 3 4 5 6 7 8 9
 G G G B B B B B B       G = 正确版本，B = 错误版本
 |       |       |
left    mid    right
场景二中，isBadVersion(mid) 返回 true，因此我们知道 mid 右侧（不包括自身）的所有版本的不可能是第一个错误的版本。
所以我们令right=mid，把下一次的搜索空间变为 [left,mid]。

public int firstBadVersion(int n) {
    int left = 1;
    int right = n;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (isBadVersion(mid)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }
    return left;
}

