Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `''`.

Example 1:
```
Input: ["flower","flow","flight"]
Output: "fl"
```

Example 2:
```
Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

Note: All given inputs are in lowercase letters `a-z`.

---
### My Answer:
```
class Solution(object):
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        if not strs:
            return('')
        
        prefix = strs[0]
        while True:
            if all(s.startswith(prefix) for s in strs):
                return(prefix)
            else:
                prefix = prefix[:-1]
```
Success: 16 ms, faster than 92.56% ; 12.1 MB, less than 12.50%

---
### Solution
#### Approach 1: Horizontal scanning
LCP[S1,S2,...,Sn] = LCP(LCP(LCP(S1,S2),S3)...,Sn)
```
Java:
public String longestCommonPrefix(String[] strs) {
    if (strs.length == 0) return "";
    String prefix = strs[0];
    for (int i = 1; i < strs.length; i++)
        while (strs[i].indexOf(prefix) != 0) {
            prefix = prefix.substring(0, prefix.length() - 1);
            if (prefix.isEmpty()) return "";
        }        
    return prefix;
}
```
Complexity Analysis:
- Time complexity : `O(S)`, where S is the sum of all characters in all strings.
- Space complexity : O(1)O(1). We only used constant extra space.

#### Approach 2: Vertical scanning
Imagine a very short string is at the end of the array. The above approach will still do SS comparisons. 
One way to optimize this case is to do vertical scanning. We compare characters from top to bottom on the same column (same character index of the strings) before moving on to the next column.
```
Java:
public String longestCommonPrefix(String[] strs) {
    if (strs == null || strs.length == 0) return "";
    for (int i = 0; i < strs[0].length() ; i++){
        char c = strs[0].charAt(i);
        for (int j = 1; j < strs.length; j ++) {
            if (i == strs[j].length() || strs[j].charAt(i) != c)
                return strs[0].substring(0, i);             
        }
    }
    return strs[0];
}
```
#### Approach 3: Divide and conquer
The idea of the algorithm comes from the associative property of LCP operation. 
We notice that : LCP(S_1 ... S_n) = LCP(LCP(S_1 ... S_k), LCP (S_{k+1} ... S_n))

#### Approach 4: Binary search


