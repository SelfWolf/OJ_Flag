# 排序算法

------

## 冒泡排序

```python
def bubble_sort(num):
    """
    冒泡排序：两两比较，总是将较大的放在后面，这样每轮比较完后，当前轮次最大值总排在末尾
    稳定性：一种稳定排序算法
    时间复杂度：O(n^2)
    分析：如果数据本身有序，还是要两两比较，复杂度不变；可以设置标记位，如果当前轮次没有发生交换
        那么就结束排序过程
    :param num:
    :return:
    """
    for i in range(len(num)):
        for j in range(len(num) - i - 1):
            if num[j] > num[j+1]:
                num[j], num[j+1] = num[j+1], num[j]
    return num
```

## 快速排序

```python
def quick_sort(num):
    """
    快速排序：选定一个基准，然后在数组中将小于基准的数移动到基准左边，大于基准的数移动到基准右边
        以基准划分的两个部分分别再次进行快速排序
    时间复杂度：O(nlogn)
    空间复杂度：O(nlogn)
    分析：如果数据初始有序而且选定第一个元素为基准，导致最差时间复杂度
    :param num:
    :return:
    """
    def partition(_left, _right, _num):
        key = _left
        while _left < _right:
            while _left < _right and _num[_right] >= _num[key]:
                _right -= 1
            while _left < _right and _num[_left] <= _num[key]:
                _left += 1
            _num[_left], _num[_right] = _num[_right], _num[_left]
        _num[_left], _num[key] = _num[key], _num[_left]
        return _left

    def _quick_sort(_num, _left, _right):
        if _left > _right:
            return
        mid = partition(_left, _right, num)
        _quick_sort(_num, _left, mid-1)
        _quick_sort(_num, mid+1, _right)
    _quick_sort(num, 0, len(num)-1)
    return num
```

## 插入排序

```python
def insert_sort(num):
    """
    插入排序：
        1. 从第一个数开始，默认是有序的
        2. 取下一个元素，在已排序的元素序列中从后往前扫描
        3. 如果已排序元素大于新元素，将排序元素往后移
        4. 重复步骤3，直到找到合适位置
    时间复杂度：O(n^2)
    空间复杂度：O(1)
    分析：关键点是从后往前遍历
    :param num:
    :return:
    """
    for i in range(1, len(num)):
        j = i
        target = num[i]
        while j > 0 and num[j-1] > num[j]:
            num[j] = num[j-1]
            j -= 1
        num[j] = target
    return num
```

## 选择排序

```python
def select_sort(num):
    """
    选择排序：将数组分为有序和无序两部分，每次从无序中选择一个最小值加入到有序集合中
    时间复杂度：O(n^2)
    不稳定排序
    :param num:
    :return:
    """
    for i in range(len(num) - 1):
        min_ind = i
        for j in range(i+1, len(num)):
            if num[j] < num[min_ind]:
                min_ind = j
        if min_ind != i:
            num[min_ind], num[i] = num[i], num[min_ind]
    return num
```

https://blog.csdn.net/weixin_41571493/article/details/81875088