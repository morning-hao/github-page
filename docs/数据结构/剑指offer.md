##
> leetcode网址:https://leetcode-cn.com/leetbook/detail/illustration-of-algorithm/

# 一.复杂度

## 1.时间复杂度

## 表示方法

时间复杂度指输入数据大小为 N 时，算法运行所需花费的时间。
常用的符号有:平均 $\Theta$ ，最佳 $\Omega(1)$，最差$O(N)$三种，一般使用最差$O(N)$来表示

## 常见种类

$O(1)<O(logN)<O(N)<O(NlogN)<O(N^2)<O(2^N)<O(N!)$

## 2.空间复杂度

## 空间来源

输入空间： 存储输入数据所需的空间大小；
暂存空间： 算法运行过程中，存储所有中间变量和对象等数据所需的空间大小；
输出空间： 算法运行返回时，存储输出数据所需的空间大小；

## 常见种类

$O(1)<O(logN)<O(N)<O(N^2)<O(2^N)$

# 二.数据结构类型基础

> 类型简介


| 是否为线性     | 具体类型 | 介绍                                                                                    |
| ---------------- | ---------- | ----------------------------------------------------------------------------------------- |
| 线性数据结构   | 数组     | 可变数组基于数组和扩容机制实现，常用操作有：访问元素、添加元素、删除元素。              |
|                | 链表     | 链表以节点为单位，每个元素都是一个独立对象，在内存空间的存储是非连续的。                |
|                | 栈       | 栈是一种具有 「先入后出」 特点的抽象数据结构，可使用数组或链表实现                      |
|                | 队列     | 队列是一种具有 「先入先出」 特点的抽象数据结构，可使用链表实现                          |
| 非线性数据结构 | 树       | 树是一种非线性数据结构，根据子节点数量可分为 「二叉树」 和 「多叉树」                   |
|                | 图       | 图是一种非线性数据结构，由「节点（顶点）vertex」和「边 edge」组成，每条边连接一对顶点。 |
|                | 散列表   | 利用 Hash 函数将指定的「键 key」映射至对应的「值 value」，以实现高效的元素查找          |
|                | 堆       | 堆分为「大顶堆」和「小顶堆」，大（小）顶堆：任意节点的值不大于（小于）其父节点的值      |

## 1.[剑指 Offer 05. 替换空格](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)

> 时间O(N):遍历字符串长度N
>
> 空间O(N):保存字符串长度N的一个变量并返回
>
> 思路：顺序遍历字符串，遇到空格就添加%20否则添加原字符

```python
class Solution:
    def replaceSpace(self, s: str) -> str:
        result = ''  # 字符串为不可变类型，需要新建一个变量
        for char in s:
            if char != ' ':  # 每次添加字符相当于重新赋值
                result += char
            else: result += '%20' 
        return result
```

## 2.[剑指 Offer 06. 从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

> 时间O(N):N为链表的长度
>
> 空间O(N):N为暂存数组的长度
>
> 用一个暂存列表暂存每个节点的值，直到链表完全遍历完

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reversePrint(self, head: ListNode) -> List[int]:
        result = []
        while head:  # 链表顺序访问的同时并保存
            result.append(head.val)
            head = head.next
        return result[::-1]
```

## 3.[剑指 Offer 09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

> appendTail时间O(1):每次添加1个数字
>
> deleteHead时间O(N):最差情况是第一次删除，需要将输入栈中的N个数字全部放到辅助栈
>
> 空间O(N):输入栈和辅助栈总共保存N个元素
>
> 一个栈做输入栈
>
> 另一个栈做删除栈，在转述句转移的时候，删除栈的数据就变成了先入后出

```python
class CQueue:

    def __init__(self):
        self.A = []
        self.B = []

    def appendTail(self, value: int) -> None:
        self.A.append(value)

    def deleteHead(self) -> int:
        # 模仿流程图，先判断有没有self.B,如果没有在判断有没有self.A
        if self.B:  
            return self.B.pop()
        elif self.A:
            while self.A:
                self.B.append(self.A.pop())
            return self.B.pop()
        else:
            return -1
        


# Your CQueue object will be instantiated and called as such:
# obj = CQueue()
# obj.appendTail(value)
# param_2 = obj.deleteHead()
```

## 4.[剑指 Offer 20. 表示数值的字符串](https://leetcode-cn.com/problems/biao-shi-shu-zhi-de-zi-fu-chuan-lcof/)

有限状态机，略

## 5.[剑指 Offer 24. 反转链表](https://leetcode.cn/problems/fan-zhuan-lian-biao-lcof/)


> 时间O(N):N为链表的长度
>
> 空间O(1):pre，cur，temp都是常数个变量
>
> 用双指针来标记None和首节点，然后暂存下一个节点，从定向当前节点，更新双指针，知道当前节点为空

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        pre, cur = None, head
        while cur: # 最后一个cur为None，pre为实际最后一个节点
            temp = cur.next  # 因为后面要重定向cur，所以需要暂存下一个节点
            cur.next = pre  # 重定向
    
            # 更新下一组节点
            pre = cur
            cur = temp
        return pre  # pre才是实际的节点，cur已经是None了
```

## 6.[剑指 Offer 30. 包含 min 函数的栈](https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/)

> 时间O(1):push(),pop(),top(),min()都是常数数量级操作
>
> 空间O(N):N为输入值的数量，输入栈和非严格降序栈最多数量为2N
>
> 一个栈用来存放输入栈，另一个栈用来存放非严格降序最小栈

```python
class MinStack:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.stack = []
        self.min_stack = []

    def push(self, x: int) -> None:
        self.stack.append(x)
        if not self.min_stack or x <= self.min_stack[-1]:
            self.min_stack.append(x)

    def pop(self) -> None:
        if self.stack:
            if self.min_stack[-1] == self.stack[-1]:
                self.min_stack.pop()
            self.stack.pop()
        

    def top(self) -> int:
        if self.stack:
            return self.stack[-1]
        else:
            return None

    def min(self) -> int:
        if self.min_stack:
            return self.min_stack[-1]
        else:
            return None


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(x)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.min()
```

## 7.[剑指 Offer 35. 复杂链表的复制](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/)

> 时间O(N):两次遍历原始链表
>
> 空间O(N):残存空间含有2N个节点
>
> 两次遍历复杂链表，第一次构造{原节点：新节点值}对，第二次用来给新节点定向next和random值

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random
"""
class Solution:
    def copyRandomList(self, head: 'Node') -> 'Node':
        if not head: return None  # 0输入情况判断
        dic = {}  
  
        cur = head  # 构造暂存{原节点:新节点含节点值}字典
        while cur:
            dic[cur] = Node(cur.val)
            cur = cur.next
  
        cur = head  # 为新节点定义next和random指向
        while cur:
            dic[cur].next = dic.get(cur.next)
            dic[cur].random = dic.get(cur.random)
            cur = cur.next
        return dic[head]  # 返回原始头节点对应的新节点
```

## 8.[剑指 Offer 58 - II. 左旋转字符串](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

> 时间O(N):N为输入字符串的长度
>
> 空间O(N):新旧字符串的长度都是N
>
> 根据n值进行列表相加

```python
class Solution:
    def reverseLeftWords(self, s: str, n: int) -> str:
        res = []

        for i in range(n, len(s)):
            res.append(s[i])
        for i in range(n):
            res.append(s[i])
  
        return ''.join(res)
```

## 9.[剑指 Offer 59 - I. 滑动窗口的最大值](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)

> 时间O(N):N为数组的长度，线性遍历用N次，每个元素入队和出队最多一共2N词，总共3N次
>
> 空间O(K):双端队列最多存储K个元素
>
> 一个单调队列用来存放输入值，另一个双端队列用来存放非严格降序的输入值

```python
import collections

class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        deque = collections.deque()
        n = len(nums)
        res = []
        # 先根据k建立滑窗，并保存第一个滑窗的结果
        for i in range(k):
            while deque and deque[-1] < nums[i]:
                deque.pop()
            deque.append(nums[i])
        res.append(deque[0])
        # 后根据滑窗来滑动
        for i in range(k, n):
            if nums[i-k] == deque[0]:
                deque.popleft()
            while deque and deque[-1] < nums[i]:
                deque.pop()
            deque.append(nums[i])
            res.append(deque[0])
        return res

class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        if not nums: return []
        res = []
        for i in range(len(nums) - k + 1):
            res.append(max(nums[i:i +k]))
        return res

```

## 10.[剑指 Offer 59 - II. 队列的最大值](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/)

> max_value()时间O(1)
>
> push_back()均摊时间O(1)
>
> pop_front()均摊时间O(1)
>
> 空间O(N):最多两个队列一共保存2N个元素
>
> 一个单调队列用于存放输入值，一个双端队列用来存放非严格降序的输入值

```python
import queue

class MaxQueue:

    def __init__(self):
        self.queue = queue.Queue()  # 单调队列用于保存入队和出队的元素
        self.deque = queue.deque()  # 双端队列用于保存非严格递减的最大元素

    def max_value(self) -> int:  
        return self.deque[0] if self.deque else -1  # 如果没有值就返回-1

    def push_back(self, value: int) -> None:
        self.queue.put(value)  # 单调队列先添加
        while self.deque and self.deque[-1] < value: self.deque.pop()  # 双端队列将小于新添加的元素都右弹出
        self.deque.append(value)  # 双端队列后添加，这样就能保证非严格递减

    def pop_front(self) -> int:
        if self.queue.empty(): return -1  # 单调队列如果为空就返回-1
        value = self.queue.get()  # 这里已经弹出了单调队列队首，put()与get()两个方法
        if value == self.deque[0]:  # 如果弹出的值跟双端队列最大值相等就业一起弹出，不然不弹出，这样就能保存最大值了
            self.deque.popleft()
        return value
  


# Your MaxQueue object will be instantiated and called as such:
# obj = MaxQueue()
# param_1 = obj.max_value()
# obj.push_back(value)
# param_3 = obj.pop_front()
```

## 11.[剑指 Offer 67. 把字符串转换成整数](https://leetcode-cn.com/problems/ba-zi-fu-chuan-zhuan-huan-cheng-zheng-shu-lcof)

> 时间O(N):N个字符需要遍历
>
> 空间O(N):最多N个字符要保存在str变量上

```python
class Solution:
    def strToInt(self, str: str) -> int:
        str = str.strip()  # 去除前面空格
        INT_MAX, INT_MIN, BOUND = 2 ** 31 -1, -2 ** 31, 2 ** 31 // 10  # 用于记录最大最小值和越界值
        sign, res = 1, 0  # 用于记录符号标记和数字和
        i = 1 # 用于记录开始的index
  
        if str[0] == '-': sign = -1  # 如果为负号，则初始值只需要改sign
        elif str[0] != '+': i = 0  # 如果不是正号，则index改成1；另一种情况就是默认的正号

        for c in str[i:]:
            if not '0' <= c <= '9': break  # 碰到数字外的就跳出
            if res > BOUND or res == BOUND and c > '7': return INT_MAX if sign == 1 else INT_MIN  # 越界处理
            res = 10 * res + ord(c) - ord('0')  # 累加
        return sign * res

```

# 三，动态规划

> 动态规划简介

主要特点

包含了「分治思想」、「空间换时间」、「最优解」等多种基石算法思想

求解框架

状态定义： 构建问题最优解模型，包括问题最优解的定义、有哪些计算解的自变量；
初始状态： 确定基础子问题的解（即已知解），原问题和子问题的解都是以基础子问题的解为起始点，在迭代计算中得到的；
转移方程： 确定原问题的解与子问题的解之间的关系是什么，以及使用何种选择规则从子问题最优解组合中选出原问题最优解；
返回值： 确定应返回的问题的解是什么，即动态规划在何处停止迭代；

## 1.[剑指 Offer 10- I. 斐波那契数列](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/)

> 时间O(N):第N个数字需要遍历N次
>
> 空间O(1):常数个变量

```python
class Solution:
    def fib(self, n: int) -> int:
        a, b = 0, 1
        for _ in range(n):
            temp = a + b
            a = b
            b = temp % 1000000007
        return a
```

## 2.[剑指 Offer 10- II. 青蛙跳台阶问题](https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/)

> 时间O(N):第N个台阶需要遍历N次
>
> 空间O(1):常数个变量

```python
class Solution:
    def numWays(self, n: int) -> int:
        a, b = 1,1
        for _ in range(n):
            temp = a + b
            a = b
            b = temp % 1000000007
        return a
```

## 3.[剑指 Offer 19. 正则表达式匹配](https://leetcode-cn.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof/)

> 时间O(MN):MN为dp矩阵遍历的次数，M行N列
>
> 空间O(MN):MN为矩阵的大小，M行N列

```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        # 定义所需变量
        m, n = len(s) + 1, len(p) + 1
        dp = [[False] * n for _ in range(m)]

        # 初始化矩阵
        dp[0][0] = True  # 空字符串能匹配
        for j in range(2, n, 2):  # 空字符和偶数的'*'能匹配
            dp[0][j] = dp[0][j - 2] and p[j - 1] == '*'

        # 更新矩阵
        for i in range(1, m):
            for j in range(1, n):
                if p[j - 1] == '*':  # 分为是'*'和不是'*'的情况
                    if dp[i][j - 2]: dp[i][j] = True  # p的前一个出现0次的时候
                    if dp[i - 1][j] and s[i - 1] == p[j - 2]:dp[i][j] = True  # 出现多次的情况，p的前一个等于新的s
                    if dp[i - 1][j] and p[j - 2] == '.':dp[i][j] = True  # 出现过次的情况，p的前一个等于'.' 
                else:
                    if dp[i - 1][j - 1] and p[j - 1] == s[i - 1]:dp[i][j] = True  # 之前匹配的情况下，新的p等于新的s
                    if dp[i - 1][j - 1] and p[j - 1] == '.':dp[i][j] = True  # 之前匹配的情况下，新的p等于'.'
  
        return dp[-1][-1]
```

## 4.[剑指 Offer 42. 连续子数组的最大和](https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/)

> 时间O(N):遍历N-1次列表
>
> 空间O(1):用原来的列表做动态规划，不用额外的空间

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        for i in range(1,len(nums)):
            nums[i] += max(nums[i - 1], 0)
        return max(nums)
```

## 5.[剑指 Offer 46. 把数字翻译成字符串](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

> 时间O(N):遍历N-1次字符串
>
> 空间O(N):字符串占用num的N长度

```python
class Solution:
    def translateNum(self, num: int) -> int:
        s = str(num)
        a = b = 1
        for i in range(2, len(s) + 1):  # 2是因为第一个已经默认了，从前两个开始，加一是因为索引最后取不到
            temp = a + b if '10' <= s[i - 2:i] <= '25' else b
            a = b
            b = temp
        return b
```

## 6.[剑指 Offer 47. 礼物的最大价值](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof)

> 时间O(MN):遍历M行N列
>
> 空间O(1):常数个额外变量

```python
class Solution:
    def maxValue(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])  # M行N列

        # 初始化第一列的累积价值
        for i in range(1, m):
            grid[i][0] += grid[i - 1][0]

        # 初始化第一行的累积价值
        for j in range(1, n):
            grid[0][j] += grid[0][j - 1]

        # 从第二行第二列开始，遍历整个棋盘
        for i in range(1, m):
            for j in range(1, n):
                # 动态规划递推公式：grid[i][j] = grid[i][j] + max(grid[i - 1][j], grid[i][j - 1])
                # 当前格子的最大价值 = 当前格子价值 + max(上方格子累积价值, 左方格子累积价值)
                grid[i][j] += max(grid[i - 1][j], grid[i][j - 1])

        # 返回最后一个格子的累积价值，即最大价值
        return grid[-1][-1]
```

## 7.[剑指 Offer 48. 最长不含重复字符的子字符串](https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)

> 时间O(N):遍历N个字符
>
> 空间O(N):最差N个字符都要保存在dic中

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        # 初始化最长不重复子串长度和当前不重复子串长度
        res = temp = 0
        # 创建一个字典用于存储字符和其在字符串中的索引
        dic = {}
        # 遍历字符串
        for i in range(len(s)):
            # 从字典中获取当前字符的索引，如果字符不存在，则返回-1
            j = dic.get(s[i], -1)
            # 更新当前字符在字典中的索引
            dic[s[i]] = i
            # 如果当前不重复子串长度小于当前索引与重复字符的索引之差，则更新当前不重复子串长度；否则，将当前不重复子串长度设置为当前索引与重复字符的索引之差
            temp = (temp + 1) if temp < i - j else i - j
            # 更新最长不重复子串长度
            res = max(temp, res)
        return res
```

## 8.[264. 丑数 II](https://leetcode-cn.com/problems/ugly-number-ii/)

> 时间O(N):遍历N次循环
>
> 空间O(N):使用N个dp长度

```python
class Solution:
    def nthUglyNumber(self, n: int) -> int:
        # 初始化三个指针，分别指向下一个将要乘以2、3、5的丑数在列表中的位置
        i2, i3, i5 = 0, 0, 0
        # 初始化一个列表，用于保存生成的丑数
        ugly_number = [1]
        # 循环生成下一个丑数，直到生成第n个丑数
        while len(ugly_number) < n:
            # 分别计算将要乘以2、3、5的下一个丑数
            ugly2 = ugly_number[i2] * 2
            ugly3 = ugly_number[i3] * 3
            ugly5 = ugly_number[i5] * 5
            # 找出这三个数中最小的一个，即为下一个丑数
            next_number = min(ugly2, ugly3, ugly5)
            # 将指向最小值的指针向后移动一位
            if next_number == ugly2:
                i2 += 1
            if next_number == ugly3:
                i3 += 1
            if next_number == ugly5:
                i5 += 1
            # 将新生成的丑数添加到列表中
            ugly_number.append(next_number)
        # 返回第n个丑数
        return ugly_number[-1]
```



## 10.[剑指 Offer 63. 股票的最大利润](https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof/)

> 时间O(N):遍历N个价格
>
> 空间O(1):常数个额外变量

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        min_price, max_profit = float('inf'), 0
        for price in prices:
            min_price = min(min_price, price) # 更新最低买入价格
            max_profit = max(max_profit, price - min_price) # 更新最大利润
        return max_profit
```

# 四，搜索与回溯算法

## 1.[剑指 Offer 12. 矩阵中的路径](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/)

> 时间O(MN$3^K$):遍历MN个元素，每个元素最多有$3^K$种可能
>
> 空间O(MN):最多递归深度为每个元素都找到，共MN个

```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        def dfs(i, j, k):
            if not 0 <= i < len(board) or not 0 <= j < len(board[0]) or board[i][j] != word[k]: return False  # 超出矩阵或者字母不符合
            if k == len(word) - 1: return True  # 如果到了最后一个字母返回True表示找到了
            board[i][j] = ''  # 替换掉当前的值
            res = dfs(i + 1, j, k + 1) or dfs(i - 1, j, k + 1) or dfs(i, j + 1, k + 1) or dfs(i, j - 1, k + 1)  # 向四个方向递归
            board[i][j] = word[k]  # 还原当前值
            return res  # 返回当前递归状态下的某个字母是否匹配

        for i in range(len(board)):  # 行遍历，这样如果是空矩阵直接返回[]
            for j in range(len(board[0])):  # 列遍历
                if dfs(i, j, 0): return True

        return False
```

## 2.[剑指 Offer 13. 机器人的运动范围](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

> 时间O(N)

```python
class Solution:
    def movingCount(self, m: int, n: int, k: int) -> int:
        def dfs(i, j , si, sj):
            if i >= m or j >= n or k < si + sj or (i, j) in visited: return 0  # 当i，j越界或两个位数加起来超过k或(i,j)曾经到过
            visited.add((i,j))  # 记录到过的位置
            return 1 + dfs(i + 1,j, si + 1 if (i + 1) % 10 else si - 8, sj) + \  #
                       dfs(i, j + 1, si, sj + 1 if (j + 1) % 10 else sj - 8)
    
        visited = set()

        return dfs(0, 0, 0, 0)

```

## 3.[剑指 Offer 26. 树的子结构](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/)

> 时间O(MN):M为A树的节点数量，N为B树的节点数量
>
> 空间O(M):M为A树的节点数量，最多递归M层

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSubStructure(self, A: TreeNode, B: TreeNode) -> bool:
        def recur(A,B):
            if not B: return True  # B树背遍历完全
            if not A or A.val != B.val: return False  # 没有A树了，AB值不匹配
            return recur(A.left, B.left) and recur(A.right, B.right)  # 递归左数，右树

        return bool(A and B) and (recur(A, B) or self.isSubStructure(A.left, B) or self.isSubStructure(A.right, B))  # AB树都需要存在同时有任何一队节点符合子树要求
```

## 4.[剑指 Offer 27. 二叉树的镜像](https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/)

> 时间O(N):N为二叉树的节点数量
>
> 空间O(N):最多递归节点数量大小的栈空间

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def mirrorTree(self, root: TreeNode) -> TreeNode:
        if not root: return  # 设定终止情况
        temp = root.left  # 递归后左子树会变，需要暂存
        root.left = self.mirrorTree(root.right)
        root.right = self.mirrorTree(temp)
        return root
```

## 5.[剑指 Offer 28. 对称的二叉树](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/)

> 时间O(N):最多一对节点计算一次，一共N/2次
>
> 空间O(N):最多递归N/2次的深度

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        def recur(L, R):
            if not L and not R: return True
            if not L or not R or L.val != R.val: return False
            return recur(L.left, R.right) and recur(L.right, R.left)

        return recur(root.left, root.right) if root else True
```

## 6.[剑指 Offer 32 - I. 从上到下打印二叉树](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/)

> 时间O(N):N为节点数量
>
> 空间O(N):最差有N/2个树节点同时在deque

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def levelOrder(self, root: TreeNode) -> List[int]:
        if not root: return []
        deque, res = collections.deque(), []
        deque.append(root)
        while deque:
            node = deque.popleft()
            res.append(node.val)
            if node.left:deque.append(node.left)
            if node.right:deque.append(node.right)
        return res
```

## 7.[剑指 Offer 32 - II. 从上到下打印二叉树 II](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/)

> 时间O(N):N为节点数量
>
> 空间O(N):最多N/2个deque暂存空间

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root: return []
        deque, res  = collections.deque(), []
        deque.append(root)

        while deque:
            temp = []
            for _ in range(len(deque)):
                node = deque.popleft()
                temp.append(node.val)
                if node.left: deque.append(node.left)
                if node.right: deque.append(node.right)
            res.append(temp)

        return res
```

## 8.[剑指 Offer 32 - III. 从上到下打印二叉树 III](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

> 时间O(N):N为节点数量
>
> 空间O(N):最多N/2个deque暂存空间

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root: return []
        deque, res = collections.deque(), []
    
        deque.append(root)
        while deque:
            temp = collections.deque()
            for _ in range(len(deque)):
                node = deque.popleft()
                if len(res) % 2: temp.appendleft(node.val)
                else:temp.append(node.val)
                if node.left: deque.append(node.left)
                if node.right:deque.append(node.right)
            res.append(list(temp))
        return res
```

## 9.[剑指 Offer 34. 二叉树中和为某一值的路径](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/)

> 时间O(N):每个节点遍历一次
>
> 空间O(N):最多每个节点都储存path中

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def pathSum(self, root: TreeNode, target: int) -> List[List[int]]:
        res, path = [], []
        def recur(node, tar):
            if not node: return 
            tar -= node.val
            path.append(node.val)
            if not node.right and not node.left and tar == 0:  # 路径满足条件
                res.append(list(path))  # 要加list，深拷贝，不然path列表会随着后面的变化而变化
            recur(node.left, tar)  # 左子树搜索
            recur(node.right, tar)  # 右子树所搜
            path.pop()  # 路径退回

        recur(root, target)
        return res
```

## 10.[剑指 Offer 36. 二叉搜索树与双向链表](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/)

## 11.[剑指 Offer 37. 序列化二叉树](https://leetcode-cn.com/problems/xu-lie-hua-er-cha-shu-lcof/)

## 12.[剑指 Offer 38. 字符串的排列](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/)

> 时间O(N!N):N!为可能性，每次join占用N的时间
>
> 空间O($N^2$):递归深度为N，dic集合中最多存有N个字母

```python
class Solution:
    def permutation(self, s: str) -> List[str]:
        c, res = list(s), []
        def dfs(x):
            if x == len(c) - 1: 
                res.append(''.join(c))  # 到底了就添加新情况
                return 
            dic = set()  # 暂存已经固定的字母
            for i in range(x, len(c)):
                if c[i] in dic: continue  # 如果固定过就跳过
                dic.add(c[i])
                c[i], c[x] = c[x], c[i]
                dfs(x + 1)
                c[i], c[x] = c[x], c[i]
        dfs(0)
        return res
```

## 13.[剑指 Offer 54. 二叉搜索树的第k大节点](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)

> 时间O(N)
>
> 空间O(N)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def kthLargest(self, root: TreeNode, k: int) -> int:
        def dfs(node):
            if not node: return
            dfs(node.right)
            if self.k == 0: return
            self.k -= 1
            if self.k == 0: self.res = node.val
            dfs(node.left)

        self.k = k
        dfs(root)
        return self.res
```

## 14.[剑指 Offer 55 - I. 二叉树的深度](https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/)

> 时间O(N)
>
> 空间O(N)

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        if not root:return 0
        queue, res = [root], 0
  
        while queue:
            temp = []
            for node in queue:
                if node.left: temp.append(node.left)
                if node.right: temp.append(node.right)
            queue = temp
            res += 1
  
        return res
```

## 15.[剑指 Offer 55 - II. 平衡二叉树](https://leetcode-cn.com/problems/ping-heng-er-cha-shu-lcof/)

> 迷

```python
class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        def recur(root):
            if not root: return 0
            left = recur(root.left)
            if left == -1: return -1
            right = recur(root.right)
            if right == -1: return -1
            return max(left, right) + 1 if abs(left - right) <= 1 else -1

        return recur(root) != -1
```

## 16.[剑指 Offer 64. 求1+2+…+n](https://leetcode-cn.com/problems/qiu-12n-lcof/)

> 时间O(N):N次递归
>
> 空间O(N):N的递归深度

```python
class Solution:
    def __init__(self):
        self.res = 0
    def sumNums(self, n: int) -> int:
        n > 1 and self.sumNums(n - 1)
        self.res += n
        return self.res
```

## 17.[剑指 Offer 68 - I. 二叉搜索树的最近公共祖先](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/)

## 18.[剑指 Offer 68 - II. 二叉树的最近公共祖先](https://leetcode-cn.com/problems/er-cha-shu-de-zui-jin-gong-gong-zu-xian-lcof/)

# 五，分治算法


## 1.[剑指 Offer 07. 重建二叉树](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/)

> 时间O(N):N为节点数量
>
> 空间O(N):中序遍历字典占N个空间，最多树的递归深度为N

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        def recur(root, left, right):
            if left > right: return 
            node = TreeNode(preorder[root])  # 建立根节点
            i = dic[preorder[root]]  # 获取根节点在中序遍历中的位置
            node.left = recur(root + 1, left, i - 1)  # 建立左子树
            node.right = recur(i - left + root + 1, i + 1, right)  # 建立右子树
            return node

        dic = {}
        for i in range(len(inorder)):  # 为中序遍历构造字典将查找节点的时间复杂度O(N)->O(1)
            dic[inorder[i]] = i
  
        return recur(0, 0, len(inorder) - 1)


```



## 2.[剑指 Offer 16. 数值的整数次方](https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/)

> 迷

```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if x == 0: return 0
        res = 1
        if n < 0: x, n = 1 / x, -n
        while n:
            if n & 1: res *= x
            x *= x
            n >>= 1
        return res 

```



## 3.[剑指 Offer 17. 打印从1到最大的n位数](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)

> 时间O($10^n$):建立列表用$10^n$
>
> 空间O(1):建立列表需使用o(1)大小的额外空间(列表作为返回结果，不计入额外空间)

```python
class Solution:
    def printNumbers(self, n: int) -> List[int]:
        res = []
        for i in range(1,10 ** n):
            res.append(i)
        return res
```

## 4.[剑指 Offer 33. 二叉搜索树的后序遍历序列](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)

```python
class Solution:
    def verifyPostorder(self, postorder: List[int]) -> bool:
        def recur(left, right):
            if left >= right: return True
            p = left
            while postorder[p] < postorder[right]: p += 1
            m = p
            while postorder[p] > postorder[right]: p += 1
            return p == right and recur(left, m - 1) and recur(m, right - 1)

        return recur(0, len(postorder) - 1)
```




## 5.[剑指 Offer 51. 数组中的逆序对](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/)





# 六，排序

## 1.[剑指 Offer 40. 最小的k个数](https://leetcode.cn/problems/zui-xiao-de-kge-shu-lcof/)

```python
class Solution:
    def getLeastNumbers(self, arr: List[int], k: int) -> List[int]:
        def quicksort(arr, l, r):
            if l >= r: return  # 跳出条件
            i, j = l, r
            while i < j:  # 哨兵划分
                while i < j and arr[j] >= arr[l]: j -= 1
                while i < j and arr[i] <= arr[l]: i += 1
                arr[i], arr[j] = arr[j], arr[i]
            arr[l], arr[i] = arr[i], arr[l]
            quicksort(arr, l, i - 1)  # 递归
            quicksort(arr, i + 1, r)
        quicksort(arr, 0, len(arr) - 1)
        return arr[:k]
```



## 2.[剑指 Offer 41. 数据流中的中位数](https://leetcode.cn/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/)

```python
from heapq import *

class MedianFinder:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.small =  []
        self.big = []

    def addNum(self, num: int) -> None:
        if len(self.small) != len(self.big):
            heappush(self.small, num)
            heappush(self.big, -heappop(self.small))  # 用符号模拟大顶堆
        else:
            heappush(self.big, -num)
            heappush(self.small, -heappop(self.big))

    def findMedian(self) -> float:
        return self.small[0] if len(self.small) != len(self.big) else (self.small[0] - self.big[0]) / 2.0
```



##  3.[剑指 Offer 45. 把数组排成最小的数](https://leetcode.cn/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

```python
class Solution:
    def minNumber(self, nums: List[int]) -> str:
        def quicksort(arr, l, r):
            if l >= r: return  # 跳出情况
            i, j = l, r
            while i < j:
                while i < j and arr[l] + arr[j] <= arr[j] + arr[l]: j -= 1  # 新的判断标准
                while i < j and arr[l] + arr[i] >= arr[i] + arr[l]: i += 1
                arr[i], arr[j] = arr[j], arr[i]
            arr[l], arr[i] = arr[i], arr[l]
            quicksort(arr, i + 1, r)
            quicksort(arr, l, i - 1)
        arr = [str(i) for i in nums]  # 利用字符串来比较大小
        quicksort(arr, 0, len(arr) - 1)
        return ''.join(arr)
```



## 4.[剑指 Offer 61. 扑克牌中的顺子](https://leetcode.cn/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)

```python
class Solution:
    def isStraight(self, nums: List[int]) -> bool:
        ma, mi = 0, 14
        repeat = set()
        for num in nums:
            if num == 0: continue
            ma = max(ma, num)
            mi = min(mi, num)
            if num in repeat: return False
            repeat.add(num)
        return ma - mi < 5
```



# 七.查找算法

## 1.[剑指 Offer 03. 数组中重复的数字](https://leetcode.cn/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

```python
class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        dic = {}
        for num in nums:
            dic[num] = num in dic
        for k, v in dic.items():
            if v: return k
        return ''
```

## 2.[剑指 Offer 04. 二维数组中的查找](https://leetcode.cn/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

```python
class Solution:
    def findNumberIn2DArray(self, matrix: List[List[int]], target: int) -> bool:
        i, j = len(matrix) - 1, 0
        while i >= 0 and j <= len(matrix[0]) - 1:
            if target > matrix[i][j]: j += 1
            elif target < matrix[i][j]: i -= 1
            else: return True
        return False
```

## 3.[剑指 Offer 11. 旋转数组的最小数字](https://leetcode.cn/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)

```python
class Solution:
    def minArray(self, numbers: List[int]) -> int:
        i, j = 0, len(numbers) - 1
        m = 0
        while i < j:
            m = (i + j) // 2
            if numbers[m] < numbers[j]: j = m
            elif numbers[m] > numbers[j]: i = m + 1
            else: j -= 1
        return numbers[i]

class Solution:
    def minArray(self, numbers: List[int]) -> int:
		return min(numbers)        
```



## 4.[剑指 Offer 50. 第一个只出现一次的字符](https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/)

> 时间O(N):遍历N个字符
>
> 空间O(1):最多只有26个小写字母

```python
class Solution:
    def firstUniqChar(self, s: str) -> str:
        dic = {}
        for c in s:
            dic[c] = c not in dic
        for k, v in dic.items():
            if v: return k
        return ' '
```

## 5.[剑指 Offer 53 - I. 在排序数组中查找数字 I](https://leetcode.cn/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/)

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        i, j = 0, len(nums) - 1
        while i <= j:  # 找左边界
            m = (i + j) // 2
            if nums[m] < target: i = m + 1
            elif nums[m] > target: j = m - 1
            else: j = m - 1
        left = j
        if not nums:return 0
        if (left + 1) < len(nums) and nums[left + 1] != target: return 0
        i, j = 0, len(nums) - 1
        while i <= j:
            m = (i + j) // 2
            if nums[m] > target: j = m - 1
            elif nums[m] < target: i = m + 1
            else: i = m + 1
        return i - left - 1
```



## 6.[剑指 Offer 53 - II. 0～n-1中缺失的数字](https://leetcode.cn/problems/que-shi-de-shu-zi-lcof/)

```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        i, j = 0, len(nums) - 1
        while i <= j:
            m = (i + j) // 2
            if nums[m] == m: i = m + 1
            elif nums[m] > m: j = m - 1
        return i
```



# 八，双指针

## 1.[剑指 Offer 18. 删除链表的节点](https://leetcode.cn/problems/shan-chu-lian-biao-de-jie-dian-lcof)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None
class Solution:
    def deleteNode(self, head: ListNode, val: int) -> ListNode:
        if head.val == val: return head.next
        pre, cur = head, head.next
        while cur:
            if cur.val == val:
                pre.next = cur.next
                break
            pre, cur = cur, cur.next
        return head
```



## 2.[剑指 Offer 21. 调整数组顺序使奇数位于偶数前面](https://leetcode.cn/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/)

```python
class Solution:
    def exchange(self, nums: List[int]) -> List[int]:
        i, j = 0, len(nums) - 1
        while i < j:
            while i < j and nums[i] % 2 != 0: i += 1
            while i < j and nums[j] % 2 == 0: j -= 1
            nums[i], nums[j] = nums[j], nums[i]
        return nums
```

## 3.[剑指 Offer 22. 链表中倒数第k个节点](https://leetcode.cn/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)

```python
class Solution:
    def getKthFromEnd(self, head: ListNode, k: int) -> ListNode:
        nums = 0
        node = head
        while node:
            node = node.next
            nums += 1
        node = head
        nums = nums - k
        num = 0
        while node:
            if nums == num:
                return node
            node = node.next
            num += 1
```



# 九，位运算

# 十，数字

# 十一，模拟
