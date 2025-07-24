```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static int cnt = 0;
    static StringBuilder sb = new StringBuilder();
    public static void main(String[] args) throws Exception {
        int N = Integer.parseInt(br.readLine());
        hanoi(N, 1, 2, 3);
        bw.write(cnt+"\n");
        bw.write(sb.toString());
        bw.close();
    }
    static void hanoi(int n, int from, int temp, int to) throws Exception{
        if(n == 0) return;

        hanoi(n-1,from, to, temp); //from에서 to로 잠깐 옮겨놓음 맨 아래 빼고
        sb.append(from).append(" ").append(to).append("\n"); //그럼 이제 from에서 원래 가고 싶은 to로 보낼 수 있으니 출력
        cnt++;
        hanoi(n-1,temp,from, to); //그 담에 잠깐 올려뒀던 위에 있는거 다시 to로 올려놔야하니까
    }
}
```
