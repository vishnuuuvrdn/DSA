<strong>Problem: Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.</strong>

<strong>Solution: </strong>

<code>
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
</code>
