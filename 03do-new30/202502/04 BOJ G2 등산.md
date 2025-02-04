```java
import java.io.*;
import java.util.*;

public class Main {
	
	private static class Node implements Comparable<Node>{
		int r;
		int c;
		int weight;
		public Node(int r, int c, int weight) {
			this.r = r;
			this.c = c;
			this.weight = weight;
		}
		
		public String toString() {
			return "(" + r + ", " + c + ", time:" + weight + ")";
		}

		@Override
		public int compareTo(Node o) {
			return Integer.compare(this.weight, o.weight);
		}
	}
	
	private static int N;
	private static int M;
	private static int T;
	private static int D;
	private static int[][] arr;
	private static int[] dr = {0, 0, -1, 1};
	private static int[] dc = {-1, 1, 0, 0};
	private static final int INF = Integer.MAX_VALUE;
	private static List<List<Node>> graph;
	
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
		
		StringTokenizer st = new StringTokenizer(br.readLine());
		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());
		T = Integer.parseInt(st.nextToken());
		D = Integer.parseInt(st.nextToken());
		
		arr = new int[N][M];
		for (int i = 0; i < N; i++) {
			char[] tmpChar = br.readLine().toCharArray();
			for (int j = 0; j < M; j++) {
				if (Character.isLowerCase(tmpChar[j])) {
					arr[i][j] = tmpChar[j] - 'a' + 26;
				} else {
					arr[i][j] = tmpChar[j] - 'A';
				}
			}
		}
		
		// 인접리스트 생성
		graph = new ArrayList<>();
		for (int i = 0; i < N * M; i++) {
			graph.add(new ArrayList<>());
		}
		for (int r = 0; r < N; r++) {
			for (int c = 0; c < M; c++) {
				
				int index = r * M + c;
				
				for (int i = 0; i < 4; i++) {
					int nr = r + dr[i];
					int nc = c + dc[i];
					if (nr < 0 || nr >= N || nc < 0 || nc >= M) {
						continue;
					}
					
					// 높이의 차이가 T보다 크지 않은 곳으로만 다닐 수 있다.
					if (Math.abs(arr[nr][nc] - arr[r][c]) > T) {
						continue;
					}
					
					int time;
					if (arr[r][c] >= arr[nr][nc]) {
						time = 1;
					} else {
						time = (int)Math.pow(arr[nr][nc] - arr[r][c], 2);
					}
					
					graph.get(index).add(new Node(nr, nc, time));
				}
				
			}
		}
		
		// 시작점 0에서 각 점까지의 최단거리
		int[] dist = dijkstra(new Node(0, 0, 0));
		
		// 시작점에서 최단경로가 존재하는 정점 중, 제한 시간 내에 다시 시작점으로 돌아올 수 있는 경우
		int highest = arr[0][0];
		for (int mountain = 1; mountain < N*M; mountain++) {
			if (dist[mountain] != INF) {
				int mountC = mountain % M;
				int mountR = mountain / M;
				
				if (highest >= arr[mountR][mountC]) continue;
				
				int[] backDist = dijkstra(new Node(mountR, mountC, 0));
				if (dist[mountain] + backDist[0] <= D) {
					highest = arr[mountR][mountC];
				}
			}
		}
		
		bw.write(highest + "\n");
		
		br.close();
		bw.flush();
		bw.close();
	}
	
	private static int[] dijkstra(Node start) {
		int[] dist = new int[N * M];
		Arrays.fill(dist, INF);
		
		int startIdx = start.r * M + start.c;
		dist[startIdx]= 0;
		
		PriorityQueue<Node> pq = new PriorityQueue<>();
		pq.offer(start);
		
		while (!pq.isEmpty()) {
			Node node = pq.poll();
			int nodeIdx = node.r * M + node.c;
			
			List<Node> nextNodes = graph.get(nodeIdx);
			for (Node nextNode : nextNodes) {
				int nextIdx = nextNode.r * M + nextNode.c;
				int nextDist = dist[nodeIdx] + nextNode.weight;
				if (nextDist < dist[nextIdx]) {
					dist[nextIdx] = nextDist;
					pq.offer(new Node(nextNode.r, nextNode.c, nextDist));
				}
			}
		}
		
		return dist;
	}
}
```
- 주어진 입력을 인접 리스트 형태의 그래프로 변환
- 시작점에서 dijkstra로 최단경로를 구한 뒤, 각 정점에서 시작점으로 제한시간 내에 돌아올 수 있는지 한번 더 체크
- 유의사항
    - 시작점의 높이가 가장 높은 경우도 있을 수 있음
    - `highest`를 0으로 초기화하는 것이 아니라 시작점의 높이로 초기화
- 테스트케이스
    ```
    3 3 51 1000
    zAA
    AAA
    AAA
    ```