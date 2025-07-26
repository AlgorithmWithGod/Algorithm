```java
import java.awt.Point;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {

    static int depth,leafCnt;
    static int [] edges,maxSum,dp;


    static int ans;

    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        depth = Integer.parseInt(br.readLine());
        leafCnt = 1 << depth;
        ans = 0;
        edges = new int [leafCnt*2];
        maxSum = new int [leafCnt*2]; //maxSum: 자신부터 리프노드까지의 가중치 합 중 최댓값
        dp = new int[leafCnt*2]; // 1번노드부터 i번노드까지 왔을 때 가중치 합의 최대치

        //edge[i] -> i/2번 노드에서 i번 노드로 오는데 드는 가중치
        // 노드가 1번부터 시작하기에 엣지 0,1번은 없다.
        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 2; i < edges.length; i++) {
            edges[i] = Integer.parseInt(st.nextToken());
        }
    }

    private static void process() throws IOException {
        makeMaxSumArr(1);

        int totalMaxSum = maxSum[1];

        for (int i = 2; i < edges.length; i++) {
            int curSum =  dp[i/2] + edges[i];
            int goal = totalMaxSum - maxSum[i];

            edges[i] += goal - curSum;
            dp[i] = dp[i/2] + edges[i];
        }

        for (int i = 2; i < edges.length; i++) {
            ans += edges[i];
        }

    }

    private static int makeMaxSumArr(int nodeNum) {
        if (nodeNum *2 >= edges.length) return maxSum[nodeNum];// == 0
        int left = makeMaxSumArr(nodeNum*2) + edges[2*nodeNum];
        int right = makeMaxSumArr(2*nodeNum+1)  +edges[2*nodeNum+1];

        return maxSum[nodeNum] =  + Math.max(left, right);
    }


    private static void print() {
        System.out.println(ans);
    }
}


```