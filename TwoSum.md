## 1. Two Sum

Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to_ `target`.

You may assume that each input would have **_exactly_ one solution**, and you may not use the same element twice.

You can return the answer in any order.

 

**Example 1:**
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].
```

**Example 2:**
```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

**Example 3:**
```
Input: nums = [3,3], target = 6
Output: [0,1]
``` 

**Constraints:**

- `2 <= nums.length <= 104`
- `-109 <= nums[i] <= 109`
- `-109 <= target <= 109`
- **Only one valid answer exists.**
 

**Follow-up:** Can you come up with an algorithm that is less than `O(n^2)` time complexity?

### 解题思路
这道题用暴力解法的话可以用一个嵌套的for循环来枚举数组中的每一对不同的数(a,b):

1. 如果找到满足条件的一对(a,b)使得 a + b = target，则立即返回a和b对应的index
2. 如果循环结束依旧没有找到，则返回nil。

这个解法的复杂度是O(n^2)，不符合题目的要求。

由于题目中要求返回找到的数字对应的index，所以不能对数组进行排序后再用Two Pointer，否则index都乱掉了。所以本题只能用哈希表。哈希表T的Key是数组中的元素，Value是数组中该元素的index。初始时T为空，我们开始对数组进行顺次遍历。遍历过程中，假设当前访问的数组元素为a，则去T中查找是否存在target-a，如果存在则返回a的index和T(target - a)。如果遍历结束依旧没有找到，则返回nil。代码如下：
```
def twoSum(self, nums: List[int], target: int) -> List[int]:
    hashTable = {}
    for i in range(len(nums)):
        c = target - nums[i]
        if c in hashTable:
            return [i, hashTable[c]]
        else:
            hashTable[nums[i]] = i
    return nil
```
以上解法的时间复杂度是O(n),因为线性遍历了数组，且对每个数组成员的访问时间是常量。空间复杂度也为O(n)，因为最坏情况下哈希表容纳数组中所有元素。










