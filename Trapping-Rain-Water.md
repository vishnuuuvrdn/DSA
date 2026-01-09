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
</p>

<h2>Code:</h2>

<pre>
  <code>
    int trap(vector<int>& height) {
      if(height.empty()){
        return 0;
      }
      int l = 0;
      int r = height.size() - 1;
      int leftMax = height[l];
      int rightMax = height[r];
      int water = 0;
      while(l < r){
        if(leftMax < rightMax){
          l++;
          leftMax = max(leftMax, height[l]);
          water += leftMax - height[1];
        }
        else {
          r--;
          rightMax = max(rightMax, height[r]);
          water += rightMax - height[r];
        }
      }
      return water;
    }
  </code>
</pre>
