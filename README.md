# Minimum Window Substring
## https://leetcode.com/problems/minimum-window-substring


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
