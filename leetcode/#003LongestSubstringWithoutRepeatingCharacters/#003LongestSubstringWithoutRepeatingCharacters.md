##003 Longest Substring Without Repeating Characters
##最长不重复子串问题
##问题描述
Given a string, find the length of the longest substring without repeating characters. 
For example, the longest substring without repeating letters for "abcabcbb" is "abc", 
which the length is 3. For "bbbbb" the longest substring is "b", with the length of 1.
##问题解析
找出字符串中不包含重复字符的子串，返回最长子串的长度。  
#思路1：
遍历字符串的所有子串，一一判断子串是否为不重复子串，记录不重复子串的长度，从中取最
长子串。遍历所有串的时间复杂度为O(n^2),判断子串是否为不重复子串的时间复杂度为O(n)，
整体的时间复杂度为O(n^3).此解法时间复杂度太高，无法通过leecode。
#思路1-实现代码
```
 /**
     * 列举所有子串情况[n*(n/2)],再判断每一个子串字符都是唯一的[n]
     * 时间复杂度：O(n^3)
     * 简单但是时间复杂度太高
     *
     * @param s characters
     * @return longest number
     */
    public int lengthOfLongestSubstring(String s) {
        int length = 0;
        String[] lists = s.split("");
        for (int i = 0; i < lists.length; i++) {
            for (int j = i + 1; j < lists.length; j++) {
                String subStr = s.substring(i, j);
                String[] subLists = subStr.split("");
                Map<String, Integer> charMap = new HashMap<>();
                    for (String subStrChar : subLists) {
                    charMap.put(subStrChar, 1);
                }

                if(subLists.length == charMap.size() && length < (j - i)) {
                    length = j - i;
                }
            }
        }
        return length;
    }
```

#思路2:

#思路2-实现代码

