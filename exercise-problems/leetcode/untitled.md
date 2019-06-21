# \#15. 3Sum

Given an array `nums` of _n_ integers, are there elements _a_, _b_, _c_ in `nums` such that _a_ + _b_ + _c_ = 0? Find all unique triplets in the array which gives the sum of zero.

**Note:**

The solution set must not contain duplicate triplets.

**Example:**

```text
Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

陣列當中任意三個元素和為0

## Think

1. 延續[**Two Sum**](two-sum.md)的範例，只是將傳回值改回陣列值而非索引，並把回傳型態改為`[[Int]]`，因為不是只有一組值，如`k = -4, [-4, 0, 2, 2, 4] =>` 組合就有 `[-4, 0, 4], [-4, 2, 2]`
2. `arr.sort()`由小到大排序是為了初步過濾相同的`target`值
3. 經由`twoSum()`處理之後的陣列會加到結果陣列`res`中，此時res中可能會存在很多相同的結果，所以再將裡面的每個元素重新由小到大排序，為了要將重複的元素利用`Set`過濾掉
4. 排序後的陣列，若`第一個元素>0`或`最後一個元素<0`，表示該陣列的條件不可能符合

## Solution

```swift
func twoSum(_ nums: [Int], _ target: Int) -> [[Int]] {
    var res  = [[Int]]()
    var dict = [Int:Int]()

    for i in 0..<nums.count{
        if let val = dict[nums[i]] { res.append([nums[i], val]) }
        else { dict[target - nums[i]] = nums[i] }
    }
        return res
}

func threeSum(_ nums: [Int]) -> [[Int]] {
    var arr = nums
    var res = [[Int]]()
    var a   = [[Int]]()
    var b   = [Int]()
    var i   = 0
    
    // illegal condition
    if arr.count < 3 { return res }        
    
    var target = Int.max
    arr.sort()
    // Start with non-nagative or last with nagative must be fail
    if arr[0] > 0 || arr[0] < 0 { return res }
    
    while i < arr.count {
        b = arr
        b.remove(at: i)
        if target == arr[i] {
            i += 1
            continue
        }
        target = arr[i]
        a = twoSum(b, target * -1)
        if a == [[0]] {
            i += 1
            continue
        }
        else {
            for element in 0..<a.count {
                a[element].append(target)
                a[element].sort()
        }
            for i in a { res.append(i) }
        }
        i += 1
    }
    
    // to eliminate duplicate elements by using Set()
    let uniqRes:[[Int]] = Array(Set(res))
    return uniqRes
}

// test...
threeSum([])
threeSum([1, 2, 3])
threeSum([-1, -2, -3])
threeSum([-4, -2, -2, -2, 0, 1, 2, 2, 2, 3, 3, 4, 4, 6, 6])
```

{% hint style="warning" %}
此解法的效能可能不是很好，有機會再修改
{% endhint %}

## Question Ref.

{% embed url="https://leetcode.com/problems/3sum/description/" %}

