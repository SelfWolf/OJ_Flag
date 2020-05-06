# 热题100

* 两数之和：给定数组和target，求和为target的两个整数并返回下标

```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        _dict = {}
        for i in range(len(nums)):
            if _dict.get(nums[i]) is not None:
                return [i, _dict[nums[i]]]
            else:
                _dict[target - nums[i]] = i
        return []
```

* 三数之和：给定数组和target=0，计算三个数等于target的三个数的下标

```python
class Solution(object):
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        res = []
        nums = sorted(nums)
        for i in range(len(nums) - 2):
            if i == 0 or nums[i] > nums[i-1]:
                a, b = i+1, len(nums)-1
                while a < b:
                    val = nums[a] + nums[b] + nums[i]
                    if val == 0:
                        res.append([nums[a], nums[b], nums[i]])
                        a += 1
                        b -= 1
                        while a < b and nums[a] == nums[a-1]:
                            a += 1
                        while a < b and nums[b] == nums[b+1]:
                            b -= 1
                    elif val > 0:
                        b -= 1
                    else:
                        a += 1
        return res
```

* 四数之和：给定数组和target，计算四个数等于target的数的下标
  
```python
class Solution(object):
    def fourSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        nums = sorted(nums)
        n = len(nums)
        res = []
        for a in range(n - 3):
            if a > 0 and nums[a-1] == nums[a]:
                continue
            for b in range(a+1, n-2):
                if b > a+1 and nums[b] == nums[b-1]:
                    continue
                c = b+1
                d = n - 1
                while c < d:
                    val = nums[a] + nums[b] + nums[c] + nums[d]
                    if val == target:
                        res.append([nums[a], nums[b], nums[c], nums[d]])
                        c += 1
                        d -= 1
                        while c < d and nums[c-1] == nums[c]:
                            c += 1
                        while c < d and nums[d+1] == nums[d]:
                            d -= 1
                    elif val > target:
                        d -= 1
                    else:
                        c += 1
        return res
```

* 两数相加：两个链表逆序存储两个数字，求相加的和

```python
class Solution(object):
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        if not l1:
            return l2
        if not l2:
            return l1
        res = ListNode(0)
        cur = res
        flag = 0
        while l1 or l2:
            tmp_sum = 0
            if l1:
                tmp_sum += l1.val
                l1 = l1.next
            if l2:
                tmp_sum += l2.val
                l2 = l2.next
            number = (tmp_sum + flag) % 10
            flag = (tmp_sum + flag) // 10
            res.next = ListNode(number)
            res = res.next
            if flag:
                res.next = ListNode(1)
        return cur.next
```

* 两数相加变种：两个链表顺序存储两个数字，求相加的和
