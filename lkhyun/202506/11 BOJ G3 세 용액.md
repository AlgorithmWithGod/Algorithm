```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static int[] arr;
    static int[] selected = new int[3];
    static long min = Long.MAX_VALUE;
    public static void main(String[] args) throws IOException {

        N = Integer.parseInt(br.readLine());
        arr = new int[N];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
        Arrays.sort(arr);

        boolean[] visited = new boolean[N];
        a:for (int i = 0; i < N; i++) { //모든 값들 중 하나 선택
            long base = arr[i];
            visited[i] = true;
            int left,right;

            //base가 아닌 값들중 좌 우 맨 끝 값을 선택
            if(i==0){
                left = 1;
                right = N-1;
            }else if(i==N-1){
                left = 0;
                right = N-2;
            }else{
                left = 0;
                right = N-1;
            }

            while(left<right){
                long sum = arr[left] + arr[right] + base;
                if(sum < 0){
                    if(Math.abs(sum) < min){
                        min = Math.abs(sum);
                        selected[0] = arr[left];
                        selected[1] = arr[right];
                        selected[2] = (int)base;
                    }
                    if(visited[left+1]){
                        left += 2;
                    }else{
                        left++;
                    }
                }else if(sum > 0){
                    if(Math.abs(sum) < min){
                        min = Math.abs(sum);
                        selected[0] = arr[left];
                        selected[1] = arr[right];
                        selected[2] = (int)base;
                    }
                    if(visited[right-1]){
                        right -= 2;
                    }else{
                        right--;
                    }
                }else{
                    selected[0] = arr[left];
                    selected[1] = arr[right];
                    selected[2] = (int)base;
                    break a;
                }
            }
            visited[i] = false;
        }
        Arrays.sort(selected);
        for (int i = 0; i < 3; i++) {
            bw.write(selected[i] + " ");
        }
        bw.close();
    }
}
```
