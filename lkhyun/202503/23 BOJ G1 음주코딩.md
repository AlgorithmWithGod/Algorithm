```java
import java.util.*;
import java.io.*;
public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N = 0;
    static int K = 0;
    static int[] arr;
    static int[] tree;
    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        while(st.hasMoreTokens()){
            N = Integer.parseInt(st.nextToken());
            K = Integer.parseInt(st.nextToken());
            arr = new int[N+1];
            tree = new int[4*N];

            st = new StringTokenizer(br.readLine());
            for(int i=1;i<=N;i++){
                arr[i] = Integer.parseInt(st.nextToken());
            }
            init(1,1,N);
            for(int i=1;i<=K;i++){
                st = new StringTokenizer(br.readLine());
                String cmd = st.nextToken();
                if(cmd.equals("C")){//변경
                    int idx = Integer.parseInt(st.nextToken());
                    int newValue = Integer.parseInt(st.nextToken());

                    if(newValue>0) update(1,1,N,idx,1);
                    else if(newValue<0) update(1,1,N,idx,-1);
                    else update(1,1,N,idx,0);

                }else if(cmd.equals("P")){//곱셈
                    int left = Integer.parseInt(st.nextToken());
                    int right = Integer.parseInt(st.nextToken());
                    int result = multiplication(1,1,N,left,right);
                    if(result>0) bw.write("+");
                    else if(result<0) bw.write("-");
                    else bw.write("0");
                }
            }
            bw.write("\n");

            String nextcmd = br.readLine();
            if(nextcmd == null) break;
            else st = new StringTokenizer(nextcmd);
        }
        bw.close();
    }
    public static void init(int cur, int start, int end){
        if(start==end){
            if(arr[start]>0) tree[cur] = 1;
            else if(arr[start]<0) tree[cur] = -1;
            else tree[cur] = 0;
        }else{
            init(cur*2,start,(start+end)/2);
            init(cur*2 + 1, (start+end)/2 + 1,end);
            tree[cur] = tree[cur*2] * tree[cur*2 + 1];
        }
    }
    public static void update(int cur, int start, int end, int idx, int newValue){
        if(idx<start || idx>end) return;
        if(start == end) {
            tree[cur] = newValue;
            return;
        }
        update(cur * 2, start, (start + end) / 2, idx, newValue);
        update(cur * 2 + 1, (start + end) / 2 + 1, end, idx, newValue);
        tree[cur] = tree[cur*2] * tree[cur*2 + 1];
    }
    public static int multiplication(int cur, int start, int end, int left, int right){
        if(right<start || left>end) return 1;
        if(left<=start && right>=end) return tree[cur];

        int l = multiplication(cur*2,start,(start+end)/2,left,right);
        int r = multiplication(cur*2 + 1, (start+end)/2 + 1,end,left,right);
        return l*r;
    }
}

```
