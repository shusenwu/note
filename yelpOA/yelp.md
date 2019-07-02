### Business Messaging Response Rate
题目：  
https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=469087&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3089%5D%5Bvalue%5D%5B5%5D%3D5%26searchoption%5B3089%5D%5Btype%5D%3Dcheckbox%26searchoption%5B3046%5D%5Bvalue%5D%3D36%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline  
```python
def converRate(bizId, messages):
    involed = set()
    responsed = set()

    for m in messages:
        s, r, c = m['s'], m['r'], m['c']
        if bizId in (s, r):
            involed.add(c)
        if s == bizId:
            responsed.add(c)
    return int(len(responsed) *1.0 / len(involed) * 100)

messages = [
    {'s': 1, 'r': 42, 'c': 1},
    {'s': 42, 'r': 1, 'c': 1},
    {'s': 2, 'r': 42, 'c': 2},
    {'s': 2, 'r': 42, 'c': 2},
    {'s': 3, 'r': 88, 'c': 3},
    {'s': 3, 'r': 42, 'c': 4}
]
if __name__ == '__main__':
    print converRate(42, messages)
```
