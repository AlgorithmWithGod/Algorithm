```java
import java.io.*;
import java.util.*;

public class Main {

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        StringBuilder sb = new StringBuilder();

        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());
        int k = Integer.parseInt(st.nextToken());

        long[] arr = new long[n];
        long[] tree = new long[4*n];

        for(int i=0;i<n;i++){
            arr[i] = Long.parseLong(br.readLine());
        }

        init(arr,tree,1,0,n-1);

        for(int i=0;i<m+k;i++){
            st = new StringTokenizer(br.readLine());
            int op = Integer.parseInt(st.nextToken());

            if(op==1){
                int a = Integer.parseInt(st.nextToken());
                long b = Long.parseLong(st.nextToken());
                update(arr, tree, 1, 0, n-1, a-1,b);
            }
            else{
                int a = Integer.parseInt(st.nextToken());
                int b = Integer.parseInt(st.nextToken());

                long sum = query(tree,1,0,n-1,a-1,b-1);

                sb.append(sum+"\n");
            }
        }

        System.out.println(sb.toString());
    }

    static void init(long[] arr, long[] tree, int node, int start, int end){
        if(start == end){
            tree[node]=arr[start];
        }
        else{
            init(arr,tree,node*2,start,(start+end)/2);
            init(arr,tree,node*2+1,(start+end)/2+1,end);
            tree[node]=tree[node*2]+tree[node*2+1];
        }
    }

    static long query(long[] tree, int node, int start, int end, int left, int right) {
        if (left > end || right < start) {
            return 0;
        }
        if (left <= start && end <= right) {
            return tree[node];
        }
        long lsum = query(tree, node*2, start, (start+end)/2, left, right);
        long rsum = query(tree, node*2+1, (start+end)/2+1, end, left, right);
        return lsum+rsum;
    }

    static void update(long[] arr, long[] tree, int node, int start, int end, int index, long val) {
        if (index < start || index > end) {
            return;
        }
        if (start == end) {
            arr[index] = val;
            tree[node] = val;
            return;
        }
        update(arr, tree,node*2, start, (start+end)/2, index, val);
        update(arr, tree,node*2+1, (start+end)/2+1, end, index, val);
        tree[node] = tree[node*2] + tree[node*2+1];
    }
}

```
