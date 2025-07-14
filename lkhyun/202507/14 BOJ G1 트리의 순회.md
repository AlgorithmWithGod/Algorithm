```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static int[] inOrder;
    static int[] postOrder;
    static int[] findInOrderIdxByValue;

    static int[] preOrder;
    static int preOrderIdx = 1;

    public static void main(String[] args) throws Exception{
        N = Integer.parseInt(br.readLine());
        inOrder = new int[N+1];
        postOrder = new int[N+1];
        findInOrderIdxByValue = new int[N+1];
        preOrder = new int[N+1];

        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            inOrder[i] = Integer.parseInt(st.nextToken());
            findInOrderIdxByValue[inOrder[i]] = i;
        }
        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            postOrder[i] = Integer.parseInt(st.nextToken());
        }
        search(1,N,1,N);
        for (int i = 1; i <= N; i++) {
            bw.write(preOrder[i]+" ");
        }
        bw.close();
    }
    static void search(int InStart, int InEnd, int PostStart, int PostEnd){
        if(PostStart > PostEnd) return;
        int rootIdx = findInOrderIdxByValue[postOrder[PostEnd]];
        preOrder[preOrderIdx++] = postOrder[PostEnd];
        int leftSize = rootIdx - InStart;
        int rightSize = InEnd - rootIdx;

        search(InStart, rootIdx-1,PostStart,PostStart+leftSize-1);
        search(rootIdx+1, InEnd, PostEnd-rightSize, PostEnd-1);
    }
}
```
