```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,M;
    static int[] A,B;


    public static void main(String[] args) throws IOException {
        N = Integer.parseInt(br.readLine());
        A = new int[N];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            A[i] = Integer.parseInt(st.nextToken());
        }

        M = Integer.parseInt(br.readLine());
        B = new int[M];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < M; i++) {
            B[i] = Integer.parseInt(st.nextToken());
        }

        List<Integer> common = new ArrayList<>();
        int[] temp = searchMax(-1,-1);
        while(temp[0] != -1) {
            common.add(A[temp[0]]);
            temp = searchMax(temp[0], temp[1]);
        }
        if(common.size() == 0){
            bw.write("0");
        }else{
            bw.write(common.size()+"\n");
            for(int i:common){
                bw.write(i+" ");
            }
        }
        bw.close();
    }
    public static int[] searchMax(int endA, int endB){
        int maxAIndex = -1 ,maxBIndex = -1;
        for (int i = N-1; i > endA; i--) {
            for (int j = M-1; j > endB; j--) {
                if (A[i] == B[j]){ //공통으로 가지는 경우
                    if(maxAIndex == -1 || A[maxAIndex] <= A[i]){
                        maxAIndex = i;
                        maxBIndex = j;
                    }else{
                        break;
                    }
                }
            }
        }
        return new int[]{maxAIndex,maxBIndex};
    }
}


```
