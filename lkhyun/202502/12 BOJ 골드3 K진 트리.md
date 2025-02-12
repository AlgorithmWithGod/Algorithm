```java
import java.util.*;
import java.io.*;
public class Main{
    public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        StringTokenizer st = new StringTokenizer(br.readLine());
        long N = Long.parseLong(st.nextToken());
        long K = Integer.parseInt(st.nextToken());
        long Q = Integer.parseInt(st.nextToken());

        for(int i=0;i<Q;i++){
            st = new StringTokenizer(br.readLine());
            long x = Long.parseLong(st.nextToken());
            long y = Long.parseLong(st.nextToken());
            long start = Math.min(x,y); //start를 작은걸로
            long end = Math.max(x,y);   //end를 큰걸로 고정
            if(K == 1){
                bw.write((end-start)+"\n");
                continue;
            }
            long startdepth = findDepth(start,K);
            long enddepth = findDepth(end,K);
            long depthDiff = enddepth - startdepth;
            long dist = 0;
            for(int j=0;j<depthDiff;j++){
                end = findParent(end, K);
                dist++;
            }
            while(start!=end){
                start = findParent(start, K);
                end = findParent(end, K);
                dist+=2;
            }
            bw.write(dist+"\n");
        }
        bw.flush();
    }
    public static long findDepth(long x,long K){
        long finder = 1;
        long depth = 1;
        while(x > finder){
            finder *= K;
            finder += 1;
            depth++;
        }
        return depth;
    }
    public static long findParent(long x,long K){
        if(x%K==0 || x%K==1){
            return x/K;
        }else{
            return x/K + 1;
        }
    }
}
```
