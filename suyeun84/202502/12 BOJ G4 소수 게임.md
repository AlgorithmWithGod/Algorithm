```java
import java.util.*;
import java.io.*;

class Solution
{
	static ArrayList<Integer> dList;
	static ArrayList<Integer> gList;
	static long dScore = 0;
	static long gScore = 0;
	static boolean[] prime = new boolean[5000001];
	static boolean[] primeExist = new boolean[5000001];
	public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        dList = new ArrayList<>();
        gList = new ArrayList<>();
        
        primeNumber();
        int N = Integer.parseInt(st.nextToken());
        for (int i = 0; i < N; i++) {
        	st = new StringTokenizer(br.readLine());
        	int d = Integer.parseInt(st.nextToken());
        	int g = Integer.parseInt(st.nextToken());
        	//1. 소수 아닌 수 -> 상대방은 지금까지 상대방이 말한 소수 중 3번째로 큰 수만큼 점수 (3개 미만 -> 1000점)
        	//2. 이미 등장한 소수 -> 해당 팀 -1000, 기록x
        	if (prime[d]) { // 소수 아님
        		if (gList.size() < 3) {
        			gScore += 1000;
        		} else if (gList.size() >= 3) {
        			gScore += gList.get(0);
        		}
        	} else {
        		if (primeExist[d]) dScore -= 1000;
        		else {
        			dList.add(d);
        			primeExist[d] = true;
        			Collections.sort(dList);
        			if (dList.size() > 3) dList.remove(0);
        		}
        	}
        	if (prime[g]) {
        		if (dList.size() < 3) {
        			dScore += 1000;
        		} else if (dList.size() >= 3) {
        			dScore += dList.get(0);
        		}
        	} else {
        		if (primeExist[g]) gScore -= 1000;
        		else {
        			gList.add(g);
        			primeExist[g] = true;
        			Collections.sort(gList);
        			if (gList.size() > 3) gList.remove(0);
        		}
        	}
        }
        if (dScore > gScore) System.out.println("소수의 신 갓대웅");
        else if (dScore == gScore) System.out.println("우열을 가릴 수 없음");
        else System.out.println("소수 마스터 갓규성");
	}
	
	public static void primeNumber() { //소수 아닌게 true
		prime[0] = true;
		prime[1] = true;
		for (int i = 2; i*i <= 5000000; i++) {
			if (prime[i]) continue;
			for (int j = i*2; j <= 5000000; j+=i) {
				prime[j] = true;
			}
		}
	}
}

```
