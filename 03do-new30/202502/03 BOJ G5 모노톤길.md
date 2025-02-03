```java
import java.util.*;
import java.io.*;

public class Main {
	
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
		
		int T = Integer.parseInt(br.readLine());
		for (int tc = 1; tc <= T; tc++) {
			int n = Integer.parseInt(br.readLine());

            // TreeMap: 자동정렬(오름차순)을 보장하며, 키 기반 탐색 성능 logN
			Map<Integer, List<Integer>> map = new TreeMap<>();
			map.put(-1, new ArrayList<>(Arrays.asList(0)));
			StringTokenizer st;
			for (int i = 0; i < n; i++) {
				st = new StringTokenizer(br.readLine());
				int x = Integer.parseInt(st.nextToken());
				int y = Integer.parseInt(st.nextToken());
				
				if (map.containsKey(x)) {
					map.get(x).add(y);
				} else {
					List<Integer> val = new ArrayList<>();
					val.add(y);
					map.put(x, val);
				}
			}

			int[] keys = map.keySet().stream().mapToInt(x -> x).toArray();
			for (int i = 0; i < keys.length; i++) {
				int key = keys[i];
				
				if (key == -1) continue;
				
				if (map.get(key).size() == 1) {
					continue;
				}
				
				// 이전 x좌표의 마지막 y좌표와 비교해서
				// 같은 x좌표를 가진 좌표들 중 가장 먼저 도달하는 y좌표를 구한다.
				int prevKey = keys[i-1];
				int lastIndex = map.get(prevKey).size() - 1;
				int firstY = map.get(prevKey).get(lastIndex);
				
				// 현재 x좌표의 y좌표들 중 가장 값이 큰 y좌표를 찾는다
				int maxY = Collections.max(map.get(key));
				
				// firstY가 maxY라면 내림차순 정렬
				// firstY가 maxY가 아니라면 오름차순 정렬
				if (firstY == maxY) {
					Collections.sort(map.get(key), Collections.reverseOrder());
				}
				else {
					Collections.sort(map.get(key));
				}
			}
			List<String> points = new ArrayList<>(n);
			for (int x : keys) {
				List<Integer> values = map.get(x);
				for (int y : values) {
					points.add(x + " " + y);
				}
			}
			
			int[] tmp = Arrays.stream(br.readLine().split(" "))
							.mapToInt(x -> Integer.parseInt(x))
							.toArray();
			int total = tmp[0];
			for (int i = 1; i <= total; i++) {
				bw.write(points.get(tmp[i]) + "\n");
			}
		}
		
		br.close();
		bw.flush();
		bw.close();
	}
}
```
- `TreeMap` 사용