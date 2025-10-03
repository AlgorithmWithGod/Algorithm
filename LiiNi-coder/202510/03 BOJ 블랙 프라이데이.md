```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int C = Integer.parseInt(st.nextToken());
        int[] arr = new int[N];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(arr);

        //1개 확인
        for(int i = 0; i < N; i++){
            if (arr[i] == C) {
                System.out.println(1);
                return;
            }
        }

        //2개 확인(투포인터 사용)
        int l = 0, r = N - 1;
        while(l < r){
            int sum = arr[l] + arr[r];
            if(sum == C){
                System.out.println(1);
                return;
            }
            if(sum < C)
                l++;
            else
                r--;
        }

        //3개 확인(중간값 정하고 나머지값 투포인터로 찾기)
        for(int i = 0; i < N; i++){
            int target = C - arr[i];
            int left = 0, right = N - 1;
            while(left < right){
                if(left == i){
                    left++;
                    continue;
                }
                if(right == i){
                    right--;
                    continue;
                }
                int sum = arr[left] + arr[right];
                if(sum == target){
                    System.out.println(1);
                    return;
                }
                if(sum < target)
                    left++;
                else
                    right--;
            }
        }

        System.out.println(0);
    }
}

```
