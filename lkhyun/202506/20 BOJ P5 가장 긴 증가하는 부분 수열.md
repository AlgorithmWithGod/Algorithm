```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static int[] arr;
    static List<Integer> LIS;
    static int[] lisLen;
    static int[] realIdx;

    public static void main(String[] args) throws IOException {
        N = Integer.parseInt(br.readLine());
        arr = new int[N+1];
        LIS = new ArrayList<>();
        lisLen = new int[N+1];
        realIdx = new int[N+1];

        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            int cur = Integer.parseInt(st.nextToken());
            arr[i] = cur;

            if(LIS.isEmpty() || LIS.get(LIS.size()-1) < cur){
                LIS.add(cur);
                lisLen[i] = LIS.size();//맨 뒤에 붙이는 경우는 LIS길이만큼 만들 수 있는거
                realIdx[LIS.size()-1] = i;
            } else {
                int pos = binarySearch(cur);
                LIS.set(pos, cur);
                lisLen[i] = pos + 1; //LIS는 0-base니까 1더해줌. 이진 탐색으로 찾은 위치까지 LIS를 만들 수 있다는 의미.
                realIdx[pos] = i;
            }
        }

        bw.write(LIS.size() + "\n");

        List<Integer> result = new ArrayList<>();
        int targetLength = LIS.size();

        for (int i = N; i >= 1; i--) {
            if (lisLen[i] == targetLength) {
                result.add(arr[i]);
                targetLength--;
            }
        }

        Collections.reverse(result);

        for (int i : result) {
            bw.write(i + " ");
        }
        bw.write("\n");

        bw.close();
    }

    public static int binarySearch(int target) {
        int left = 0; int right = LIS.size() - 1;

        while(left < right){
            int mid = (left + right) / 2;
            if(LIS.get(mid) < target){
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        return left;
    }
}
```
