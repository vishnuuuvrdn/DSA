<h1>Problem:</h1>
<a href="https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/" target="_blank">Solve here!</a>

<strong>Find Minimum in Roatated Sorted Array</strong>
<br/> <br/>
Suppose an array of length n sorted in ascending order is rotated between 1 and n times. For example, the array nums = [0,1,2,4,5,6,7] might become:<br><br>

<ul>
<li>[4,5,6,7,0,1,2] if it was rotated 4 times.</li>
<li>[0,1,2,4,5,6,7] if it was rotated 7 times.</li>
</ul>

Notice that rotating an array [a[0], a[1], a[2], ..., a[n-1]] 1 time results in the array [a[n-1], a[0], a[1], a[2], ..., a[n-2]].
Given the sorted rotated array nums of unique elements, return the minimum element of this array.

You must write an algorithm that runs in O(log n) time.


<h4>Example 1:</h4>

Input: nums = [3,4,5,1,2]<br/>
Output: 1<br/>
Explanation: The original array was [1,2,3,4,5] rotated 3 times.

<h4>Example 2:</h4>

Input: nums = [4,5,6,7,0,1,2]<br/>
Output: 0<br/>
Explanation: The original array was [0,1,2,4,5,6,7] and it was rotated 4 times.

<h4>Example 3:</h4>

Input: nums = [11,13,15,17]<br/>
Output: 11<br/>
Explanation: The original array was [11,13,15,17] and it was rotated 4 times.


<h1>Solution:</h1>

<h3>Intuition:</h3>
In a rotated sorted array, the minimum element is the <strong>first element of the rotated portion</strong>.
Using binary search, we compare the middle value with the rightmost value:
<ul>
  <li>
    
  If `nums[mid] < nums[right]`, then the minimum lies in the left half (including `mid`).</li>
  <li>
    
  Otherwise, the minimum lies in the right half (excluding `mid`).</li>
</ul>
This behaves exactly like finding a lower bound, gradually shrinking the search space until only the minimum remains


<h3>Algorithm:</h3>
1. Set Low = 0 and high = n-1 <br>
2. <strong>while low < high:</strong>
  <ul>
        <li>Compute mid.</li>
        <li>if nums[mid] < nums[high] then move high to mid(minimum is on the left)</li>
        <li>otherwise low will move to mid+1(minimum is on the right)</li>
  </ul>
3. When loop ends low will points to the minimum element so return nums[low].


<h3>Code:</h3>

<pre>
  <code>
    class Solution {
public:
    int findMin(vector<int>& nums) {
        int low = 0;
        int high = nums.size() - 1;

        while(low < high){
            int mid = (low + high) / 2;

            if(nums[mid] < nums[high]){
                high = mid;
            } else {
                low = mid + 1;
            }
        }
        return nums[low];
    }
};
  </code>
</pre>
