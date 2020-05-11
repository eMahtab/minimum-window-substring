# Minimum Window Substring
## https://leetcode.com/problems/minimum-window-substring

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).
```
Example:

Input: S = "ADOBECODEBANC", T = "ABC"
Output: "BANC"
```
**Note:**
1. If there is no such window in S that covers all characters in T, return the empty string "".
2. If there is such window, you are guaranteed that there will always be only one unique minimum window in S.


# Implementation 1 : Naive (Time Limit Exceeded)
```java
class Solution {
   public String minWindow(String s, String t) {
        int length = s.length();
        String result = "";
        for(int i = 0; i < s.length(); i++) {
            for(int j = i+1; j <= s.length(); j++) {
                String substring = s.substring(i,j);
                if(countChars(substring, t)){
                    if(substring.length() <= length) {
                        result = substring;
                        length = substring.length();
                    }	
                }
            }
        }
        return result;
    }
    
    private boolean countChars(String substring, String target) {
        Map<Character, Integer> map = new HashMap<>();
        for(char ch : target.toCharArray()) {
            int count = map.getOrDefault(ch,0);
            map.put(ch, count+1);
        }
        for(char ch : substring.toCharArray()) {
            if(map.containsKey(ch)) {
                map.put(ch, map.get(ch) -1);
            }
        }
        for(char ch : map.keySet()) {
            if(!(map.get(ch) <= 0))
                return false;
        }
        return true;
    }
}
```
