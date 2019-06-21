# \#217. Contains Duplicate

Given an array of integers, find if the array contains any duplicates.

Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

**Example 1:**

```text
Input: [1,2,3,1]
Output: true
```

**Example 2:**

```text
Input: [1,2,3,4]
Output: false
```

**Example 3:**

```text
Input: [1,1,1,3,3,4,3,2,4,2]
Output: true
```

## Think

**集合\(Set\)**用來儲存相同型別且**沒有順序**、**沒有重複的值**，當順序不重要或是需要每個值只能出現一次時，可以選擇使用`Set`。

## Solution

```swift
class Solution {
    func containsDuplicate(_ nums: [Int]) -> Bool {
        return Set(nums).count != nums.count
    }
}
```

## Question Ref.

{% embed url="https://leetcode.com/problems/contains-duplicate/" %}



