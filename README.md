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

# Implementation 2 :
```java
class Solution {
  public String minWindow(String s, String t) {
        if (s.length() == 0 || t.length() == 0) return "";
        Map<Character, Integer> map = new HashMap<Character, Integer>();
        for (char ch : t.toCharArray())
            map.put(ch, map.getOrDefault(ch, 0) + 1);
      
        int start=0, end=0, left=0, right=0, target=t.length();
        while (right < s.length()) {
            int count = map.getOrDefault(s.charAt(right) , 0);
            if (count > 0)  {
            	System.out.println("Matched : "+ s.charAt(right)+" at index " + right);
            	target--;
            }
            map.put(s.charAt(right),count-1);
            right++;
            while (target == 0) {
            	System.out.println("Map : " + map);
            	System.out.println("Left : " + left);
                if (end == 0 || end - start > right - left) {
                    start = left; 
                    end = right;
                }
                int value = map.getOrDefault(s.charAt(left),0);
                if (value >= 0) target++;
                map.put(s.charAt(left),value + 1);
                left++;
            }
            
        }
        return s.substring(start, end);
    }
}
```
### Code execution output :
```java
Matched : x at index 13
Matched : y at index 15
Map : {a=-2, b=-1, c=-1, d=-1, e=-1, f=-1, g=-1, h=-1, i=-1, j=-1, k=-1, l=-1, x=-1, y=0}
Left : 0
Map : {a=-1, b=-1, c=-1, d=-1, e=-1, f=-1, g=-1, h=-1, i=-1, j=-1, k=-1, l=-1, x=-1, y=0}
Left : 1
Map : {a=-1, b=0, c=-1, d=-1, e=-1, f=-1, g=-1, h=-1, i=-1, j=-1, k=-1, l=-1, x=-1, y=0}
Left : 2
Map : {a=-1, b=0, c=0, d=-1, e=-1, f=-1, g=-1, h=-1, i=-1, j=-1, k=-1, l=-1, x=-1, y=0}
Left : 3
Map : {a=-1, b=0, c=0, d=0, e=-1, f=-1, g=-1, h=-1, i=-1, j=-1, k=-1, l=-1, x=-1, y=0}
Left : 4
Map : {a=-1, b=0, c=0, d=0, e=0, f=-1, g=-1, h=-1, i=-1, j=-1, k=-1, l=-1, x=-1, y=0}
Left : 5
Map : {a=-1, b=0, c=0, d=0, e=0, f=0, g=-1, h=-1, i=-1, j=-1, k=-1, l=-1, x=-1, y=0}
Left : 6
Map : {a=-1, b=0, c=0, d=0, e=0, f=0, g=0, h=-1, i=-1, j=-1, k=-1, l=-1, x=-1, y=0}
Left : 7
Map : {a=-1, b=0, c=0, d=0, e=0, f=0, g=0, h=0, i=-1, j=-1, k=-1, l=-1, x=-1, y=0}
Left : 8
Map : {a=-1, b=0, c=0, d=0, e=0, f=0, g=0, h=0, i=0, j=-1, k=-1, l=-1, x=-1, y=0}
Left : 9
Map : {a=-1, b=0, c=0, d=0, e=0, f=0, g=0, h=0, i=0, j=0, k=-1, l=-1, x=-1, y=0}
Left : 10
Map : {a=-1, b=0, c=0, d=0, e=0, f=0, g=0, h=0, i=0, j=0, k=0, l=-1, x=-1, y=0}
Left : 11
Map : {a=-1, b=0, c=0, d=0, e=0, f=0, g=0, h=0, i=0, j=0, k=0, l=0, x=-1, y=0}
Left : 12
Map : {a=0, b=0, c=0, d=0, e=0, f=0, g=0, h=0, i=0, j=0, k=0, l=0, x=-1, y=0}
Left : 13
Map : {a=0, b=0, c=0, d=0, e=0, f=0, g=0, h=0, i=0, j=0, k=0, l=0, x=0, y=0}
Left : 14
```

# References :
https://leetcode.com/articles/minimum-window-substring/?page=5
