## 3. [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) (Medium)
Given a string `s`, find the length of the **longest substring** without repeating characters.

 

**Example 1:**
```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

**Example 2:**
```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```
**Example 3:**
```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```
**Example 4:**
```
Input: s = ""
Output: 0
``` 

**Constraints:**

- `0 <= s.length <= 5 * 104`
- `s` consists of English letters, digits, symbols and spaces.

### 解题思路
本题如果用暴力解法的话，需要枚举字符串中所有的子串，且对每个子串判定其是否含有重复的字符，总的时间复杂度为O(n^3)。

这道题正确的思路是运用"滑动窗口"，即Slidng Window，维持两个指针l和r，分别指向窗口的左边界和右边界。然后进行一下循环操作:
1. 移动右指针扩大窗口范围，直到窗口中包含了重复字符。
2. 移动左指针缩小窗口范围，直到窗口中不再包含重复字符，回到1。
循环退出条件是右指针指向了字符串的右边界。

中间判断是否包含重复字符可以利用哈希表去做。这里哈希表的Key是单个的字符，Value是字符在字符串中对应的index的下一位。这样依次遍历数组的时候当右指针访问到一个已经在哈希表中存在的字符时，可以将左指针直接移到这个字符在哈希表里对应的Value。这样就保证了从左指针开始到右指针结束都不包含重复的字符。
···
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        l = 0
        result = 0
        mp = {}
        for r in range(len(s)):
            if s[r] in mp:
                l = max(l, mp[s[r]])
            result = max(result, r - l + 1)
            mp[s[r]] = r + 1
        return result
···
以上解法的时间复杂度是O(n)，因为线性遍历了一遍数组，空间复杂度是O(n)，因为维护了额外的哈希表。




