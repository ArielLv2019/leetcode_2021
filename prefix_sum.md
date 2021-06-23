## 1248-count-number-of-nice-subarrays
```
Given an array of integers nums and an integer k. A continuous subarray is called nice if there are k odd numbers on it.

Return the number of nice sub-arrays.

 

Example 1:

Input: nums = [1,1,2,1,1], k = 3
Output: 2
Explanation: The only sub-arrays with 3 odd numbers are [1,1,2,1] and [1,2,1,1].
Example 2:

Input: nums = [2,4,6], k = 1
Output: 0
Explanation: There is no odd numbers in the array.
Example 3:

Input: nums = [2,2,2,1,2,2,1,2,2,2], k = 2
Output: 16
```
```
Method1: 用前缀和
```
```cpp
class Solution {
public:
    int numberOfSubarrays(vector<int>& nums, int k) {
        // 求nums的和数组： sum[i]=nums[0,...i-1]的和
        vector<int> sum(nums.size()+1, 0);
        
        for(int i = 0; i < nums.size(); i++){
            sum[i+1] = sum[i] + nums[i]%2;
        }

        //sum里的值范围为[0~n],统计sum每个值的出现次数
        vector<int> count(sum.size(), 0);
        for(int i = 0; i < sum.size(); i++){
            count[sum[i]]++;
        }

        int res = 0;
        for(int i = 1; i < sum.size(); i++){
            if(sum[i] - k >= 0){ //防止越界
                res += count[sum[i]-k];
            }
        }
        return res;
    }
};
```
