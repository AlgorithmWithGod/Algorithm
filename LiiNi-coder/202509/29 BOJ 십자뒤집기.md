```java
import java.io.*;
import java.util.*;
import java.util.stream.IntStream;

public class Main {
    private static int N = 3;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());
        while(T-- > 0){
            var map = 0;
            for(int r = 0; r < N; r++) {
                char[] cs = br.readLine().toCharArray();
                for (int c = 0; c < N; c++) {
                    if (cs[c] == '*')
                        map += 1<<(N*r + c);
                }
            }
            System.out.println(solve(map));
        }
        br.close();
    }

    private static int solve(int initialMap) {
        boolean[] visited = new boolean[512];
        Deque<int[]> q = new ArrayDeque<>();
        q.add(new int[]{initialMap, 0});
        visited[initialMap] = true;
        while(!q.isEmpty()){
            int[] temp = q.poll();
            int map = temp[0], count = temp[1];
            if(map == 0){
                return count;
            }
            for(int di: IntStream.range(0, 9).toArray()){
                int nextMap = toggle(map, di);
                if(visited[nextMap]) continue;
                visited[nextMap] = true;
                q.add(new int[]{nextMap, count+1});
            }
        }
        return -1;
    }

    private static int toggle(int map, int black1d) {
        List<Integer> masks = new ArrayList<>();
        masks.add(black1d);
        if(black1d % N == 0){
            masks.add(black1d + 1);
        }else if(black1d % N == 1){
            masks.add(black1d + 1);
            masks.add(black1d-1);
        }else{
            masks.add(black1d-1);
        }

        if(black1d / N == 0){
            masks.add(black1d + N);
        }else if(black1d / N == 1){
            masks.add(black1d - N);
            masks.add(black1d + N);
        }else{
            masks.add(black1d-N);
        }

        for(int mask: masks){
            map ^= 1<<mask;
        }
        return map;
    }
}

```
