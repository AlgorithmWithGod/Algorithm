```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.Deque;
import java.util.HashSet;
import java.util.List;
import java.util.StringTokenizer;

public class Main{
	/*
	* 물고기 m마리, 아기상어
	* 아기상어 처음 크기 2
	* 1초에 상하좌우 한칸 이동 / 동시에 먹음 / 그칸은 빈칸이 됨 / 아기상어 크기만큼 물고기 먹으면 크기가 증가
	* 자신보다 큰 물고가칸 못감 / 나머진 가능
	* 자신보다 작은 물고기는 먹을수있음
	* 아기상어 이동 루틴
	*   1. 더이상 먹을수있는 물고기가 없다면 끝
	*   2. 먹을수있는 물고기 == 1 : 거기로 감
	*   3. 먹을수있는 물고기 > 1: 가장 가까운 물고기
	*   3-1. 만약 가장 가까운 물고기가 많다면 가장위 -> 그것도 많다면 가장 왼쪽
	* */

	/* 1. 아기상어 이동목표 선정 : O(N)
			1. 바로 해당 아기상어보다 같거나 작은 애들의 좌표를 알수있어야함
			2. 그중 가장 가까운 것을 바로 찾을수있어야함(절댓값구하면됨)
			3. 2번을 쌓아놓고 그중에서 가장 위, 왼쪽을 찾아야함
	 * 아기상어의 크기는 도중에 바뀜 -> 1.1 변동됨
	 */
	static int N;
	static int Size = 2;
	static int[] Coords = new int[2];
	static List<List<int[]>> FishAtSize;
	static int[][] Drdcs = {
		{0, 1},
		{1, 0},
		{0, -1},
		{-1, 0}
	};
	static int[][] Map;
	public static void main(String[] args)throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		/*
		0은 빈칸
		1, 2, 3, 4, 5, 6은 칸에 있는 물고기 크기
		9는 아기상어 위치
		 */
		N = Integer.parseInt(br.readLine());
		FishAtSize = new ArrayList<>();
		for(int i = 0; i < 7; i++){
			FishAtSize.add(new ArrayList<>());
		}
		Map = new int[N][N];
		for(int r = 0; r<N; r++){
			StringTokenizer st = new StringTokenizer(br.readLine());
			for(int c = 0; c<N; c++){
				int value = Integer.parseInt(st.nextToken());
				if(value == 0) continue;
				else if(value == 9) {
					Coords[0] = r;
					Coords[1] = c;
				}else if(value >= 1 && value <= 6){
					FishAtSize.get(value).add(new int[]{r, c});
					Map[r][c] = value;
				}
			}
		}

		int t = 0;
		int countEating = Size;
		HashSet<Integer> blackList = new HashSet<>();
		while(true) {
			List<int[]> q1 = new ArrayList<>();
			List<int[]> q2 = new ArrayList<>();



			// // 2. 큐1중에서 가장 가까운 애들 큐2에 넣음
			// int i = 0;
			// int[] dists = new int[q1.size()];
			// int minDist = Integer.MAX_VALUE;
			// for (int[] fishCoord : q1) {
			// 	// 2-1.q1에서 i번째마다 거리를 모두 구함
			// 	dists[i] = Math.abs(fishCoord[0] - Coords[0]) + Math.abs(fishCoord[1] - Coords[1]);
			// 	minDist = Math.min(minDist, dists[i]);
			// 	i++;
			// }
			// //2-1. 굳이정렬? 그냥 가장 최솟값을 가지는 애들을 q2에 넣음
			// i = 0;
			// for (int[] fishCoord : q1) {
			// 	if (dists[i] == minDist)
			// 		q2.add(fishCoord);
			// 	i++;
			// }

			// 2. fish1DSet을 발견할때 bfs로 하여서 가장 작은 값을 구하고
			Deque<int[]> qbfs = new ArrayDeque<>();
			qbfs.add(new int[]{Coords[0], Coords[1], 0});
			int minDist = Integer.MAX_VALUE;
			boolean validMinDist = false;
			boolean[][] visited = new boolean[N][N];
			visited[Coords[0]][Coords[1]] = true;
			while(!qbfs.isEmpty()){
				int[] qItem = qbfs.poll();
				int r = qItem[0]; int c = qItem[1]; int step = qItem[2];
				if(validMinDist && minDist <= step)
					continue;
				for(int[] drdc: Drdcs){
					int nr = r + drdc[0];
					int nc = c + drdc[1];
					if(nr < 0 || nr >= N || nc < 0 || nc >= N) continue;
					if(visited[nr][nc]) continue;
					if(Map[nr][nc] > Size) continue;
					// 자신보다 작은 것들만 먹을수있으
					if(Map[nr][nc] < Size && Map[nr][nc] >= 1){
						if(blackList.contains(N*nr + nc)) continue;
						if(!validMinDist){
							validMinDist = true;
							minDist = step+1;
						}
						q2.add(new int[]{nr, nc});
					}
					qbfs.add(new int[]{nr, nc, step+1});
					visited[nr][nc] = true;
				}
			}


			// printArr(q2);

			// 3. 큐2중에서 가장 위 -> 가장 왼쪽애를 targetCoords에 넣음
			// 이쯤되면 그냥 정렬해도되지않을까(채에 2번 걸렀으니)
			Collections.sort(q2, (o1, o2) -> {
				if (o1[0] == o2[0]) {
					return o1[1] - o2[1];
				}
				return o1[0] - o2[0];
			});
			int[] targetCoord = q2.isEmpty()? null: q2.get(0);
			if (targetCoord == null) {
				break;
			}

			//System.out.println("targetCoord : (%d, %d)".formatted(targetCoord[0], targetCoord[1]));

			//Coords 이동
			Coords[0] = targetCoord[0];
			Coords[1] = targetCoord[1];
			// 시간 더하기
			t += minDist;
			// 아기상어 크기 처리
			countEating--;
			if(countEating <= 0 ){
				Size++;
				countEating = Size;
			}
			// 해당 칸에 속한 물고기 삭제
			blackList.add(N*targetCoord[0] + targetCoord[1]);
			Map[targetCoord[0]][targetCoord[1]] = 0;
			//System.out.println("Coord: " + Arrays.toString(Coords));
			// System.out.println("t, size : " + t + ", " + Size);
		}
		System.out.println(t);
		br.close();
	}

	static void printArr(List<int[]> arrs){
		StringBuilder sb = new StringBuilder();
		for(int[] arr: arrs)
			sb.append("(").append(arr[0]).append(", ").append(arr[1]).append("\n");
		System.out.println(sb.toString());
	}
}
```
