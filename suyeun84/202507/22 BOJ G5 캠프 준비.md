```java
import java.util.*;
import java.io.*;

public class boj16938 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    static int N, L, R, X;
    static int[] arr;
    static int tmp_cnt,tmp_min,tmp_answer;
    public static void main(String[] args) throws Exception {
        nextLine();
        N = nextInt();
        L = nextInt();
        R = nextInt();
        X = nextInt();
        arr = new int[N];
        nextLine();
        for (int i = 0; i < N; i++) arr[i] = nextInt();
        Arrays.sort(arr);

        int answer = 0;
        for(int i = 0; i < N-1; i++) {
            tmp_cnt = N-i;
            tmp_min = arr[i];
            tmp_answer = 0;
            comb(i+1,1,1,arr[i],arr[i]);
            answer += tmp_answer;
        }
        System.out.print(answer);
    }

    static void comb(int idx, int cnt,int add_cnt,int max,int tot) {
        if(cnt == tmp_cnt) {
            if(add_cnt > 1 && (max-tmp_min >= X) && (tot >= L && tot <= R)) tmp_answer++;
            return;
        }

        for(int i = idx; i < N; i++) {
            comb(i+1,cnt+1,add_cnt,max,tot);
            comb(i+1,cnt+1,add_cnt+1,arr[i],tot+arr[i]);
        }
    }
}
```
