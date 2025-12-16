```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        int M = Integer.parseInt(st.nextToken());
        int N = Integer.parseInt(st.nextToken());
        
        List<List<Integer>> spaces = new ArrayList<>();
        
        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            List<Integer> space = new ArrayList<>();
            Set<Integer> set = new HashSet<>();
            
            for (int j = 0; j < N; j++) {
                int planet = Integer.parseInt(st.nextToken());
                set.add(planet);
                space.add(planet);
            }
            
            List<Integer> sorted = new ArrayList<>(set);
            Collections.sort(sorted);
            
            for (int j = 0; j < N; j++) {
                int idx = Collections.binarySearch(sorted, space.get(j));
                space.set(j, idx);
            }
            spaces.add(space);
        }
        
        int answer = 0;
        for (int i = 0; i < M; i++) {
            for (int j = i + 1; j < M; j++) {
                if (spaces.get(i).equals(spaces.get(j))) answer++;
            }
        }
        
        System.out.println(answer);
    }
}
```
