```python

S = input()
P = input()

dp = [0 for _ in range(len(P))]
for i in range(len(P)):
    if P[:i+1] in S:
        dp[i] = 1
        continue
        
    j = 1
    dp[i] = i+1
    while i-j>=0:
            
        if P[i-j+1:i+1] not in S:
            break
        
        dp[i] = min(dp[i], dp[i-j] + 1)
        j+=1

print(dp[len(P)-1])

```
