# Lucky的算法小记

## 1 算法基础

### 1.1 二分查找系列

总结：插入位置、左右边界、算术平方根、完全平方数等涉及到有序数组查找的基本都可用二分优化。

#### 1、插入位置

left, right] left <= right；target不存在时插入位置：left 或者 right + 1；[left, right) left < right；target不存在时插入位置：right

#### 2、左右边界

https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/

```shell
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        int start = -1, end = -1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                right = mid - 1;
            }
            if (nums[mid] < target) {
                left = mid + 1;
            }
            if (nums[mid] > target) {
                right = mid - 1;
            }
        }
        // 判断有无出界
        if (right < nums.length - 1 && left >= 0 && nums[right + 1] == target) {
            start = right + 1;
        }
        right = nums.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                left = mid + 1;
            }
            if (nums[mid] < target) {
                left = mid + 1;
            }
            if (nums[mid] > target) {
                right = mid - 1;
            }
        }
        if (right < nums.length && left - 1 >= 0 && nums[left - 1] == target) {
            end = left - 1;
        }

        return new int[]{start, end};
    }
}
```

#### 3、x的算数平方根

[1, x]二分查找,mid * mid <=x && (mid + 1) * (mid + 1) > x，注意long和int类型转换