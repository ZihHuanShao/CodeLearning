# \#1. Two Sum

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have _**exactly**_ one solution, and you may not use the _same_ element twice.

**Example:**

```text
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

找出陣列的兩元素相加等於`target`值，並回傳兩元素的索引值

## **Think**

1. 使用字典\(dictionary\)來當作查找的方法
2. 依序將陣列的`索引值`與`目標值 - 陣列元素`的值存進字典，請注意，`目標值 - 陣列元素`是當作字典的key存入，而`索引值`是當作key對應的值：`dict[target - nums[i]] = i`
3. 只要陣列元素存在字典裡，即符合

## **Solution**

```swift
class Solution {
    func twoSum(_ nums: [Int], _ target: Int) -> [Int] {
        var dict:[Int:Int] = [:]
        
        for i in 0..<nums.count{
            if let val = dict[nums[i]]{
                return [val, i]
            }else{
                dict[target - nums[i]] = i
            }
        }
        return [0]
    }
    
}
```

## Question Ref.

{% embed url="https://leetcode.com/problems/two-sum/description/" %}

