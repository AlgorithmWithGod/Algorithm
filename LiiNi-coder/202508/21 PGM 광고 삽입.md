```java
import java.util.*;

class Solution {
    static class TimeInfo{
        int startCount; //time에 시작하는 log개수
        int endCount;//time에 끝나는 log개수
        long prefix; //time까지의 가중치 누적합
        
        TimeInfo(int sc, int ec, long p){
            this.startCount = sc;
            this.endCount = ec;
            this.prefix = p;
        }
        @Override
        public String toString(){
            return String.format("sc: %d, ec: %d prefix:%d", this.startCount, this.endCount, this.prefix);
        }
    }
    
    private static TreeMap<Integer, TimeInfo> timeInfos;
    public String solution(String play_time, String adv_time, String[] logs) {
        timeInfos = new TreeMap<Integer, TimeInfo>();
        timeInfos.put(0, new TimeInfo(0, 0, 0));

        for(String log : logs){
            String[] temp = log.split("-");
            int startTime = convertToSeconds(temp[0]);
            int endTime = convertToSeconds(temp[1]);
            
            timeInfos.computeIfAbsent(startTime, k -> new TimeInfo(0, 0, 0)).startCount++;
            timeInfos.computeIfAbsent(endTime, k -> new TimeInfo(0, 0, 0)).endCount++;
        }
        
        //prefix 누적합 계산
        long currentLogs = 0;
        long cumulativeSum = 0;
        Integer prevTime = null;
        for(Map.Entry<Integer, TimeInfo> entry : timeInfos.entrySet()){
            int time = entry.getKey();
            TimeInfo info = entry.getValue();
            
            if(prevTime != null){
                cumulativeSum += currentLogs * (time - prevTime);
            }
            info.prefix = cumulativeSum;
            currentLogs += info.startCount - info.endCount;
            prevTime = time;
        }

        int advSeconds = convertToSeconds(adv_time);
        int playSeconds = convertToSeconds(play_time);
        long maxViewTime = 0;
        int bestStartTime = 0;
        for(int startTime = 0; startTime <= playSeconds - advSeconds; startTime++){
            int endTime = startTime + advSeconds;
            long viewTime = getViewTime(startTime, endTime);
            
            if(viewTime > maxViewTime){
                maxViewTime = viewTime;
                bestStartTime = startTime;
            }
        }
        
        return convertToHHMMSS(bestStartTime);
    }
    
    //startTime부터 endTime까지의 총 재생시간 계산
    private long getViewTime(int startTime, int endTime){
        long endPrefix = getPrefixSum(endTime);
        long startPrefix = getPrefixSum(startTime);
        return endPrefix - startPrefix;
    }
    
    //time 시점까지의 누적 재생시간
    private long getPrefixSum(int time){
        Map.Entry<Integer, TimeInfo> floorEntry = timeInfos.floorEntry(time);
        if(floorEntry == null) return 0;
        
        int floorTime = floorEntry.getKey();
        TimeInfo floorInfo = floorEntry.getValue();
        long prefix = floorInfo.prefix;
        
        //구간 내 재생시간 추가 계산
        if(time > floorTime){
            long currentLogs = 0;
            // floorTime 이후의 로그 수 계산
            for(Map.Entry<Integer, TimeInfo> entry : timeInfos.headMap(floorTime, true).entrySet()){
                TimeInfo info = entry.getValue();
                currentLogs += info.startCount - info.endCount;
            }
            prefix += currentLogs * (time - floorTime);
        }
        return prefix;
    }
    
    private int convertToSeconds(String hms){
        String[] tokens = hms.split(":");
        int result = 0;
        for(int i = 2, gop = 1; i>=0; i--, gop*=60){
            result += Integer.parseInt(tokens[i])*gop;
        }
        return result;
    }
    
    private String convertToHHMMSS(int seconds){
        int h = seconds / 3600;
        seconds %= 3600;
        int m = seconds / 60;
        int s = seconds % 60;
        return String.format("%02d:%02d:%02d", h, m, s);
    }
}

```
