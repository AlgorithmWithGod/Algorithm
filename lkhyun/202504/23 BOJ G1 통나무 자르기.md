```java
import java.io.*;
import java.util.*;

public class Main {

    static int L, K, C;
    static boolean[] visited;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        StringTokenizer st;

        st = new StringTokenizer(br.readLine());

        L = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());
        C = Integer.parseInt(st.nextToken());

        Set<Integer> removeDup = new TreeSet<>();
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < K; i++) {
            removeDup.add(Integer.parseInt(st.nextToken()));
        }

        int[] arr = new int[removeDup.size()];
        int i = 0;
        for (int a : removeDup) {
            arr[i++] = a;
        }

        int count = Math.min(removeDup.size(), C);
        // result[0] = 최대 길이, result[1] = 첫번째 위치, result[2] = 분할 수
        int[] result = search(0, L, arr, count);

        if (result[2] == count) {
            bw.write(result[0] + " " + result[1]);
        } else {
            for (int j = 0; j < arr.length; j++) {
                if (!visited[j]) {
                    if (arr[j] < result[1]) {
                        bw.write(result[0] + " " + arr[j]);
                    } else {
                        bw.write(result[0] + " " + result[1]);
                    }
                    break;
                }
            }
        }
        bw.close();
    }

    public static int[] search(int start, int end, int[] arr, int count) {
        int l = start;
        int r = end;
        int cnt = 0;
        int max = 0;
        int prev = end;
        while (l <= r) {
            int mid = (l + r) / 2; //mid를 넘어서면 분할함.
            prev = end;
            cnt = 0;
            max = 0;
            visited = new boolean[arr.length];
            for (int i = arr.length - 1; i >= 0; i--) {
                if ((prev - arr[i]) >= mid) {
                    if(i+1 <= arr.length - 1 && !visited[i+1]){ // 현 시점이 기준치를 넘어버린 상황이기에 그 이전을 자름.
                        visited[i+1] = true;
                        max = Math.max(max,prev-arr[i+1]);
                        prev = arr[i+1];
                        max = Math.max(max,prev-arr[i]);
                    }else { // 현시점이 첫 분할 지점이거나 혹은 이전 지점이 이미 분할된 곳이어서 더이상 나눌 수 없을 때
                        visited[i] = true;
                        max = Math.max(max, prev - arr[i]);
                        prev = arr[i];
                    }
                    cnt++;
                }
            }
            if ((prev - start) >= mid) { // 마지막 구간 처리
                if (arr[0] != prev) {
                    max = Math.max(max, prev - arr[0]);
                    visited[0] = true;
                    prev = arr[0];
                    cnt++;
                }
                max = Math.max(max, prev);
            }
            if(l == r) break;
            if (cnt > count) {
                l = mid + 1;
            } else {
                r = mid;
            }
        }
        return new int[] {max, prev, cnt};
    }

}

```
