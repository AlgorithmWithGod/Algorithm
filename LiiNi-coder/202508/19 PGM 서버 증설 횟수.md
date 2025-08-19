```java
class Solution {
    public int solution(int[] players, int m, int k) {
        int answer = 0;
        int[] servers = new int[24+k];
        for(int i = 0; i<players.length; i++){
            int player = players[i];
            int mustServer = player / m;
            if(servers[i] < mustServer){
                int needServers = mustServer - servers[i];
                for(int di = 0; di<k; di++)
                    servers[i+di]+= needServers;
                answer+= needServers;
            }
        }
        return answer;
    }
}
```
