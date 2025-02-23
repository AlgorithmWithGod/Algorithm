```java
import java.util.*;
import java.io.*;

public class solution {
    static final int MOD = 1000000007;

    public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        int T = Integer.parseInt(br.readLine());
        for(int t = 1;t<=T; t++){
            String str = br.readLine();
            int N = str.length();
            int[] respBits = new int[N];
            for (int i = 0; i < N; i++) {
                respBits[i] = charToInt(str.charAt(i));
            }
            List<Integer>[] daySubsets = new List[N];
            for(int i=0;i<N;i++){
                daySubsets[i] = new ArrayList<>();
                for(int mask=1;mask<16;mask++){
                    if((mask & respBits[i])==0) continue;
                    if(i==0 && (mask&1)==0) continue;
                    daySubsets[i].add(mask);
                }
            }
            long[] dpPrev = new long[16];
            long[] dpCur = new long[16];

            for(int mask : daySubsets[0]){
                dpPrev[mask] = 1;
            }
            for(int day=1; day<N;day++){
                Arrays.fill(dpCur,0);

                for(int curMask : daySubsets[day]){
                    long sum = 0;
                    for(int prevMask : daySubsets[day-1]){
                        if((curMask&prevMask)!=0){
                            sum += dpPrev[prevMask];
                        }
                    }
                    dpCur[curMask] = sum % MOD;
                }
                dpPrev = Arrays.copyOf(dpCur,16);
            }
            long answer = 0;
            for(int mask : daySubsets[N-1]){
                answer = (answer + dpPrev[mask]) % MOD;
            }
            bw.write("#"+t+" "+answer+"\n");
        }
        bw.flush();
    }
    public static int charToInt(char c){
        switch (c){
            case 'A' : return 1;
            case 'B' : return 2;
            case 'C' : return 4;
            case 'D' : return 8;
        }
        return 0;
    }
}

```
