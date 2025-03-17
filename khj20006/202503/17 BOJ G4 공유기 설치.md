```java

import java.util.*;
import java.io.*;

public class Main {

	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st = new StringTokenizer("");
	
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() throws Exception {
		if(!st.hasMoreTokens()) nextLine();
		return Integer.parseInt(st.nextToken());
	}
	static long nextLong() throws Exception {
		if(!st.hasMoreTokens()) nextLine();
		return Long.parseLong(st.nextToken());
	}
	static void ioClose() throws Exception {bw.flush();bw.close();br.close();}
		
	/*
	 * [solving strategy]
	 * 주어진 문제를 살짝 변형하여, 다음과 같이 생각했습니다.
	 * "가장 인접한 가스 설치 지점 사이의 최대 거리가 m이 되도록 C개의 방역 가스를 설치할 수 있을까?"
	 * 위 문제는 '결정 문제'로, 단순 O(N)에 가능 여부를 판별할 수 있습니다.
	 * 또한, 어떤 m에 대해 가능했다면 m이하의 값들에 대해서도 항상 가능함이 보장됩니다.
	 * -> 유효한 m값의 범위를 매 step마다 반씩 줄일 수 있습니다.
	 * 이분 탐색으로 m의 최댓값을 찾아주었습니다.
	 * 
	 * [description]
	 * - N, C : 집, 방역 가스의 개수
	 * - X : 집의 위치 정보 저장
	 * 
	 * - ready() : input 처리 및 집 위치 X를 정렬
	 * - solve() : 이분 탐색으로 범위를 좁혀가며 해 도출하기
	 * - isPossible(m) : m이 유효한 값인지 가능 여부를 판별하여 boolean 형태로 반환
	 */
	
	static int N, C;
	static int[] X;
	
	public static void main(String[] args) throws Exception {
		//--------------솔루션 코드를 작성하세요.--------------------------------
		
		ready();
		solve();
		
		ioClose();
		
	}
	
	static void ready() throws Exception {
		
		N = nextInt();
		C = nextInt();
		X = new int[N];
		for(int i=0;i<N;i++) X[i] = nextInt();
		Arrays.sort(X);
		
	}
	
	static void solve() throws Exception {
		
		int s = 0, e = X[N-1] - X[0], m = (s+e+1)>>1;
		while(s<e) {
			if(isPossible(m)) s = m;
			else e = m-1;
			m = (s+e+1)>>1;
		}
		bw.write(m + "\n");
		
	}
	
	static boolean isPossible(int dist) {
		int cnt = 1, prev = X[0];
		for(int i=1;i<N;i++) {
			if(X[i]-prev >= dist) {
				cnt++;
				prev = X[i];
			}
		}
		return cnt >= C;
	}

}


```
