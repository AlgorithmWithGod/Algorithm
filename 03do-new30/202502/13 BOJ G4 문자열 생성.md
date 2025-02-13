```java
import java.io.*;

public class Main {

    static int N;
    static char[] arr;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        N = Integer.parseInt(br.readLine());
        arr = new char[N];
        for (int i = 0; i < N; i++) {
            arr[i] = br.readLine().charAt(0);
        }

        char[] result = new char[N];
        int headIdx = 0; // arr 앞쪽 포인터
        int tailIdx = N-1; // arr 뒤쪽 포인터
        int idx = 0; // result의 인덱스
        
        while (headIdx <= tailIdx) {

            if (idx == N) { break; }

            if (arr[headIdx] < arr[tailIdx]) {
                result[idx++] = arr[headIdx++];
            }
            else if (arr[headIdx] > arr[tailIdx]) {
                result[idx++] = arr[tailIdx--];
            }
            else {

                boolean isHeadSmaller = true;

                for (int offset = 1; offset < N; offset++) {
                    if (headIdx + offset >= N || tailIdx - offset < 0) {
                        break;
                    }
                    if (headIdx + offset > tailIdx - offset) {
                        break;
                    }

                    if (arr[headIdx + offset] < arr[tailIdx - offset]) {
                        break;
                    } else if (arr[headIdx + offset] > arr[tailIdx - offset]) {
                        isHeadSmaller = false;
                        break;
                    }
                }

                if (isHeadSmaller) {
                    result[idx++] = arr[headIdx++];
                } else {
                    result[idx++] = arr[tailIdx--];
                }
            }
        }


        // 80글자마다 새줄 문자를 출력한다.
        for (int i = 0; i < N; i++) {
            bw.write(result[i]);
            if ((i+1) % 80 == 0) {
                bw.write("\n");
            }
        }

        br.close();
        bw.flush();
        bw.close();
    }

}

```
