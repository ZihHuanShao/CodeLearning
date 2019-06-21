# \#530. Minimum Absolute Difference in BST

Given a binary search tree with non-negative values, find the minimum [absolute difference](https://en.wikipedia.org/wiki/Absolute_difference) between values of any two nodes.

**Example:**

```text
Input:

   1
    \
     3
    /
   2

Output:
1

Explanation:
The minimum absolute difference is 1, which is the difference between 2 and 1 (or between 2 and 3).
```

給一個BST，找出任意兩節點相差最小的值

## Think

使用**中序**演算法 \(使用遞迴\)遍歷整棵樹，利用走訪完的特性：**由小到大**，再依序比較前後差值再取最小值

```c
inorder(Node *root){ 
    if(root == NULL)
        return;
    inorder(root->Lchild);
    printf("%d", root->data);
    inorder(root-<Rchild); 
}
```

{% hint style="info" %}
EX:          
           7  
        /     \  
      4        11  
    /  \       /  \  
   2    5   8    14         =&gt; Inorder: \[2, 4, 5, 7, 8, 11, 14\]  
  
min\(Int.max, 4 - 2\) =&gt; 2  
min\(**2**, 5 - 4\) =&gt; 1  
min\(**1**, 7 - 5\) =&gt; 1  
min\(**1**, 8 - 7\) =&gt; 1  
min\(**1**, 11 - 8\) =&gt; 1  
min\(**1**, 14 - 11\) =&gt; 1
{% endhint %}

| 存放走訪前的陣列 | 當前走訪的節點 | 跟陣列最後一個元素比較最小值 |
| :---: | :---: | :--- |
| \[ \] | 2 |  |
| \[2\] | 4 | min\(4 - 2, Int.max\) |
| \[2, 4\] | 5 | min\(2, 5 - 4\) |
| \[2, 4, 5\] | 7 | min\(1, 7 - 5\) |
| \[2, 4, 5, 7\] | 8 | min\(1, 8 - 7\) |
| \[2, 4, 5, 7, 8\] | 11 | min\(1, 11 - 8\) |
| \[2, 4, 5, 7, 8, 11\] | 14 | min\(1, 14 - 11\) |

## Solution

```swift
public class TreeNode {
    public var val: Int
    public var left: TreeNode?
    public var right: TreeNode?
    public init(_ val: Int) {
        self.val = val
        self.left = nil
        self.right = nil
    }
}

func getMinimumDifference(_ root: TreeNode?) -> Int {
    var throughArr = [Int]()
    var res = Int.max

    func inOrder(_ root: TreeNode?) {
    
        guard (root?.val) != nil else {return} // make sure root is not empty
        
        inOrder(root!.left)

        if let last = throughArr.last {
            res = min((root!.val - last), res)
        }
        throughArr.append(root!.val)
        
        inOrder(root!.right)
    }
    inOrder(root)
    return res
}
```

## Question Ref.

{% embed url="https://leetcode.com/problems/minimum-absolute-difference-in-bst/" %}



