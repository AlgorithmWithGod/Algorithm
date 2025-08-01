```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N, M, R, K;
    static Map<String, Integer> cityMap = new HashMap<>();
    static List<String> will;
    static double[][] normalCost;
    static double[][] naeilroCost;
    static final int INF = Integer.MAX_VALUE;
  
    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        R = Integer.parseInt(st.nextToken());
        
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            cityMap.put(st.nextToken(), i);    
        }

        M = Integer.parseInt(br.readLine());
        will = new ArrayList<>();
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < M; i++) {
            will.add(st.nextToken());
        }

        normalCost = new double[N][N];
        naeilroCost = new double[N][N];
        
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (i == j) {
                    normalCost[i][j] = 0;
                    naeilroCost[i][j] = 0;
                } else {
                    normalCost[i][j] = INF;
                    naeilroCost[i][j] = INF;
                }
            }
        }

        K = Integer.parseInt(br.readLine());
        for (int i = 0; i < K; i++) {
            st = new StringTokenizer(br.readLine());
            String type = st.nextToken();
            String from = st.nextToken();
            String to = st.nextToken();
            int cost = Integer.parseInt(st.nextToken());
            
            int fromIdx = cityMap.get(from);
            int toIdx = cityMap.get(to);
            
            normalCost[fromIdx][toIdx] = Math.min(normalCost[fromIdx][toIdx], cost);
            normalCost[toIdx][fromIdx] = Math.min(normalCost[toIdx][fromIdx], cost);
            
            double naeilroPrice = getNaeilroPrice(type, cost);
            naeilroCost[fromIdx][toIdx] = Math.min(naeilroCost[fromIdx][toIdx], naeilroPrice);
            naeilroCost[toIdx][fromIdx] = Math.min(naeilroCost[toIdx][fromIdx], naeilroPrice);
        }

        floyd(normalCost);
        floyd(naeilroCost);

        double totalNormalCost = 0;
        double totalNaeilroCost = 0;
        
        for (int i = 0; i < M - 1; i++) {
            int from = cityMap.get(will.get(i));
            int to = cityMap.get(will.get(i + 1));
            
            totalNormalCost += normalCost[from][to];
            totalNaeilroCost += naeilroCost[from][to];
        }
       
        totalNaeilroCost += R;
        
        if (totalNaeilroCost < totalNormalCost) {
            System.out.println("Yes");
        } else {
            System.out.println("No");
        }
    }
    
    static double getNaeilroPrice(String type, double cost) {
        if(type.equals("S-Train") || type.equals("V-Train")){
            return cost/2;
        }else if(type.equals("Mugunghwa") ||  type.equals("ITX-Cheongchun") || type.equals("ITX-Saemaeul")){
            return 0;
        }else{
            return cost;
        }
    }
    
    static void floyd(double[][] dist) {
        for (int k = 0; k < N; k++) {
            for (int i = 0; i < N; i++) {
                for (int j = 0; j < N; j++) {
                    if (dist[i][k] != INF && dist[k][j] != INF) {
                        dist[i][j] = Math.min(dist[i][j], dist[i][k] + dist[k][j]);
                    }
                }
            }
        }
    }
}
```
