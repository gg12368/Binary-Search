349. 两个数组的交集
给定两个数组，编写一个函数来计算它们的交集。

示例 1：
输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2]
示例 2：
输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[9,4]

public int[] intersection(int[] nums1, int[] nums2) {
  Set<Integer> set = new HashSet<>();
  Arrays.sort(nums2);
  for (int target : nums1) {
    if (binarySearch(nums2, target) && !set.contains(target)) {
      set.add(target);
    }
  }
  int index = 0;
  int[] res = new int[set.size()];
  for (int num : set) {
    res[index++] = num;
  }
  return res;
}
public boolean binarySearch(int[] nums, int target) {
  int left = 0, right = nums.length - 1;
  while (left <= right) {
    int mid = left + (right - left) / 2;
    if (nums[mid] == target) {
      return true;
    } else if (nums[mid] > target) {
      right = mid - 1;
    } else if (nums[mid] < target) {
      left = mid + 1;
    }
  }
  return false;
}

