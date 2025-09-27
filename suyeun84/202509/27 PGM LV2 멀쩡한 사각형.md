```java
class Solution {
	public long solution(int w, int h) {
		long answer = (long)w * (long)h;
        
		long wl = (long)w / gcd(w, h);
		long hl = (long)h / gcd(w, h);
		
		answer -= (wl + hl - 1) * gcd(w, h); 
		
		return answer;
	}

	//최대 공약수 (유클리드 호제법)
	private static long gcd(long w, long h) {
		if(h == 0) {
			return w;
		}
		return gcd(h, w % h);
	}
}
```
