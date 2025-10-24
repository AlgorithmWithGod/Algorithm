```java
import java.io.*;
import java.util.*;

public class boj1114 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    static int L, K, C;
    static int[] pos;
    static int ansLen, ansPos = -1, firstCut;
    public static void main(String[] args) throws Exception {
        nextLine();
        L = nextInt(); // 통나무 길이
        K = nextInt(); // 위치 개수
        C = nextInt(); // 자를 수 있는 최대 횟수
        // 통나무의 가장 긴 조각을 작게 만들고, 그 길이 구하기
        nextLine();
        pos = new int[K+2];
        pos[0] = 0;
        pos[K+1] = L;
        for (int i = 1; i <= K; i++) pos[i] = nextInt();
        Arrays.sort(pos);

        // 가장 긴 조각의 길이, 그 때 처음 자르는 위치
        int start = 1, end = L;
        ansLen = L;
        while (start <= end) {
            int mid = (start + end) / 2;
            int cnt = calc(mid);
            
            if (cnt <= C) {
            	ansLen = mid;
            	ansPos = firstCut;
            	end = mid - 1;
            } else {
            	start = mid + 1;
            }
        }
        System.out.println(ansLen + " " + ansPos);
    }

    static int calc(int mid) {
        int dist = 0, cnt = 0;
        for (int i = K; i >= 0; i--) {
            dist += pos[i+1] - pos[i];
            if (dist > mid) {
                dist = (pos[i+1] - pos[i]);
                cnt++;
                if (dist > mid) {
                    cnt = C+1;
                    break;
                }
            }
        }
        if (cnt < C) firstCut = pos[1];
        else firstCut = dist;
        
        return cnt;
    }
}
```
