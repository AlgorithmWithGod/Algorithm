```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;


public class Main {

    static final int UPDATE = 1;
    static final int QUERY = 2;
    static int size, changeCnt, sumCnt,queryCnt;
    static long[] input;
    static StringBuilder sb = new StringBuilder();
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

    static class SegmentTree{
        private long[] lazy; //레이지 프로파게이션
        public long[] tree;
        private int size; // 원본 배열의 크기

        public SegmentTree(long[] arr){
            size = arr.length;
            this.lazy = new long[size*4];
            this.tree = new long[size*4];
            build(arr,1,0,size-1);
        }

        private void build(long[] arr, int node, int startIdx, int endIdx){
            if(startIdx == endIdx){
                tree[node] = arr[startIdx];
                return;
            }

            int mid = (startIdx + endIdx)/2;
            build(arr,node*2,startIdx,mid);
            build(arr,node*2+1,mid+1,endIdx);
            tree[node] = tree[node*2]^tree[node*2+1];
        }

        public void updateRange(int startIdx , int endIdx,  long k ){
            updateRange(1, 0, size-1, startIdx, endIdx, k);
        }

        private void updateRange(int node,int left,int right, int startIdx , int endIdx,  long k){
            updateLazy(node, left, right);

            if ( left > endIdx  || right < startIdx) return; //현 구간과 업데이트 구간이 아예 안겹칩

            if (left >= startIdx && right <= endIdx){ // 완전히 포함되는 경우
                // XOR의 특성: 구간 길이가 홀수일 때만 실제로 값이 변함
                int rangeLength = right - left + 1;
                if (rangeLength % 2 == 1) {
                    tree[node] ^= k;
                }

                // 리프 노드가 아니라면 lazy 전파
                if (left != right) {
                    lazy[2*node] ^= k;
                    lazy[2*node+1] ^= k;
                }
                return;
            }

            int mid = (left+right)/2;

            updateRange(node*2, left, mid, startIdx, endIdx, k);
            updateRange(node*2+1, mid+1, right, startIdx, endIdx, k);

            updateLazy(node*2, left, mid);
            updateLazy(node*2+1, mid+1,right);
            tree[node] = tree[node*2]^tree[node*2+1];
        }

        private void updateLazy(int node, int left, int right){
            if (lazy[node] == 0) return;

            long k = lazy[node];
            // XOR의 특성: 구간 길이가 홀수일 때만 실제로 값이 변함
            int rangeLength = right - left + 1;
            if (rangeLength % 2 == 1) {
                tree[node] ^= k;
            }

            if (left != right){
                lazy[node*2] ^= k;
                lazy[node*2+1] ^= k;
            }
            lazy[node] = 0;
        }

        public long query(int startIdx, int endIdx){
            return query(1,0, size-1, startIdx, endIdx);
        }

        private long query(int node , int left, int right, int startIdx , int endIdx){
            updateLazy(node, left, right);
            if ( left > endIdx  || right < startIdx) return 0;
            if (left >= startIdx && right <= endIdx) return tree[node];

            int mid = (left+right)/2;
            return query(node*2, left, mid, startIdx, endIdx)^query(node*2+1, mid+1, right, startIdx, endIdx);
        }
    }



    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        size = Integer.parseInt(br.readLine());
        input = new long[size];


        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < size; i++) {
            input[i] = Long.parseLong(st.nextToken());
        }

        queryCnt =  Integer.parseInt(br.readLine());

    }

    private static void process() throws IOException {

        SegmentTree tree = new SegmentTree(input);

        for (int i = 0; i < queryCnt; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int order = Integer.parseInt(st.nextToken());
            int start = Integer.parseInt(st.nextToken());
            int end = Integer.parseInt(st.nextToken());


            if (order == UPDATE) {
                long plus = Long.parseLong(st.nextToken());
                tree.updateRange(start, end, plus);
            } else sb.append(tree.query(start, end)).append("\n");


            int power = 2;
            for (int j = 1; j < tree.tree.length; j++) {
                if (j == power) {
                    System.out.println();
                    power *= 2;
                }
                System.out.print(tree.tree[j] +" ");
            }
            System.out.println();


            power = 2;
            for (int j = 1; j < tree.tree.length; j++) {
                if (j == power) {
                    System.out.println();
                    power *= 2;
                }
                System.out.print(tree.lazy[j] +" ");
            }
            System.out.println();
        }

    }


    private static void print() {
        System.out.println(sb.toString());

    }
}
```
