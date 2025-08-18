```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.HashSet;
import java.util.LinkedList;
import java.util.List;
import java.util.Queue;
import java.util.StringTokenizer;


public class Main {
    static int nodeCnt;
    static Node[] nodes;
    static Queue<Edge> q =  new LinkedList<>();
    static HashSet<Node> visited = new HashSet<>();

    static class Node{
        int idx;
        int num;

        List<Node> list = new ArrayList<>();

        public Node(int idx){
            this.idx = idx;
        }

        public void propagate(int weight){
            visited.add(this);
            num *=  weight;

            for (Node node : list){
                if (visited.contains(node)) continue;
                node.propagate(weight);
            }
        }
    }

    static class Edge{
        int from;
        int to;
        int fromWeight;
        int toWeight;

        public Edge(int from, int to, int fromWeight, int toWeight){
            this.from = from;
            this.to = to;
            this.fromWeight = fromWeight;
            this.toWeight = toWeight;
        }
    }




    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        nodeCnt = Integer.parseInt(br.readLine());
        nodes = new Node[nodeCnt];

        for (int i = 0 ; i < nodeCnt -1; i++){
            StringTokenizer st = new StringTokenizer(br.readLine());

            int from = Integer.parseInt(st.nextToken());
            int to = Integer.parseInt(st.nextToken());
            int fromWeight = Integer.parseInt(st.nextToken());
            int toWeight = Integer.parseInt(st.nextToken());

            q.add(new Edge(from,to,fromWeight,toWeight));

        }


    }

    private static void process() throws IOException {
        firstSetting();
        makeNums();

        int gcd = euclid();

        for (int i = 0; i < nodeCnt; i++){
            nodes[i].num /= gcd;
        }



        for (int i = 0 ; i< nodeCnt ; i++){
            System.out.print(nodes[i].num + " ");
        }


    }

    private static int euclid() {
        int gcd = nodes[0].num;
        int large,small;

        for (int i = 1; i < nodeCnt; i++){


            int target = nodes[i].num;

            if (gcd < target) {
                large = target;
                small = gcd;
            } else if (gcd > target) {
                large = gcd;
                small = target;
            } else continue;

            while(true){
                int remainder = large%small;
                if (remainder == 0){
                    gcd = small;
                    break;
                }

                large = small;
                small = remainder;
            }
        }

        return gcd;
    }

    private static void makeNums() {
        while(!q.isEmpty()){
            Edge e = q.poll();

            if (nodes[e.from] == null &&  nodes[e.to] == null) {
                q.offer(e);
                continue;
            }

            visited = new HashSet<>();

            if (nodes[e.from] == null) {

                nodes[e.from] = new Node(e.from);
                nodes[e.from].num = e.fromWeight * nodes[e.to].num;
                nodes[e.from].list.add(nodes[e.to]);
                nodes[e.to].list.add(nodes[e.from]);

                visited.add(nodes[e.from]);
                nodes[e.to].propagate(e.toWeight);

            } else{
                nodes[e.to] = new Node(e.to);
                nodes[e.to].num = e.toWeight * nodes[e.from].num;
                nodes[e.to].list.add(nodes[e.from]);
                nodes[e.from].list.add(nodes[e.to]);

                visited.add(nodes[e.to]);

                nodes[e.from].propagate(e.fromWeight);
            }
        }
    }

    private static void firstSetting() {
        Edge first = q.poll();

        nodes[first.from] = new Node(first.from);
        nodes[first.from].num = first.fromWeight;

        nodes[first.to] = new Node(first.to);
        nodes[first.to].num = first.toWeight;

        nodes[first.from].list.add(nodes[first.to]);
        nodes[first.to].list.add(nodes[first.from]);

    }


    private static void print() {

    }
}
```