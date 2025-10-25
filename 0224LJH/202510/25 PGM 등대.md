```java
import java.io.*;
import java.util.*;

class Solution {
    static int nodeCnt, answer;
    static Node[] nodes;
    
    static class Node{
        int num;
        boolean isOn = false;
        Node parent = null;
        HashSet<Node> to = new HashSet<>();
        
        public Node(int num){
            this.num = num;
        }
    }
    
    public int solution(int n, int[][] lighthouse) {
        nodeCnt = n;
        answer = 0;
        init(lighthouse);
        
        makeTree(1);
        turnLight(1);
        for (int i = 1; i<= nodeCnt; i++){
            if (nodes[i].isOn)answer++;
        }
        answer = Math.min(answer, nodeCnt - answer);
        
        return answer;
    }
    
    private void turnLight(int nodeNum){
        Node node = nodes[nodeNum];
        if (node.to.size() == 0){
            node.isOn = false;
            return;
        }
        
        boolean result = true;
        for (Node child: node.to){
            turnLight(child.num);
            result &= child.isOn;
        }
        node.isOn = !result;
    }
    
    private void makeTree(int nodeNum){
        Node node = nodes[nodeNum];
        for (Node child: node.to){
            child.parent = node;
            child.to.remove(node);
            makeTree(child.num);
        }
        
    }
    
    private void init(int[][] lighthouse){
        
        nodes = new Node[nodeCnt+1];
        for (int i = 0; i <= nodeCnt; i++){
            nodes[i] = new Node(i);
        }
        
        for (int i = 0; i< nodeCnt-1; i++){
            int n1 = lighthouse[i][0];
            int n2 = lighthouse[i][1];
            
            Node node1 = nodes[n1];
            Node node2 = nodes[n2];
            node1.to.add(node2);
            node2.to.add(node1);
            
        }
    }
}
```
