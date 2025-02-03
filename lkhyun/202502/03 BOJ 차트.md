import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.*;
public class Main {
    static BufferedReader br;
    static BufferedWriter bw;
    static int N;
    static int[] comb;
    static boolean[] visited;
    static int[] dogs;
    static int max = 0;
    public static void main(String[] args) throws Exception {
        br = new BufferedReader(new InputStreamReader(System.in));
        bw = new BufferedWriter(new OutputStreamWriter(System.out));
        N = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());

        dogs = new int[N];
        comb = new int[N];
        visited = new boolean[N];
        for(int i=0;i<N;i++){
            dogs[i] = Integer.parseInt(st.nextToken());
        }
        combination(0);
        bw.write(max + "");
        bw.flush();
    }

    public static void combination(int depth){
        if(depth == N){
            int count = 0;
            for(int j=0;j<N-1;j++){
                int sum = comb[j];
                for(int k=j+1;k<N;k++){
                    if(sum == 50){count++; break;}
                    else if(sum > 50){break;}
                    sum += comb[k];
                }
            }
            if(max<count){max = count;}
            return;
        }

        for(int i=0;i<N;i++){
            if(visited[i]){continue;}
            visited[i] = true;
            comb[depth] = dogs[i];
            combination(depth+1);
            visited[i] = false;
        }
    }
}
