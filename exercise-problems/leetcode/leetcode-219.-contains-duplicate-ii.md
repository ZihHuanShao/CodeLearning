# \#219. Contains Duplicate II

Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that **nums\[i\] = nums\[j\]** and the **absolute** difference between i and j is at most k.

**Example 1:**

```text
Input: nums = [1,2,3,1], k = 3
Output: true
```

**Example 2:**

```text
Input: nums = [1,0,1,1], k = 1
Output: true
```

**Example 3:**

```text
Input: nums = [1,2,3,1,2,3], k = 2
Output: false
```

給定一個整數陣列和一個整數`k`，找出陣列是否存在兩個不同的索引`i`和`j`，使得`nums [i] = nums [j]`並且`i`和`j`之間的絕對差值最多為`k`。  
＝＞陣列中兩個相同元素之間的距離不超過`k`

## Think

1. **集合\(Set\)**用來儲存相同型別且**沒有順序**、**沒有重複的值**，當順序不重要或是需要每個值只能出現一次時，可以選擇使用`Set`。
2. 利用`Set`的`.inserted`方法能夠檢查是否成功插入元素到`Set`中，並回傳布林值
3. 依序走訪陣列並將元素存到`Set`，陣列索引若大於k值，移除陣列的第一個元素，再存入當前元素（重複直到走訪完畢）並查找`set`是否有重複的元素，若有，則代表陣列中兩個相同元素距離不超過`k`，回傳`true`，反之則`false`。以上述**Example 3**為例：

| i &gt; k | set存放元素 |
| :---: | :--- |
| 0 &gt; 2 | \[1\] |
| 1 &gt; 2 | \[1, 2\] |
| 2 &gt; 2 | \[1, 2, 3\] |
| 3 &gt; 2 | \[2, 3, 1\]  刪除原陣列的第一個元素再存入當前元素 |
| 4 &gt; 2 | \[3, 1, 2\]  刪除原陣列的第二個元素再存入當前元素 |
| 5 &gt; 2 | \[1, 2, 3\]  刪除原陣列的第三個元素再存入當前元素  |
|  | `return false` |

## Solution

```swift
class Solution {
    func containsNearbyDuplicate(_ nums: [Int], _ k: Int) -> Bool {
        var set = Set<Int>()
        for i in 0..<nums.count {
            if i > k { 
                set.remove(nums[i - k - 1]) 
            }
            if set.insert(nums[i]).inserted != true{
                return true 
            }
        }
        return false
    }
}
```

## Question Ref.

{% embed url="https://leetcode.com/problems/contains-duplicate-ii/" %}



