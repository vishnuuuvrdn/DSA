<h1>Problem</h1>
<h3><a href="https://leetcode.com/problems/minimum-window-substring/description/">Minimum Window Substring</a></h3>

Given two strings s and t of lengths m and n respectively, return the minimum window of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "".

The testcases will be generated such that the answer is unique.


<strong>Example 1:</strong>

Input: s = "ADOBECODEBANC", t = "ABC"<br/>
Output: "BANC"<br/>
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.<br/>


<strong>Example 2:</strong>

Input: s = "a", t = "a"<br/>
Output: "a"<br/>
Explanation: The entire string s is the minimum window.<br/>


<strong>Example 3:</strong>

Input: s = "a", t = "aa"<br/>
Output: ""<br/>
Explanation: Both 'a's from t must be included in the window.<br/>
Since the largest window of s only has one 'a', return empty string.<br/>




<h1>Solution</h1>

<h3>Intuition:</h3> 

Imagine you are highlighting a specific section of a long sentence (string s) using a highlighter. You want to find the shortest possible section that contains all the letters found in a specific word (string t). 

You cannot just scan the sentence randomly because that would be too slow and confusing. Instead, you use a Sliding Window technique:
<ul>
  <li><strong>Expand</strong>: You start highlighting from the left and keep moving right until you have successfully found all the letters you need. </li>
  <li><strong>Contract</strong>: Once you have a valid section, you try to shrink it from the left to see if you can make it shorter while still keeping all the required letters. This helps you find the minimum size. </li>
  <li><strong>Repeat</strong>: You keep doing this—expanding to find a match, then shrinking to optimize it—until you reach the end of the sentence. </li>
</ul>

<h3>Algorithm:</h3>

1. Setup and Preparation
  <ul>
    <ul>
      <li>Create a list (countT) of every character in string t and count how many times each one appears.</li>
      <li>Create a variable called need. This is simply the number of unique characters required (the size of the list above).</li>
      <li>Initialize an empty list (window) to keep track of characters currently inside our sliding window on string s.</li>
    </ul>
  </ul>

2. Start Scanning with Two Pointers
  <ul>
    <ul>
     <li>Place a Left pointer (l) and a Right pointer (r) at the start of string s.</li>
     <li>Initialize a variable have to 0. This will track how many unique characters we currently satisfy.</li>
    </ul>
  </ul>
     

3. Expand the Window (Move Right)
<ul>
  <ul>
     <li>Move the Right pointer (r) forward one step at a time.</li>
     <li>Add the character at s[r] to your window list.</li>
     <li>Check if this character is one we need (is it in t?). If yes, check if we now have the exact amount required.
     <li>If we reached the exact required amount, increase have by 1.</li>
  </ul>
</ul>
         
     

4. Try to Shrink (Move Left)
<ul>
  <ul>
    <li>Check: Is have equal to need?</li>
    <li>If NO: Keep expanding (Go back to Step 3).</li>
    <li>If YES: We have a valid window! Now we try to make it smaller.</li>
    <li>Record: Check if the current window is smaller than the best one we found before. If it is, save the position and length.</li>
    <li>Shrink: Remove the character at the Left pointer (l) from your window list (decrease its count).</li>
    <li>Check Validity: Did removing that character cause us to have less than required?</li>
    <li>If YES: Decrease have by 1. (The window is no longer valid, so stop shrinking and go back to expanding).</li>
    <li>If NO: Move the Left pointer (l) one step to the right and repeat the shrinking process.</li>
  </ul>
</ul>



5. Final Result
<ul>
  <ul>
    <li>Once the Right pointer reaches the end of the string, stop.</li>
    <li>Return the substring from the saved position. If we never found a valid window, return an empty string.</li>
  </ul>
</ul>


<h3>Code:</h3>

<pre>
  <code>
    class Solution {
    public:
        string minWindow(string s, string t) {
    
            if(t.empty()) return "";
    
            unordered_map<char, int> countT;
            for(char c : t){
                countT[c]++;
            }
    
            unordered_map<char, int> window;
    
            int have = 0;
            int need = countT.size();
            pair<int, int> res = {-1, -1};
            int resLen = INT_MAX;
            int l = 0;
    
            for(int r = 0; r < s.length(); r++){
                char c = s[r];
                window[c]++;
    
                if (countT.count(c) && window[c] == countT[c]) {
                    have++;
                }
    
                while (have == need) {
                    if ((r - l + 1) < resLen) {
                        resLen = r - l + 1;
                        res = {l, r};
                    }
    
                    window[s[l]]--;
                    if (countT.count(s[l]) && window[s[l]] < countT[s[l]]) {
                        have--;
                    }
                    l++;
                }
            }
    
            return resLen == INT_MAX ? "" : s.substr(res.first, resLen);
        }
    };
  </code>
</pre>
