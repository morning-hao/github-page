> 时间O(N)：
>
> 空间O(N)：

```python

```



#### [1. 两数之和](https://leetcode.cn/problems/two-sum/)

> 时间O(N)：遍历N个num
>
> 空间O(N)：一个哈希表随着N的数量增大
>
> 如果不用哈希表直接暴力搜索的话时间复杂度是$O(N^2)$，空间O(1)

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        dic = {}
        for i, num in enumerate(nums):
            aim = target - num
            if aim in dic:
                return [i,dic[aim]]
            else:
                dic[num] = i
```

#### [2. 两数相加](https://leetcode.cn/problems/add-two-numbers/?favorite=2cktkvj)

> 时间O(max(m,n)+1)：，遍历m或者n的链表完后，还可能会进位运行一次
>
> 空间O(1)：返回值不计入空间复杂度

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        head = result = ListNode(0)  # head用于添加结果，result用于返回结果
        carry = 0  # 进位标志符号
        while l1 or l2 or carry:  # 如果两个链表都遍历完了同时不存在进位才跳出
            # 获得链表的值
            num_l1 = l1.val if l1 else 0  
            num_l2 = l2.val if l2 else 0
            num_add = num_l1 + num_l2 + carry  # 计算位数相加和
            carry = 1 if num_add >= 10 else 0  # 更新进位值，大于9就为1
            head.next = ListNode(num_add % 10)  # 对10求余获得个位
            # 更新节点
            head = head.next
            l1 = l1.next if l1 else 0
            l2 = l2.next if l2 else 0
        return result.next  # 返回的是result.next因为原本的result是0
```

#### [3. 无重复字符的最长子串](https://leetcode.cn/problems/longest-substring-without-repeating-characters/?favorite=2cktkvj)

> 时间O(N)：每个元素遍历一次，一共N次
>
> 空间O(N)：substr最多存储N个元素。
>
> 遍历每个元素，如果碰到有重复的就在子串中去除，然后更新最大长度

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        if not s: return 0

        n = len(s)
        left = 0  # 用于记录当前的左元素索引
        substr = set()
        max_len = 0
        cur_len = 0
        for i in range(n):
            cur_len += 1  # 每添加一个元素就加一
            while s[i] in substr:  # 剔除重复的部分
                substr.remove(s[left])
                left += 1
                cur_len -= 1
            if cur_len > max_len: max_len = cur_len  # 更新最大长度
            substr.add(s[i])  # 记录字串元素
        return max_len
```

#### [4. 寻找两个正序数组的中位数](https://leetcode.cn/problems/median-of-two-sorted-arrays/?favorite=2cktkvj)

> 时间O($nlog_n$)：[Timsort - Wikipedia](https://en.wikipedia.org/wiki/Timsort)
>
> 空间O(N)：合并后的列表有N个元素(num1+num2)

```python
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        num = nums1 + nums2  # 合并
        num = sorted(num)  # 排序
        n = len(num)
        if n % 2 == 0:  # 偶数 
            return (num[n//2] + num[n//2 - 1]) / 2
        else:
            return num[n//2]  # 基数
```



#### [5. 最长回文子串](https://leetcode.cn/problems/longest-palindromic-substring/?favorite=2cktkvj)

> 时间O($N^2$)：遍历N个元素，每个元素判断也是O(N)的复杂度，总共N*N
>
> 空间O(1)：常数个变量

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        def backtextcheck(left, right):  # 中心扩散判断
            while left >= 0 and right < len(s) and s[left] == s[right]:
                left -= 1
                right += 1
            return left + 1, right - 1  # 各返回一个位置代表实际的左右下标
        
        start, end = 0, 0
        for i in range(len(s)):
            start1, end1 = backtextcheck(i, i)  # 中心元素是奇数个
            start2, end2 = backtextcheck(i, i + 1)  # 中心元素是偶数个
            if end1 - start1 > end - start:
                end = end1
                start = start1
            if end2 - start2 > end - start:
                end = end2
                start = start2
        return s[start: end + 1]  # 切片最右边+1返回字串
```

#### [10. 正则表达式匹配](https://leetcode.cn/problems/regular-expression-matching/?favorite=2cktkvj)

> 时间O(MN)：遍历二维dp表
>
> 空间O(MN)：dp表有MN个

```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        # 初始化DP表
        m, n = len(s) + 1, len(p) + 1
        dp = [[False] * n for _ in range(m)]
        dp[0][0] = True
        for i in range(2, n, 2):
            dp[0][i] = dp[0][i - 2] and p[i - 1] == '*'
        # 遍历状态
        for j in range(1, m):
            for i in range(1, n):
                if p[i - 1] == "*":
                    if dp[j][i - 2]: dp[j][i] = True
                    elif dp[j - 1][i] and s[j - 1] == p[i - 2]: dp[j][i] = True
                    elif dp[j - 1][i] and p[i - 2] == '.': dp[j][i] = True
                else:
                    if dp[j - 1][i - 1] and p[i - 1] == s[j - 1]: dp[j][i] = True
                    elif dp[j - 1][i - 1] and p[i - 1] == '.': dp[j][i] = True
        return dp[-1][-1]
```


#### [11. 盛最多水的容器](https://leetcode.cn/problems/container-with-most-water/?favorite=2cktkvj)

> 时间O(N)：遍历N个容器
>
> 空间O(1)：常数个变量

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        left, right, res = 0, len(height) - 1, 0
        while left < right:  # 跳出条件直到左右相碰
            # 循环收窄短边，同同时更新最大面积
            if height[left] < height[right]:
                res = max(res, height[left] * (right - left))
                left += 1
            else:
                res = max(res, height[right] * (right - left))
                right -= 1
        return res
```

#### [15. 三数之和](https://leetcode.cn/problems/3sum/?favorite=2cktkvj)

> 时间O($N^2$)：其中固定指针`k`循环复杂度 O(N)，双指针 `i`，`j` 复杂度 O(N)。
>
> 空间O(1)：指针使用常数大小的额外空间。

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        res = []
        for k in range(len(nums) - 2):  # 定位k循环，k定位少两个指针的位置
            i, j = k + 1, len(nums) - 1
            if k > 0 and nums[k] == nums[k - 1]: continue  # 跳过重复，首个k没有重复不用跳，后面有重复则跳过
            while i < j:  # 判断双指针是否遍历完
                s = nums[k] + nums[i] + nums[j]
                if s < 0:
                    i += 1
                    while i < j and nums[i] == nums[i - 1]: i += 1
                elif s > 0:
                    j -= 1
                    while i < j and nums[j] == nums[j + 1]: j -= 1
                else:
                    res.append([nums[k], nums[i], nums[j]])
                    i += 1
                    j -= 1
                    while i < j and nums[i] == nums[i - 1]: i += 1
                    while i < j and nums[j] == nums[j + 1]: j -= 1
        return res
```

#### [17. 电话号码的字母组合](https://leetcode.cn/problems/letter-combinations-of-a-phone-number/?favorite=2cktkvj)

> 时间O($3^m * 4^n$)：m,n分别为三个字符和四个字符的数字长度每种组合都会计算，复杂度相乘
>
> 空间O(m+n)：m+n的情况不包括输出空间是回溯过程中的递归调用深度，如果算上输出空间的话为O($3^m * 4^n$)

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        if not digits:  # 空值情况
            return []
        
        digits2str = {  # 映射表
            '2': 'abc',
            '3': 'def',
            '4': 'ghi',
            '5': 'jkl',
            '6': 'mno',
            '7': 'pqrs',
            '8': 'tuv',
            '9': 'wxyz'
        }

        def backtrack(i):  # 回溯
            if i == len(digits):  # 索引超过实际长度才追加，不然会漏掉最后一个字符
                results.append(''.join(result))
            else:
                digit = digits[i]
                for s in digits2str[digit]:
                    result.append(s)
                    backtrack(i + 1)
                    result.pop()
        results = []
        result = []
        backtrack(0)  # 启动回溯
        return results
```

#### [19. 删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/?favorite=2cktkvj)

> 时间O(N)：N为链表的长度，相当于遍历一次
>
> 空间O(1)：常数个变量

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        first = head
        second = dummy
        for _ in range(n):
            first = first.next  # 遍历n次是因为后面判断是当first为空时改动前驱节点
        
        while first:
            first = first.next
            second = second.next
        second.next = second.next.next
        return dummy.next
```