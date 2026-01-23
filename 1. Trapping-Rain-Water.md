<h1>Trapping Rain Water</h1>
<h2>Problem:</h2>
<p>

<strong> Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.</strong>

<h6>Example 1:
  <br/>
  <br/>
    <img src="https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png">
<br/>
<br/>
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
<br/>
Output: 6
<br/>
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
<br/>
<br/>
Constraints:
<br/>
n == height.length
<br/>
1 <= n <= 2 * 104
<br/>
0 <= height[i] <= 105
</h6>
</p>

<h2>Solution:</h2>

<h3>Understanding The Problem:</h3>
<p>
  There is a container (or we can say a tub) containing sticks of different heights. When rain falls into the tub, the sticks store water between them. We need to calculate    and return the maximum amount of water that can be stored between the sticks, based on their heights.
</p>

<h3>Main Solution:</h3>
<p>
  I am approaching Two Pointers concept for this problem.
  <ul>
    <li>First we have to check the Array is empty or not</li>
    <li>then take two pointers left and right</li>
    <li>after the two pointers take leftMax and rightMax so that we can easily calculate the amount of watter tripped</li>
    <li>now take a variable for result</li>
    <li>run a loop until left < right </li>
    <li>write a condition the if leftMax is lessthan rightMax increase left and change leftMax to maximum of leftMax and height[left] and then add leftMax - height[left] to result</li>
    <li>if the condition is not satisfied then decrease right and change rightMax to maximum of rightMax and height[right] and then add rightMax - height[right] to result</li>
    <li>getout from loop and return result</li>
  </ul>

  <h4><em>This is my first Problem Explanation and I felt explanation is not good but i will increase day by day it's a promise to myself</em></h4>
</p>

<h2>Code:</h2>

<pre>
  <code>
    int trap(vector<int>& height) {
      if(height.empty()){
        return 0;
      }
      int left = 0;
      int right = height.size() - 1;
      int leftMax = height[l];
      int rightMax = height[r];
      int water = 0;
      while(l < r){
        if(leftMax < rightMax){
          left++;
          leftMax = max(leftMax, height[left]);
          water += leftMax - height[left];
        }
        else {
          right--;
          rightMax = max(rightMax, height[right]);
          water += rightMax - height[right];
        }
      }
      return water;
    }
  </code>
</pre>
