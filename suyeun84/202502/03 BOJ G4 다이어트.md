```java
import java.util.*;
import java.io.*;

class boj19942
{
	static int N;
	static Ingredient[] list;
	static ArrayList<ArrayList<Integer>> combinations;
	
	public static void main(String[] args) throws Exception{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		int[] target = new int[4];
		int answer = Integer.MAX_VALUE;
		List<String> answer2 = new ArrayList<>();
		N = Integer.parseInt(st.nextToken());
		st = new StringTokenizer(br.readLine());
		for (int i = 0; i < 4; i++) {
			target[i] = Integer.parseInt(st.nextToken());
		}
		
		list = new Ingredient[N];
		for (int i = 0; i < N; i++) {
			st = new StringTokenizer(br.readLine());
			list[i] = new Ingredient(i, Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken()));
		}
		
		//combinations
		for (int i = 1; i <= N; i++) {
			//식재료 선택 갯수
			combinations = new ArrayList<>();
			dfs(new ArrayList<Integer>(), i, 0);
			for (List<Integer> ingredient : combinations) {
				int mp = 0;
				int mf = 0;
				int ms = 0;
				int mv = 0;
				int mc = 0;
				ArrayList<Integer> temp2 = new ArrayList<>();
				for (int idx : ingredient) {
					mp += list[idx].p;
					mf += list[idx].f;
					ms += list[idx].s;
					mv += list[idx].v;
					mc += list[idx].c;
					temp2.add(list[idx].idx+1);
				}
				if (mp >= target[0] && mf >= target[1] && ms >= target[2] && mv >= target[3]) {
					if (answer > mc) {
						answer = mc;
						answer2.clear();
						Collections.sort(temp2);
						String sb = "";
						for (int t : temp2) {
							sb = sb + t + " ";
						}
						answer2.add(sb);
					} else if (answer == mc) {
						Collections.sort(temp2);
						String sb = "";
						for (int t : temp2) {
							sb = sb + t + " ";
						}
						answer2.add(sb);
					}
				}
			}
			combinations.clear();
		}
		if (answer != Integer.MAX_VALUE) {
			System.out.println(answer);
			Collections.sort(answer2);
			System.out.println(answer2.get(0));
		} else {
			System.out.println(-1);
		}
	}
	
	static void dfs(ArrayList<Integer> curr, int i, int idx) {
		if (curr.size() == i) {
			combinations.add(curr);
			return;
		}
		for (int k = idx; k < N; k++) {
			ArrayList<Integer> newList = new ArrayList<>();
			for (int c : curr) {
				newList.add(c);
			}
			newList.add(list[k].idx);
			dfs(newList, i, k+1);
		}
	}
	
	static class Ingredient {
		int idx, p, f, s, v, c;
		
		public Ingredient(int idx, int p, int f, int s, int v, int c) {
			this.idx = idx;
			this.p = p;
			this.f = f;
			this.s = s;
			this.v = v;
			this.c = c;
		}
	}
}

```
