```python
def solution(s):
    answer = []
    unions = s[2:-2].split("},{")
    
    dic = {}
    for union in unions:
        u = list(map(int, union.split(",")))
        for i in u:
            dic[i] = dic.get(i,0) + 1
            
    dic = sorted(dic.items(),key=lambda x : x[1],reverse=True)
    return [x[0] for x in dic]
```
