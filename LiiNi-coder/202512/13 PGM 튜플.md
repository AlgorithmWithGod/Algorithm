import java.util.*;

class Solution {
    public int[] solution(String s) {
        s = s.substring(2, s.length() - 2);
        String[] groups = s.split("}", "{");

        Arrays.sort(groups, (a, b) -> a.length() - b.length());
        Set<Integer> used = new HashSet<Integer>();
        int[] answer = new int[groups.length];
        int index = 0;
        for(String group : groups){
            String[] nums = group.split(",");
            for(String num : nums){
                int value = Integer.parseInt(num);
                if(!used.contains(value)){
                    used.add(value);
                    answer[index++] = value;
                    break;
                }
            }
        }
        return answer;
    }
}
