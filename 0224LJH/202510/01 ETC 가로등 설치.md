```java
import java.io.*;
import java.util.*;

public class Main {

    static class Node{
        int point;
        Node left;
        Node right;
        boolean isAlive = true;

        public Node (int point){
            this.point = point;
        }
    }

    static class Edge implements Comparable<Edge>{
        Node left;
        Node right;
        int distance;


        public Edge(Node left, Node right){
            this.left = left;
            this.right = right;
            distance = right.point - left.point;

            left.right = right;
            right.left = left;
        }

        public boolean isAlive(){
            if (left.isAlive && right.isAlive
            && left.right == right
            && right.left == left) return true;
            return false;
        }

        @Override
        public int compareTo(Edge e){
            if (e.distance == this.distance) {
                return Integer.compare(this.left.point , e.left.point);
            }
            return Integer.compare(e.distance, this.distance);
        }
    }

    static final int INIT = 100;
    static final int ADD = 200;
    static final int DELETE = 300;
    static final int CALCULATE = 400; 

    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringBuilder sb = new StringBuilder();

    static int totalStreet,nodeCnt, orderCnt, aliveCnt, min,max;
    static List<Node> nodes = new ArrayList<>();
    static PriorityQueue<Edge> pq = new PriorityQueue<>();
     


    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }


    private static void init() throws IOException {
        orderCnt = Integer.parseInt(br.readLine());
        
        StringTokenizer st = new StringTokenizer(br.readLine());

        st.nextToken(); // 100
        
        totalStreet = Integer.parseInt(st.nextToken());
        nodeCnt = Integer.parseInt(st.nextToken());
        aliveCnt = nodeCnt;
        min = totalStreet;
        max = 0;

        Node dummy = new Node(-1);
        nodes.add(dummy);
        for (int i = 1; i<= nodeCnt; i++){
            int point = Integer.parseInt(st.nextToken());
            min = Math.min(min, point);
            max = Math.max(max, point);
            Node n = new Node(point);
            nodes.add(n);
        }

        for (int i = 1; i < nodeCnt; i++){
            Node left = nodes.get(i);
            Node right = nodes.get(i+1);
            Edge e = new Edge(left,right);
            pq.add(e);
        }

    }

    private static void process() throws IOException {
        for (int i = 1 ; i < orderCnt; i++){
            StringTokenizer st = new StringTokenizer(br.readLine());
            int order = Integer.parseInt(st.nextToken());

            if (order == ADD){
                add();
            } else if (order == DELETE){
                int target = Integer.parseInt(st.nextToken());
                delete(target);
            } else if (order == CALCULATE){
                calculate();
            }
        }

    }

    private static void add(){
        aliveCnt++;

        Edge e = pq.poll();

        while(!e.isAlive()){
            e = pq.poll();
        }

        int nPoint = e.left.point + (e.distance + 1)/2;
        Node n = new Node(nPoint);
        nodes.add(n);
        Edge e1 = new Edge(e.left, n);
        Edge e2 = new Edge(n, e.right);
        
        pq.add(e1);
        pq.add(e2);
    }

    private static void delete(int target){
        aliveCnt--;
        Node t = nodes.get(target);
        t.isAlive = false;

        if (t.left == null){
            // 이 노드가 가장 왼쪽(시작지점)에 있는 경우
            min = t.right.point;
            t.right.left = null;
        } else if (t.right == null){
            // 이 노드가 가장 오른쪽(끝)에 있는 경우
            max = t.left.point; 
            t.left.right = null;
        } else{
            Edge e = new Edge(t.left, t.right);
            pq.add(e);
        }

    }




    private static void calculate(){
        Edge e = pq.peek();

        while (!e.isAlive()){
            pq.poll();
            e = pq.peek();
        }

        int cost = e.distance;

        cost = Math.max( cost,(min-1)*2);
        cost = Math.max( cost,(totalStreet - max)*2);

        sb.append(cost).append("\n");

    }

    private static void print(){
        System.out.println(sb.toString());
    }
}

```
