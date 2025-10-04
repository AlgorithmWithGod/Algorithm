```java
import java.io.*;
import java.util.*;

class Solution {
    
    // 결국 자신으로 향하는 노드가 없는 경우는 딱 두가지임
    // 1. 막대 그래프에서의 시작점
    // 2. 추가된 간선
    // 하지만 둘간의 차이점 존재. 1번은 내가 가리키는 노드가 반드시 1개, 2번은 최소 2개 이상
    // 이를 통해서, 몇번을 추가했는지 찾은 후, 걔를 빼고 나머지 간선들로 계산하면됨
    // 이때 1번들을 기억해놓고, 얘네들이 곧 막대 모양 그래프 개수임
    // 나머지는 bfs 진행하면 된다. 
    // bfs 진행하면서 만약 내가 가리키고 있거나, 가리킴 당하는게 2개 이상이면 8자, 한번도 그런적 없으면 도넛.
    
    static final int TO = 1;
    static final int FROM = 0;
    static final int NEW_NODE = 0;
    
    static boolean[] visited = new boolean[1000_001];
    static int[] answer = new int[4];
    static Node[] nodes = new Node[1000_001];
    static ArrayList<Integer> stickStart =new ArrayList<>();
    
    static int newNode;
    
    static class Node{
        int num;
        int parentCnt = 0;
        List<Node> to = new ArrayList<>();
        public Node(int num){
            this.num = num;
        }
    }
    
    public int[] solution(int[][] edges) {
        findAndRemoveNewNode(edges);
        makeNode(edges);
        makeAns();
        return answer;
    }
    
    private void makeAns(){
        for (int i = 1; i <= 1000_000; i++){
            if (visited[i]) continue;
            if (nodes[i].parentCnt == 0) stickStart.add(i);
        }
        
        for (int t: stickStart){
            bfs(t,true);
        }
        
        for (int i = 1; i <= 1000_000; i++){
            if (visited[i]) continue;
            bfs(i,false);
        }
    }
    
    private void bfs(int target,boolean isStick){
        Node node = nodes[target];
        visited[target] = true;
        int maxToCnt = 0;
        
        Queue<Node> q = new LinkedList<>();
        q.add(node);
        
        while(!q.isEmpty()){
            Node n = q.poll();
            maxToCnt = Math.max(maxToCnt, n.to.size());
            for (Node t: n.to){
                if( visited[t.num]) continue;
                visited[t.num] = true;
                q.add(t);
            }
        }
        
        if (isStick){
            answer[2]++;
            return;
        }
        
        if (maxToCnt > 1) answer[3]++;
        else answer[1]++;
    }
    
    private void makeNode(int[][] edges){
        for (int i = 1; i <= 1000_000; i++){
            if (visited[i]) continue;
            nodes[i] = new Node(i);
        }
        
        
        for (int i = 0; i < edges.length; i++){
            int fromNum = edges[i][FROM];
            int toNum = edges[i][TO];
            
            if (fromNum == newNode || toNum == newNode) continue;
            
            nodes[fromNum].to.add(nodes[toNum]);
            nodes[toNum].parentCnt++;
        }
        
    }
    
    private void findAndRemoveNewNode(int[][] edges){
        int[][] arr = new int[2][1000_001];
        
        for (int i = 0; i < edges.length; i++){
            int fromNum = edges[i][FROM];
            int toNum = edges[i][TO];
            
            arr[TO][toNum]++;
            arr[FROM][fromNum]++;
        }
        
        for (int i = 0; i <= 1000_000; i++){
            if( arr[TO][i] == 0 && arr[FROM][i] == 0){
                visited[i] = true;
                continue;
            }
            
            if (arr[TO][i] == 0 ){
                if (arr[FROM][i] > 1){
                    answer[NEW_NODE] = i; 
                    newNode = i;
                    visited[i] = true;
                    continue;
                }

            }
            
            
        }
        
    }
}
```
