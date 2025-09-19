LeetCode **112. Path Sum** easy problem .


**Question**

- Given the root of a binary tree and an integer targetSum, return true if the tree has a root-to-leaf path such that adding up all the values along the path equals targetSum.
- A leaf is a node with no children.

**Solution**

```javascript
var hasPathSum = function(root, targetSum) {
    
    let sum = 0;

    const helper = (root) => {
        if (root === null) {
            return;
        }

        sum += root.val;
        
        if (sum === targetSum && (root.left == null && root.right === null)) {
            return true;
        }

        if (helper(root.left)){
            return true;
        }
        if (helper(root.right)) {
            return true;
        };
        sum -= root.val;
    }

    return helper(root) ? true : false;
};
```

If it is not clear please check my other Article on Tree Algorithm then it will be very much easier to understand.


Feel Free to reach out to me if you have any concerns.

Reference:- 

1. https://leetcode.com/problems/path-sum/?envType=study-plan-v2&envId=top-interview-150
