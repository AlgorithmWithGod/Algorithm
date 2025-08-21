```java
class Solution {
    public int convertTime(String time) {
        String[] args = time.split(":");
        return Integer.parseInt(args[0])*3600 + Integer.parseInt(args[1])*60 + Integer.parseInt(args[2]);
    }
    
    public String solution(String play_time, String adv_time, String[] logs) {
        // 1. imos
        int N = convertTime(play_time), M = convertTime(adv_time);
        long[] arr = new long[N+2];
        for(String log : logs) {
            String[] args = log.split("-");
            int start = convertTime(args[0]), end = convertTime(args[1]);
            arr[start]++;
            arr[end]--;
        }
        
        // 2. find
        long s = arr[0];
        long[] b = new long[N+1];
        b[0] = s;
        for(int i=1;i<=N;i++) {
            s += arr[i];
            b[i] = s + b[i-1];
        }
        
        int ans = 0;
        long max = b[M];
        for(int i=1;i+M-1<=N;i++) if(b[i+M-1]-b[i-1] > max) {
            max = b[i+M-1]-b[i-1];
            ans = i;
        }
        
        int hour = ans / 3600;
        ans %= 3600;
        int minute = ans / 60;
        ans %= 60;
        int second = ans;
        
        String result = "";
        if(hour < 10) result += "0";
        result += Integer.toString(hour) + ":";
        if(minute < 10) result += "0";
        result += Integer.toString(minute) + ":";
        if(second < 10) result += "0";
        result += Integer.toString(second);
        
        return result;
        
    }
}
```
