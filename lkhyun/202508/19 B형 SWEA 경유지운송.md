```java
import java.util.*;
class UserSolution {
    static class state implements Comparable<state>{
        int to,w;
        state(int to, int w){
            this.to = to;
            this.w = w;
        }

        @Override
        public int compareTo(state other){
            return Integer.compare(other.w,this.w);
        }
    }
    static List<state>[] adjLists;

    public int[] dijkstra(int start){
        PriorityQueue<state> pq = new PriorityQueue<>();
        int[] dist = new int[1000];
        for (int i = 0; i < dist.length; i++) {
            dist[i] = -1;
        }
        for (state cur : adjLists[start]) {
            pq.offer(new state(cur.to,cur.w));
            dist[cur.to] = cur.w;
        }

        while(!pq.isEmpty()){
            state cur = pq.poll();
            
            if(dist[cur.to] > cur.w) continue;

            for (state next : adjLists[cur.to]) {
                int newDist = Math.min(cur.w,next.w);
                if(newDist > dist[next.to]){
                    dist[next.to] = newDist;
                    pq.offer(new state(next.to,newDist));
                }
            }
        }
        return dist;
    }

	public void init(int N, int K, int sCity[], int eCity[], int mLimit[]) {
        adjLists = new ArrayList[N];
        for (int i = 0; i < N; i++) {
            adjLists[i] = new ArrayList<>();
        }
        for (int i = 0; i < K; i++) {
            adjLists[sCity[i]].add(new state(eCity[i],mLimit[i]));
            adjLists[eCity[i]].add(new state(sCity[i],mLimit[i]));
        }
		return;
	}

	public void add(int sCity, int eCity, int mLimit) {
        adjLists[sCity].add(new state(eCity,mLimit));
        adjLists[eCity].add(new state(sCity,mLimit));
		return;
	}

	public int calculate(int sCity, int eCity, int M, int mStopover[]) {
        int[] fromStart = dijkstra(sCity);
        int ans = fromStart[eCity];
        for (int i = 0; i < M; i++) {
            if(fromStart[mStopover[i]] == -1){
                return -1;
            }
            ans = Math.min(ans, fromStart[mStopover[i]]);
        }
		return ans;
	}
}
```
