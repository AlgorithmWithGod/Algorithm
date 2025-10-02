```java
import java.util.*;
class Solution {
    static Map<Integer,List<Integer>> adjList = new HashMap<>();
    static Map<Integer,Boolean> visited = new HashMap<>();
    static Set<Integer> startCandidate = new TreeSet<>();
    static Set<Integer> noStart = new TreeSet<>();
    static int[] answer = new int[4];
    
    public int[] solution(int[][] edges) {
        
        for(int[] edge : edges){
            List<Integer> temp;
            if(adjList.containsKey(edge[0])){
                startCandidate.add(edge[0]);
                temp = adjList.get(edge[0]);
            }else{
                temp = new ArrayList<>();
            }
            temp.add(edge[1]);
            adjList.put(edge[0],temp);
            visited.put(edge[0],false);
            visited.put(edge[1],false);
        }
        for(int[] edge : edges){
            if(startCandidate.contains(edge[1])){
                noStart.add(edge[1]);
            }
        }
        for(int start : startCandidate){
            if(!noStart.contains(start)){
                answer[0] = start;
                break;
            }
        }
        
        for(int start : adjList.get(answer[0])){
            BFS(start);
        }
        return answer;
    }
    public void BFS(int start){
        ArrayDeque<Integer> q = new ArrayDeque<>();
        q.offer(start);
        visited.put(start,true);
        
        while(!q.isEmpty()){
            int cur = q.poll();
            if(adjList.get(cur) == null){
                answer[2]++;
                return;
            }
            for(int next : adjList.get(cur)){
                if(adjList.get(next) == null){
                    answer[2]++;
                    return;
                }
                if(adjList.get(next).size() == 2){
                    answer[3]++;
                    return;
                }
                if(visited.get(next)){
                    answer[1]++;
                    return;
                }
                q.offer(next);
                visited.put(next,true);
            }
        }
    }
}
```
