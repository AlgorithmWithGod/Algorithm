```java
class Solution {
    public String solution(String s) {
        String temp = s.toLowerCase();
        StringBuilder sb = new StringBuilder();
        String[] splits = temp.split(" ",-1);
        for (int i = 0; i < splits.length; i++) {
            String split = splits[i];
            if (split.isEmpty()) {
            } else if (!Character.isDigit(split.charAt(0))) {
                sb.append(Character.toUpperCase(split.charAt(0)));
                sb.append(split.substring(1));
            } else {
                sb.append(split);
            }
            
            if (i < splits.length - 1) {
                sb.append(" ");
            }
        }
        return sb.toString();
    }
}
```
