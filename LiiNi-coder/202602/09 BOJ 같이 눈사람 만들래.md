```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class Main {
	/*
		눈사람 : 머리 <= 몸통
		눈사람의 키 == 두 눈덩이의 지름 합
		N개중 서로 다른 4개 골라서 눈사람 2개
		두 눈사람의 키차이 최소가 되도록
		N <= 600

 	*/
	private static int[] Snows;
	private static class Snowman implements Comparable<Snowman> {
		int idx1;
		int idx2;
		int sum;

		public Snowman(int idx1, int idx2, int sum) {
			this.idx1 = idx1;
			this.idx2 = idx2;
			this.sum = sum;
		}

		@Override
		public int compareTo(Snowman o) {
			return this.sum - o.sum;
		}
	}

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int n = Integer.parseInt(br.readLine());

		Snows = new int[n];
		String[] tokens = br.readLine().split(" ");
		for (int i = 0; i < n; i++) {
			Snows[i] = Integer.parseInt(tokens[i]);
		}

		// 모든 가능한 두 눈덩이 쌍 생성 및 합
		List<Snowman> snowmen = new ArrayList<>();
		for (int i = 0; i < n; i++) {
			for (int j = i + 1; j < n; j++) {
				snowmen.add(new Snowman(i, j, Snows[i] + Snows[j]));
			}
		}
		// 합 기준으로 정렬
		Collections.sort(snowmen);
		int answer = Integer.MAX_VALUE;
		//정렬된 합들을 기준으로 최소 차이 찾기
		//(0, 1), (0, 2)... 0행 에서 찾다가 만약 더 최소값을 찾고나면 바로 다음1행으로 가면된다. 어차피 정렬되어있으니까.
		for(int i = 0; i < snowmen.size(); i++){
			Snowman s1 = snowmen.get(i);
			for(int j = i + 1; j < snowmen.size(); j++){
				Snowman s2 = snowmen.get(j);
				int diff = s2.sum - s1.sum;
				if (diff >= answer) {
					break;//애초에 다음행
				}
				if (isOverlap(s1, s2)) {
					continue;
				}
				answer = diff;
				break;// 바로 다음행
			}
		}
		System.out.println(answer);
		br.close();
	}

	private static boolean isOverlap(Snowman s1, Snowman s2) {
		//네 개의 인덱스 중 어느 하나라도 겹치면 true
		return s1.idx1 == s2.idx1 || s1.idx1 == s2.idx2 ||
			s1.idx2 == s2.idx1 || s1.idx2 == s2.idx2;
	}
}

```
