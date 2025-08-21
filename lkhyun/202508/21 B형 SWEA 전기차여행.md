```java
import java.util.*;
class UserSolution {
    static class Edge implements Comparable<Edge>{
        int from;
        int to;
        int id;
        int time;
        int power;
        
        Edge(int from, int to, int id, int time, int power){
            this.from = from;
            this.to = to;
            this.id = id;
            this.time = time;
            this.power = power;
        }

        @Override
        public int compareTo(Edge other){
            return this.time - other.time;
        }
    }
    static class State implements Comparable<State>{
        // to로 오는데 걸린 시간과 남은 차량의 충전 용량
        int to;
        int time;
        int power;

        State(int to, int time, int power){
            this.to = to;
            this.time = time;
            this.power = power;
        }
        
        @Override
        public int compareTo(State other){
            if(this.time == other.time){
                return other.power - this.power;
            }else{
                return this.time - other.time;
            }
        }
    }
    static List<Edge>[] adjList;
    static int[] chargeOfCity;
    static Map<Integer,Edge> edgeById;
    
	public void init(int N, int mCharge[], int K, int mId[], int sCity[], int eCity[], int mTime[], int mPower[]) {
        adjList = new ArrayList[N];
        chargeOfCity = new int[N];
        edgeById = new HashMap<>();

        for (int i = 0; i < N; i++) {
            adjList[i] = new ArrayList<>();
            chargeOfCity[i] = mCharge[i];
        }

        for (int i = 0; i < K; i++) {
            Edge e = new Edge(sCity[i], eCity[i], mId[i], mTime[i], mPower[i]);
            adjList[sCity[i]].add(e);
            edgeById.put(mId[i],e);
        }
		return;
	}

	public void add(int mId, int sCity, int eCity, int mTime, int mPower) {
        Edge e = new Edge(sCity, eCity, mId, mTime, mPower);
        adjList[sCity].add(e);
        edgeById.put(mId,e);
		return;
	}

	public void remove(int mId) {
        Edge e = edgeById.get(mId);
        adjList[e.from].remove(e);
        edgeById.remove(mId);
		return;
	}
    
    public int[][] dijkstraForCar(int start, int end, int B, int[] corona){
        int[][] dist = new int[adjList.length][B+1]; //여기로 오는데 B만큼 충전량이 남음.
        PriorityQueue<State> pq = new PriorityQueue<>();
        for (int i = 0; i < dist.length; i++) {
            for (int j = 0; j <= B; j++) {
                dist[i][j] = Integer.MAX_VALUE;
            }
        }
        State init = new State(start, 0, B);
        dist[start][B] = 0;
        pq.offer(init);

        while(!pq.isEmpty()){
            State cur = pq.poll();

            if(dist[cur.to][cur.power] < cur.time) continue;
            if(cur.to == end) return dist;

            for(Edge e : adjList[cur.to]){
                if(e.power > B) continue;
                int tempPower = cur.power;
                int tempTime = cur.time;
                while(tempPower < e.power){ //도착지로 가기위한 전기가 충분치 않아서 충전
                    tempPower = Math.min(B,tempPower + chargeOfCity[cur.to]);
                    tempTime++;
                }
                //딱 최소 용량만 충전하고 갔을때, 전염병 만나는지 혹은 기존의 최적 루트보다 최적인지 판단.
                if(corona[e.to] <= (tempTime + e.time) || dist[e.to][tempPower - e.power] <= (tempTime + e.time)) continue;
                pq.offer(new State(e.to, tempTime + e.time, tempPower - e.power));
                dist[e.to][tempPower - e.power] = tempTime + e.time;
                
                while(tempPower != B){ //여기서 충전을 충분히 해두는게 이득일 수 있음
                    tempPower = Math.min(B,tempPower + chargeOfCity[cur.to]);
                    tempTime++;
                    if(corona[e.to] <= (tempTime + e.time) || dist[e.to][tempPower - e.power] <= (tempTime + e.time)){
                        continue;
                    }
                    pq.offer(new State(e.to, tempTime + e.time, tempPower - e.power));
                    dist[e.to][tempPower - e.power] = tempTime + e.time;
                }
            }
        }
        return dist;
    }
    public int[] dijkstraForCorona(int start, int startTime){
        int[] dist = new int[adjList.length];
        PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> a[1] - b[1]);
        for (int i = 0; i < dist.length; i++) {
            dist[i] = Integer.MAX_VALUE;
        }
        dist[start] = startTime;
        pq.offer(new int[]{start,startTime});

        while(!pq.isEmpty()){
            int[] cur = pq.poll();

            if(dist[cur[0]] < cur[1]) continue;

            for(Edge e : adjList[cur[0]]){
                int newDist = cur[1] + e.time;
                if(newDist < dist[e.to]){
                    pq.offer(new int[]{e.to,newDist});
                    dist[e.to] = newDist;
                }
            }
        }
        return dist;
    }

	public int cost(int B, int sCity, int eCity, int M, int mCity[], int mTime[]) {
        //전염병을 하나만 만나도 어차피 못감.
        //그니까 전염병들도 다익스트라를 돌려서 가장 빠르게 도시에 가는 경우를 미리 뽑아둠.
        int[][] coronas = new int[M][adjList.length];
        int[] minimumAccess = new int[adjList.length];
        for (int i = 0; i < M; i++) {
            coronas[i] = dijkstraForCorona(mCity[i],mTime[i]);
        }
        for (int i = 0; i < adjList.length; i++) {
            int minimum = coronas[0][i];
            for (int j = 1; j < M; j++) {
                minimum = Math.min(minimum,coronas[j][i]);
            }
            minimumAccess[i] = minimum;
        }

        int result[][] = dijkstraForCar(sCity, eCity, B, minimumAccess);
        int ans = result[eCity][0];
        for (int i = 0; i <= B; i++) {
            ans = Math.min(ans, result[eCity][i]);
        }
		return ans == Integer.MAX_VALUE ? -1 : ans;
	}
}
```
