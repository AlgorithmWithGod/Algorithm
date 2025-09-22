```java
import java.io.*;
import java.util.*;

public class Main {
    static class Node{
        int key,difficulty;

        Node(int key, int difficulty){
            this.key = key;
            this.difficulty = difficulty;
        }
    }

    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,M;
    static Map<Integer,Integer> problems = new HashMap<>();
    static TreeSet<Node> s = new TreeSet<>((a,b) -> {
        if(a.difficulty == b.difficulty){
            return Integer.compare(a.key,b.key);
        }else{
            return Integer.compare(a.difficulty,b.difficulty);
        }
    });
    
    public static void main(String[] args) throws IOException {
        N = Integer.parseInt(br.readLine());
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int p = Integer.parseInt(st.nextToken());
            int l = Integer.parseInt(st.nextToken());
            problems.put(p,l);
            s.add(new Node(p,l));
        }
        
        M = Integer.parseInt(br.readLine());
        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            String cmd = st.nextToken();
            
            if(cmd.equals("add")){
                int p = Integer.parseInt(st.nextToken());
                int l = Integer.parseInt(st.nextToken());
                problems.put(p,l);
                s.add(new Node(p,l));
            }
            else if(cmd.equals("recommend")){
                int x = Integer.parseInt(st.nextToken());
                if(x == 1){
                    Node hard = s.last();
                    bw.write(hard.key + "\n");
                }
                else{
                    Node easy = s.first();
                    bw.write(easy.key + "\n");
                }
            }
            else if(cmd.equals("solved")){
                int p = Integer.parseInt(st.nextToken());
                int difficulty = problems.get(p);
                problems.remove(p);
                s.remove(new Node(p, difficulty));
            }
        }
        
        bw.close();
    }
}
```
