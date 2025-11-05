```java
import java.util.*;

class Solution {
    
    private static int maxNode;
    private static int[] answer;
    private static boolean[] isParent, isChild, visited;
    private static Queue<Integer> q;
    
    private static Map<Integer, List<Integer>> graph;
    
    private static void init(int[][] edges) {
        answer = new int[4];
        isParent = new boolean[1000001];
        isChild = new boolean[1000001];
        
        graph = new HashMap<>();
        
        maxNode = 0;
        for (int[] edge : edges) {
            List<Integer> tmp;
            
            maxNode = Math.max(maxNode, Math.max(edge[0], edge[1]));
            
            isParent[edge[0]] = true;
            isChild[edge[1]] = true;
            
            if (graph.get(edge[0]) == null) {
                tmp = new ArrayList<>();
            } else {
                tmp = graph.get(edge[0]);
            }
            
            tmp.add(edge[1]);
            graph.put(edge[0], tmp);
        }
        q = new ArrayDeque<>();
        visited = new boolean[maxNode + 1];
    }
    
    private static void findRoot() {
        for (int i = 0; i <= maxNode; i++) {
            if (isParent[i] && !isChild[i]) {
                List<Integer> children = graph.get(i);
                
                // 나가는 간선이 2개 이상
                if (children != null && children.size() >= 2) {
                    answer[0] = i;
                    break;
                }
            }
        }
    }
    
    private static void bfs(int start) {        
        q.offer(start);
        visited[start] = true;
        
        int nodeCnt = 0;
        int edgeCnt = 0;
        
        while (!q.isEmpty()) {
            int cur = q.poll();
            nodeCnt++;
            
            List<Integer> children = graph.get(cur);
            
            // |
            if (children == null) {
                answer[2]++;
                return;
            }
            
            edgeCnt += children.size();
            
            // 자식 정점이 2개 이상 - 8
            if (children.size() > 1) {
                answer[3]++;
                return;
            }
            
            for (int next : children) {
                if (visited[next]) {
                    // 간선 수 == 노드 수 - O
                    // 간선 수 > 노드 수 - 8자
                    if (edgeCnt == nodeCnt) {
                        answer[1]++;
                    } else {
                        answer[3]++;
                    }
                    return;
                }
                
                visited[next] = true;
                q.offer(next);
            }
        }
    }
    
    public int[] solution(int[][] edges) {
        init(edges);        
        findRoot();
        
        for (int n : graph.get(answer[0])) {
            Arrays.fill(visited, false);
            bfs(n);
            q.clear();
        }
        
        return answer;
    }
}
```