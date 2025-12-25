```python
import random

prime_for_miller_rabin = [2,3,5,7,11,13,17,19,23,29,31,37]
prime_factors_count = dict()

def power(a,b,c):
    if b == 0: return 1
    if b == 1: return a % c
    h = power(a, b>>1, c) % c
    h = (h * h) % c
    if b%2 == 1: return (h*a)%c
    return h

def miller_rabin(x):
    if x <= 1: return False
    if x <= 3: return True
    if x%2 == 0: return False
    
    for prime in prime_for_miller_rabin:
        if x == prime: return True
        if x % prime == 0: return False
        
        t = (x-1) >> 1
        may_prime = False
        while True:
            v = power(prime, t, x)
            if v == x-1:
                may_prime = True
                break
            if t%2 == 1:
                if v == x-1 or v == 1:
                    may_prime = True
                break
            t = t>>1
        
        if x > 40 and may_prime == False:
            return False
    
    if x > 40: return True
    return False

def gcd(a,b):
    if a == 0: return b
    if b == 0: return a
    if a < b:
        t = a
        a = b
        b = t
    if a%b == 0: return b
    return gcd(b, a%b)

def pollard_rho(x):
    if x == 1: return
    if x%2 == 0:
        try:
            prime_factors_count[2] = prime_factors_count[2]+1
        except:
            prime_factors_count[2] = 1
        pollard_rho(x>>1)
        return
    if miller_rabin(x):
        try:
            prime_factors_count[x] = prime_factors_count[x]+1
        except:
            prime_factors_count[x] = 1
        return
    
    c = random.randint(1,20)
    a = random.randint(2,x-1)
    b = a
    v = 1
    
    def f(g):
        return (g*g + c)%x
    
    while v == 1:
        a = f(a)
        b = f(f(b))
        v = gcd(abs(a-b), x)
    
    pollard_rho(v)
    pollard_rho(x//v)


N = int(input())
a = map(int, input().split())
for i in a:
    pollard_rho(i)

count_max, count = 0, 0
for prime in prime_factors_count:
    cnt = prime_factors_count[prime]
    if cnt > count_max:
        count_max = cnt
        count = 1
    elif cnt == count_max:
        count += 1

ans = 1
for _ in range(count):
    ans = ans << 1

print(count_max)
print(ans-1)
```
