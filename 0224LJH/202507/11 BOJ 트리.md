```java
//1시간 30분
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {

    static final int PAINT = 1;
    static final int MOVE = 2;
    static final int COUNT = 3;

    static StringBuilder sb = new StringBuilder();
    static Node[] nodes;
    static int nodeCnt, operCnt;
    static int[][] opers;

    static class Node{
        Node parent = null;
        int num;
        int color = 0; // 자신의 부모로 가는 길의 색상

        public Node(int num){
            this.num = num;
        }

        public void moveTo(Node nParent){
            parent = nParent;
        }
    }


    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        nodeCnt = Integer.parseInt(st.nextToken());
        operCnt = Integer.parseInt(st.nextToken());

        nodes = new Node[nodeCnt];
        opers = new int[operCnt][4];

        nodes[0] = new Node(0);
        for (int i = 1; i < nodeCnt; i++) {
            nodes[i] = new Node(i);
            nodes[i].moveTo(nodes[0]);
        }

        for (int i = 0; i < operCnt; i++) {
            st = new StringTokenizer(br.readLine());
            int idx = 0;
            while(st.hasMoreTokens()){
                opers[i][idx++] = Integer.parseInt(st.nextToken());
            }
        }
    }

    private static void process() {
        for (int i = 0; i < operCnt; i++) {
            int[] oper = opers[i];

            switch (oper[0]) {
                case PAINT: paintWholePath(oper[1], oper[2], oper[3]); break;
                case MOVE: move(oper[1], oper[2]); break;
                case COUNT: getColorCntOfPath(oper[1], oper[2]); break;
            }

        }

    }

    private static Node findFirstCommonParent(Node node1, Node node2){
        Node curNode1 = node1;
        Node curNode2 = node2;

        if (node1 == node2) {return node1;}


        HashSet<Node> set = new HashSet<>();
        set.add(curNode1);
        set.add(curNode2);
        while(true){
            if (curNode1.parent != null) {
                curNode1 = curNode1.parent;
                if (set.contains(curNode1)) {
                    return curNode1;
                }
                set.add(curNode1);
            }

            if (curNode2.parent != null) {
                curNode2 = curNode2.parent;
                if (set.contains(curNode2)) {
                    return curNode2;
                }
                set.add(curNode2);
            }
        }
    }

    private static void paintWholePath(int num1, int num2, int color){
        Node node1 = nodes[num1];
        Node node2 = nodes[num2];
        Node parent = findFirstCommonParent(node1, node2);

        while (node1 != parent){
            node1.color = color;
            node1 = node1.parent;
        }
        while (node2 != parent){
            node2.color = color;
            node2 = node2.parent;
        }

    }
    private static void getColorCntOfPath(int num1, int num2){
        Node node1 = nodes[num1];
        Node node2 = nodes[num2];
        Node parent = findFirstCommonParent(node1, node2);

        HashSet<Integer> set = new HashSet<>();
        while (node1 != null && node1 != parent ){
            //노드1부터 상위 노드로 가는 엣지의 색상 추가.
            set.add(node1.color);
            node1 = node1.parent;
        }
        while (node2 != null && node2 != parent){
            set.add(node2.color);
            node2 = node2.parent;
        }

        sb.append(set.size()).append("\n");
    }

    private static void move(int targetN, int nParentNum){
        Node target = nodes[targetN];
        Node nParent = nodes[nParentNum];
        target.moveTo(nParent);
    }



    private static void print() {
        System.out.print(sb.toString());
    }
}
```