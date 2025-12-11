```java
import java.util.*;

class Solution {
    private static Map<String, int[]> map;
    public int solution(String str1, String str2) {
        map = new HashMap<String, int[]>();
        pushSet(str1, 0);
        pushSet(str2, 1);
        
        int bunja = 0;
        int bunmo = 0;
        for(Map.Entry<String, int[]> entry: map.entrySet()){
            int[] v = entry.getValue();
            bunja += Math.min(v[0], v[1]);
            bunmo += Math.max(v[0], v[1]);
        }

        if(bunmo == 0)
            return 65536;

        return (int)( (bunja /(float)bunmo) * 65536 );
    }

    private void pushSet(String str, int index){
        char[] cs = str.toCharArray();
        for(int i = 0; i < cs.length - 1; i++){
            char a = cs[i];
            char b = cs[i + 1];
            if(!Character.isLetter(a) || !Character.isLetter(b))
                continue;
            a = Character.toLowerCase(a);
            b = Character.toLowerCase(b);

            String key = "" + a + b;

            if(!map.containsKey(key))
                map.put(key, new int[2]);

            map.get(key)[index]++;
        }
    }
}

```
