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
        int[] arr = new int[n];
        for(int i=0;i<n;i++){
            arr[i]= Integer.parseInt(br.readLine());
        }

        int[] min_tree = new int[4*n];
        int[] max_tree = new int[4*n];

        init(arr,min_tree,1,0,n-1);
        initmax(arr,max_tree,1,0,n-1);

        for(int i=0;i<m;i++){
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());

            int min = query(min_tree,1,0,n-1,a-1,b-1);
            int max = querymax(max_tree,1,0,n-1,a-1,b-1);
            sb.append(min+" "+max+"\n");
        }

        System.out.println(sb.toString());
    }

    static void init(int[] arr, int[] tree, int node, int start, int end) {
        if (start == end) {
            tree[node] = arr[start];
        } else {
            init(arr, tree, node * 2, start, (start + end) / 2);
            init(arr, tree, node * 2 + 1, (start + end) / 2 + 1, end);
            tree[node] = Math.min(tree[node * 2], tree[node * 2 + 1]);
        }
    }

    static int query(int[] tree, int node, int start, int end, int left, int right) {
        if (left > end || right < start) {
            return -1;
        }
        if (left <= start && end <= right) {
            return tree[node];
        }
        int lmin = query(tree, node*2, start, (start+end)/2, left, right);
        int rmin = query(tree, node*2+1, (start+end)/2+1, end, left, right);
        if (lmin == -1) {
            return rmin;
        } else if (rmin == -1) {
            return lmin;
        } else {
            return Math.min(lmin, rmin);
        }
    }

    static void initmax(int[] arr, int[] tree, int node, int start, int end) {
        if (start == end) {
            tree[node] = arr[start];
        } else {
            initmax(arr, tree, node * 2, start, (start + end) / 2);
            initmax(arr, tree, node * 2 + 1, (start + end) / 2 + 1, end);
            tree[node] = Math.max(tree[node * 2], tree[node * 2 + 1]);
        }
    }

    static int querymax(int[] tree, int node, int start, int end, int left, int right) {
        if (left > end || right < start) {
            return -1;
        }
        if (left <= start && end <= right) {
            return tree[node];
        }
        int lmax = querymax(tree, node*2, start, (start+end)/2, left, right);
        int rmax = querymax(tree, node*2+1, (start+end)/2+1, end, left, right);
        if (lmax == -1) {
            return rmax;
        } else if (rmax == -1) {
            return lmax;
        } else {
            return Math.max(lmax, rmax);
        }
    }
}

```
