<h1>Problem:</h1>
<h3>Car Fleet</h3>
There are n cars at given miles away from the starting mile 0, traveling to reach the mile target.

You are given two integer arrays position and speed, both of length n, where position[i] is the starting mile of the ith car and speed[i] is the speed of the ith car in miles per hour.

A car cannot pass another car, but it can catch up and then travel next to it at the speed of the slower car.

A car fleet is a single car or a group of cars driving next to each other. The speed of the car fleet is the minimum speed of any car in the fleet.

If a car catches up to a car fleet at the mile target, it will still be considered as part of the car fleet.

Return the number of car fleets that will arrive at the destination.

<br/>
<strong>Example 1:</strong>

Input: target = 12, position = [10,8,0,5,3], speed = [2,4,1,1,3]

Output: 3

Explanation:

The cars starting at 10 (speed 2) and 8 (speed 4) become a fleet, meeting each other at 12. The fleet forms at target.
The car starting at 0 (speed 1) does not catch up to any other car, so it is a fleet by itself.
The cars starting at 5 (speed 1) and 3 (speed 3) become a fleet, meeting each other at 6. The fleet moves at speed 1 until it reaches target.

<br/>
<strong>Example 2:</strong>

Input: target = 10, position = [3], speed = [3]

Output: 1

Explanation:

There is only one car, hence there is only one fleet.

<br/>
<strong>Example 3:</strong>

Input: target = 100, position = [0,2,4], speed = [4,2,1]

Output: 1

Explanation:

The cars starting at 0 (speed 4) and 2 (speed 2) become a fleet, meeting each other at 4. The car starting at 4 (speed 1) travels to 5.
Then, the fleet at 4 (speed 2) and the car at position 5 (speed 1) become one fleet, meeting each other at 6. The fleet moves at speed 1 until it reaches target.
 

<h4>Constraints:</h4>

n == position.length == speed.length<br/>
1 <= n <= 105<br/>
0 < target <= 106<br/>
0 <= position[i] < target<br/>
All the values of position are unique.<br/>
0 < speed[i] <= 106


<h1>Solution:</h1>

<h3>Intution:</h3>

Cars that start closer to the target are processed first.<br/>
For each car, we compute the time it will take to reach the target.<br/>
If a car behind reaches the target no faster than the car in front, it will eventually catch up and join the same fleet.<br/>
So we only keep the car’s time if it forms a new fleet; otherwise, it merges with the previous one.<br/>
Using a stack helps us easily compare each car’s time with the fleet ahead of it.<br/>


<h3>Algorithm:</h3>
<ul>
  <li>Pair the Postions and Speeds</li>
  <li>Sort them in reverse(descending) order</li>
  <li>Create a empty stack array to store double values</li>
  <li>Go through pairs and add the <strong>time</strong> into stack.</li>
  <li>if new car's time less than or equal to the time before it, it catches up and merges that fleet then pop it from the stack</li>
  <li>The number of remaining times in the stack equals the number of fleets.</li>
  <li>return the stack size.</li>
</ul>


<h3>Code:</h3>
<pre>
  <code>
    class Solution {
    public:
        int carFleet(int target, vector<int>& position, vector<int>& speed) {
            vector<pair<int, int>> pair;
            for(int i = 0; i < position.size(); i++){
                pair.push_back({position[i], speed[i]});
            }
            sort(pair.rbegin(), pair.rend());
            vector<double> stack;
            for(auto p : pair){
                stack.push_back((double)(target - p.first) / p.second);
                if(stack.size() >= 2 && stack.back() <= stack[stack.size() - 2]){
                    stack.pop_back();
                }
            }
            return stack.size();
        }
    };
  </code>
</pre>
