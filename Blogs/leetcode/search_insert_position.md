### 1. code
```c++
#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;

class Solution {
   public:
    int searchInsert(vector<int>& nums, int target) {
        return binary_search_left_bound(nums, target);
    }

   public:
    int binary_search_left_bound(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size() - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (target < nums[mid]) {
                right = mid - 1;
            } else if (target > nums[mid]) {
                left = mid + 1;
            } else if (target == nums[mid]) {
                right = mid - 1;// if search tht left bound,or not return mid
            }
        }
        return left;
    }
    int binary_search_right_bound(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size() - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (target > nums[mid]) {
                left = mid + 1;
            } else if (target < nums[mid]) {
                right = mid - 1;
            } else if (target = nums[mid]) {
                left = mid + 1;// if search tht right bound,or not return mid
            }
        }
        return left;
    }
};
```
### 2. key points
* binary search
* `left` bound and `right` bound
  * left boun
    ```c++
    else if (target == nums[mid]) {
        right = mid - 1;// if search tht left bound,or not return mid
    }
  * right bound
    ```c++
    else if (target == nums[mid]) {
        left = mid + 1;// if search tht right bound,or not return mid
    }
* no duplicated elements
    ```c++
    else if (target == nums[mid]) {
        return mid;// if search tht right bound,or not return mid
    }
    ```