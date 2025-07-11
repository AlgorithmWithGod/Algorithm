```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static List<int[]> flowers;
    static int[] current = {3,1};
    static int[] maxCoverage = new int[2];
    static int cnt = 0;
    static boolean isCover;

    public static void main(String[] args) throws Exception{
        N = Integer.parseInt(br.readLine());
        flowers = new ArrayList<>();

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int startMonth = Integer.parseInt(st.nextToken());
            int startDay = Integer.parseInt(st.nextToken());
            int endMonth = Integer.parseInt(st.nextToken());
            int endDay = Integer.parseInt(st.nextToken());
            flowers.add(new int[]{startMonth, startDay, endMonth, endDay});
        }

        flowers.sort((a,b) -> {
            if(a[0] == b[0]){
                if(a[1] == b[1]){
                    if(a[2] == b[2]){
                        return Integer.compare(a[3], b[3]);
                    }else{
                        return Integer.compare(a[2], b[2]);
                    }
                }else{
                    return Integer.compare(a[1], b[1]);
                }
            }else{
                return Integer.compare(a[0], b[0]);
            }
        });

        for (int[] flower : flowers) {
            if(flower[0]<current[0] || (flower[0] == current[0] && flower[1]<=current[1])){
                if(maxCoverage[0] < flower[2]){
                    maxCoverage[0] = flower[2];
                    maxCoverage[1] = flower[3];
                }else if(maxCoverage[0] == flower[2] && maxCoverage[1] < flower[3]){
                    maxCoverage[1] = flower[3];
                }
            }else if(flower[2] > maxCoverage[0] || (flower[2] == maxCoverage[0] && flower[3] > maxCoverage[1])){
                current[0] = maxCoverage[0];
                current[1] = maxCoverage[1];
                cnt++;
                if(flower[0]<current[0] || (flower[0] == current[0] && flower[1]<=current[1])){
                    if(maxCoverage[0] < flower[2]){
                        maxCoverage[0] = flower[2];
                        maxCoverage[1] = flower[3];
                    }else if(maxCoverage[0] == flower[2] && maxCoverage[1] < flower[3]){
                        maxCoverage[1] = flower[3];
                    }
                }
            }
            if(maxCoverage[0]>11 || (maxCoverage[0] == 11 && maxCoverage[1]>30)){
                cnt++;
                isCover = true;
                break;
            }
        }
        if(isCover){
            bw.write(cnt+"");
        }else{
            bw.write("0");
        }
        bw.close();
    }
}
```
