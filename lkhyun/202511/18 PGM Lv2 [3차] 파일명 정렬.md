```java
import java.util.stream.*;
class Solution {
    static class File implements Comparable<File>{
        String fileName;
        String HEAD;
        int NUMBER;
        int index;
        
        File(String fileName, int index){
            this.fileName = fileName;
            
            int i = 0;
            while(i<fileName.length() && !Character.isDigit(fileName.charAt(i))) i++;
            HEAD = fileName.substring(0,i);
            
            int j = i;
            while(j<fileName.length() && Character.isDigit(fileName.charAt(j))) j++;
            NUMBER = Integer.parseInt(fileName.substring(i,j));
            
            this.index = index;
        }
        
        @Override
        public int compareTo(File o){
            int compare1 = this.HEAD.toLowerCase().compareTo(o.HEAD.toLowerCase());
            if(compare1 != 0) return compare1;
            
            int compare2 = Integer.compare(this.NUMBER, o.NUMBER);
            if(compare2 != 0) return compare2;
            
            return Integer.compare(this.index, o.index);
        }
        
    }
    public String[] solution(String[] files) {
        return IntStream.range(0,files.length)
                        .mapToObj(i -> new File(files[i],i))
                        .sorted()
                        .map(i -> i.fileName)
                        .toArray(String[]::new);
    }
}
```
