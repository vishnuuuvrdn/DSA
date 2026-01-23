<h1>Problem:</h1>
<h3>74. Search a 2D Matrix</h3>

You are given an m x n integer matrix matrix with the following two properties:
<ul>
<li>Each row is sorted in non-decreasing order.</li>
<li>The first integer of each row is greater than the last integer of the previous row.</li>
Given an integer target, return true if target is in matrix or false otherwise.
</ul>
You must write a solution in O(log(m * n)) time complexity.

<h4>Example 1:</h4>
<img src="https://assets.leetcode.com/uploads/2020/10/05/mat.jpg">

Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3<br/>
Output: true

<h4>Example 2:</h4>
<img src="https://assets.leetcode.com/uploads/2020/10/05/mat2.jpg">

Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13<br />
Output: false

<h4>Constraints:</h4>
<ul>
<li>m == matrix.length</li>
<li>n == matrix[i].length</li>
<li>1 <= m, n <= 100</li>
<li>-104 <= matrix[i][j], target <= 104</li>
</ul>


<h1>Solution:</h1>
<h3>Intuition:</h3>
<p>
  We pretend the 2D matrix is a single sorted 1D array and run binary search on it.
</p>

<h3>Algorithm:</h3>
<p>
  <h4>Look at the matrix.</h4>
  <ul>
    <li>
      Treat it like one long straight line, not rows and columns.
    </li>
  </ul>
  
  <h4>Count everything.</h4>
  <ul>
    <li>
      Total numbers = rows × columns.
    </li>
  </ul>
  
  <h4>Start the search.</h4>
  <ul>
    <li>Left side starts at the first number.</li>
    <li>Right side starts at the last number.</li>
  </ul>
  <h4>While left has not crossed right:</h4>
  <ul>
    <li>Go to the middle number.</li>
    <li>Figure out which row it is in.</li>
    <li>Figure out which column it is in.</li>
    <li>Check the number.</li>
    
  <li><h4>If the number is equal to the target:</h4></li>
        Return true.
  
  <li><h4>If the number is smaller than the target:</h4></li>
      Move to the right side.

  <li><h4>If the number is bigger than the target:</h4></li>
      Move to the left side.
</ul>

  <h4>If loop ended then:</h4>
  <ul>
     <li>Return false.</li>
  </ul>
</p>


<h3>Code:</h3>

<pre>
  <code>
    class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int low = 0;
        int high = matrix.size() * matrix[0].size() - 1;

        while(low <= high){
            int mid = (low+high) / 2;
            int row = mid / matrix[0].size();
            int col = mid % matrix[0].size();

            int val = matrix[row][col];

            if(val == target) return true;
            else if(val < target) low = mid + 1;
            else high = mid - 1;
        }
        return false;
    }
};
  </code>
</pre>
