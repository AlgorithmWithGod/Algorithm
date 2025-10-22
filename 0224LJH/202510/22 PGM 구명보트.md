```java
import java.io.*;
import java.util.*;

class Solution {
    public int solution(int[] people, int limit) {
        
        Arrays.sort(people);
        System.out.println(people);
        int front = 0;
        int answer = 0;
        int back = people.length-1;
        
        while (front < back){
            if (people[front]+people[back] <= limit){
                answer++;
                people[front++] = 0;
                people[back--] = 0;
                
                
            } else{
                back--;
            }
        }
        
        for (int n: people){
            if (n != 0) answer++;
        }
        
        return answer;
    }
}```
