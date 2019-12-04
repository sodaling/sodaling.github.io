KMP算法是经典字符串匹配算法，时间复杂度为O(m+n)，n为主串长度，m为模式串长度。

过了一遍知乎这个答案，更加自己的理解改成了python版本。

如何更好的理解和掌握 KMP 算法? - 海纳的回答 - 知乎
https://www.zhihu.com/question/21923021/answer/281346746

```python
def kmp(long_srt, find_str):
    def _find_next(find_str):
        len_find_str = len(find_str)
        nex = [0] * len_find_str
        nex[0] = -1
        i, j = 0, -1
        while i < len_find_str - 1:
            if j == -1 or find_str[i] == find_str[j]:  # 索引不能为-1，所以加判断条件
                i += 1
                j += 1
                nex[i] = j
            else:
                j = nex[j]  # 不匹配时候就置为0了
        return nex

    nex = _find_next(find_str)
    i = j = 0
    while i < len(long_srt) and j < len(find_str):
        if j == -1 or long_srt[i] == find_str[j]:
            # 两步都相同都齐齐往前挪动
            i += 1
            j += 1
        else:
            j = nex[j]  # 出现不同j就往回退，退到模式觉得重合可以从这个下标开始的地方。也因为是这样，有可能会得到-1

    if j == len(find_str):
        return i - j
    else:
        return -1
```
