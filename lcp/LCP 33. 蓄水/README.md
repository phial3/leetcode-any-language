# [LCP 33. 蓄水](https://leetcode.cn/problems/o8SXZn)

## 题目描述

<!-- 这里写题目描述 -->

给定 N 个无限容量且初始均空的水缸，每个水缸配有一个水桶用来打水，第 `i` 个水缸配备的水桶容量记作 `bucket[i]`。小扣有以下两种操作：

-   升级水桶：选择任意一个水桶，使其容量增加为 `bucket[i]+1`
-   蓄水：将全部水桶接满水，倒入各自对应的水缸

每个水缸对应最低蓄水量记作 `vat[i]`，返回小扣至少需要多少次操作可以完成所有水缸蓄水要求。

注意：实际蓄水量 **达到或超过** 最低蓄水量，即完成蓄水要求。

**示例 1：**

> 输入：`bucket = [1,3], vat = [6,8]`
>
> 输出：`4`
>
> 解释：
> 第 1 次操作升级 bucket[0]；
> 第 2 ~ 4 次操作均选择蓄水，即可完成蓄水要求。
> ![vat1.gif](https://cdn.jsdelivr.net/gh/doocs/leetcode@main/lcp/LCP%2033.%20蓄水/images/1616122992-RkDxoL-vat1.gif)

**示例 2：**

> 输入：`bucket = [9,0,1], vat = [0,2,2]`
>
> 输出：`3`
>
> 解释：
> 第 1 次操作均选择升级 bucket[1]
> 第 2~3 次操作选择蓄水，即可完成蓄水要求。

**提示：**

-   `1 <= bucket.length == vat.length <= 100`
-   `0 <= bucket[i], vat[i] <= 10^4`

## 解法

<!-- 这里可写通用的实现逻辑 -->

<!-- tabs:start -->

### **Python3**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```python

```

### **Java**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```java

```

### **...**

```

```

<!-- tabs:end -->
