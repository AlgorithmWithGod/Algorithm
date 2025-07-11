```java
import java.util.*;
import java.io.*;

public class Main{
    static class pos{
        int i,j;
        pos(int i,int j){
            this.i=i;
            this.j=j;
        }

        @Override
        public boolean equals(Object obj) {
            if(this == obj) return true;
            if(obj == null || getClass() != obj.getClass()) return false;
            pos other = (pos)obj;
            return i==other.i && j==other.j;
        }

        @Override
        public int hashCode() {
            return Objects.hash(i, j);
        }
    }
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,M;
    static pos[][] parent;
    public static void main(String[] args) throws Exception{
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        parent = new pos[N][M];
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                parent[i][j] = new pos(i,j);
            }
        }

        for (int i = 0; i < N; i++) {
            String line = br.readLine();
            for (int j = 0; j < M; j++) {
                char cmd = line.charAt(j);
                if(cmd == 'U' && i != 0){
                    merge(i,j,i-1,j);
                }else if(cmd == 'D' && i != N-1){
                    merge(i,j,i+1,j);
                }else if(cmd == 'L' && j != 0){
                    merge(i,j,i,j-1);
                }else if(cmd == 'R' && j != M-1){
                    merge(i,j,i,j+1);
                }
            }
        }
        Set<pos> s = new HashSet<>();
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                s.add(find(i,j));
            }
        }
        bw.write(s.size()+"");
        bw.close();
    }
    static pos find(int i,int j){
        if(parent[i][j] != null){
            if(parent[i][j].i == i && parent[i][j].j == j){
                return parent[i][j];
            }
            else{
                return parent[i][j] = find(parent[i][j].i,parent[i][j].j);
            }
        }
        return null;
    }
    static void merge(int i,int j,int k,int l){
        pos a = find(i,j);
        pos b = find(k,l);

        if(a != null && b != null){
            if(a.equals(b)){
                return;
            }else{
                parent[a.i][a.j] = b;
            }
        }
    }
}
```
