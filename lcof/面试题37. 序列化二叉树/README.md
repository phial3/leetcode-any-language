# [面试题 37. 序列化二叉树](https://leetcode.cn/problems/xu-lie-hua-er-cha-shu-lcof/)

## 题目描述

<!-- 这里写题目描述 -->

<p>请实现两个函数，分别用来序列化和反序列化二叉树。</p>

<p>你需要设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。</p>

<p><strong>提示：</strong>输入输出格式与 LeetCode 目前使用的方式一致，详情请参阅&nbsp;<a href="https://support.leetcode.cn/hc/kb/article/1194353/">LeetCode 序列化二叉树的格式</a>。你并非必须采取这种方式，你也可以采用其他的方法解决这个问题。</p>

<p>&nbsp;</p>

<p><strong>示例：</strong></p>
<img alt="" src="https://cdn.jsdelivr.net/gh/doocs/leetcode@main/lcof/%E9%9D%A2%E8%AF%95%E9%A2%9837.%20%E5%BA%8F%E5%88%97%E5%8C%96%E4%BA%8C%E5%8F%89%E6%A0%91/images/serdeser.jpg" style="width: 442px; height: 324px;" />
<pre>
<strong>输入：</strong>root = [1,2,3,null,null,4,5]
<strong>输出：</strong>[1,2,3,null,null,4,5]
</pre>

<p>&nbsp;</p>

<p>注意：本题与主站 297 题相同：<a href="https://leetcode.cn/problems/serialize-and-deserialize-binary-tree/">https://leetcode.cn/problems/serialize-and-deserialize-binary-tree/</a></p>

## 解法

<!-- 这里可写通用的实现逻辑 -->

层次遍历解决。

<!-- tabs:start -->

### **Python3**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.

        :type root: TreeNode
        :rtype: str
        """
        if not root:
            return '[]'
        queue = deque()
        queue.append(root)
        res = []
        while queue:
            node = queue.popleft()
            if node:
                res.append(str(node.val))
                queue.append(node.left)
                queue.append(node.right)
            else:
                res.append('null')
        return f'[{",".join(res)}]'


    def deserialize(self, data):
        """Decodes your encoded data to tree.

        :type data: str
        :rtype: TreeNode
        """
        if not data or data == '[]':
            return None
        queue = deque()
        nodes = data[1:-1].split(',')
        root = TreeNode(nodes[0])
        queue.append(root)
        idx = 1
        while queue and idx < len(nodes):
            node = queue.popleft()
            if nodes[idx] != 'null':
                node.left = TreeNode(nodes[idx])
                queue.append(node.left)
            idx += 1
            if nodes[idx] != 'null':
                node.right = TreeNode(nodes[idx])
                queue.append(node.right)
            idx += 1
        return root


# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.deserialize(codec.serialize(root))
```

### **Java**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        if (root == null) {
            return "[]";
        }
        StringBuilder sb = new StringBuilder("[");
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();
            if (node != null) {
                sb.append(node.val);
                queue.offer(node.left);
                queue.offer(node.right);
            } else {
                sb.append("null");
            }
            sb.append(",");
        }
        return sb.deleteCharAt(sb.length() - 1).append("]").toString();
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data == null || "[]".equals(data)) {
            return null;
        }
        String[] nodes = data.substring(1, data.length() - 1).split(",");
        Queue<TreeNode> queue = new LinkedList<>();
        TreeNode root = new TreeNode(Integer.parseInt(nodes[0]));
        queue.offer(root);
        int idx = 1;
        while (!queue.isEmpty() && idx < nodes.length) {
            TreeNode node = queue.poll();
            if (!"null".equals(nodes[idx])) {
                node.left = new TreeNode(Integer.parseInt(nodes[idx]));
                queue.offer(node.left);
            }
            ++idx;
            if (!"null".equals(nodes[idx])) {
                node.right = new TreeNode(Integer.parseInt(nodes[idx]));
                queue.offer(node.right);
            }
            ++idx;
        }
        return root;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```

### **JavaScript**

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */

/**
 * Encodes a tree to a single string.
 *
 * @param {TreeNode} root
 * @return {string}
 */
var serialize = function (root) {
    if (!root) return '[]';
    let queue = [root];
    let res = '';
    while (queue.length) {
        let node = queue.shift();
        if (node) {
            res += node.val + ',';
            queue.push(node.left);
            queue.push(node.right);
        } else {
            res += 'null' + ',';
        }
    }
    return `[${res.substring(0, res.length - 1)}]`;
};

/**
 * Decodes your encoded data to tree.
 *
 * @param {string} data
 * @return {TreeNode}
 */
var deserialize = function (data) {
    if (!data || data.length <= 2) return null;
    let arr = data.substring(1, data.length - 1).split(',');
    let root = new TreeNode(arr.shift());
    let queue = [root];
    while (queue.length) {
        let node = queue.shift();
        let leftVal = arr.shift();
        if (leftVal !== 'null') {
            node.left = new TreeNode(leftVal);
            queue.push(node.left);
        }
        let rightVal = arr.shift();
        if (rightVal !== 'null') {
            node.right = new TreeNode(rightVal);
            queue.push(node.right);
        }
    }
    return root;
};

/**
 * Your functions will be called as such:
 * deserialize(serialize(root));
 */
```

### **...**

```

```

<!-- tabs:end -->
