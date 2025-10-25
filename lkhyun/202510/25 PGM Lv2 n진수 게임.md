```python
def solution(n, t, m, p):
    answer = ''
    total = ''
    cur = 0
    while len(total) <= t*m:
        total += convert(cur,n)
        cur+=1
    
    for i in range(t):
        answer += total[i*m + p - 1]
    return answer

def convert(num, base):
    
    if num == 0:
        return '0'
    
    digit = "0123456789ABCDEF"
    result = ''
    while num > 0:
        result = digit[num%base] + result
        num //= base
        
    return result
```
