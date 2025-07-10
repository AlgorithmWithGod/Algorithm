```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
    static int[] map = new int[10];
    static int sum;
    static int minToggle = Integer.MAX_VALUE;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        for (int i = 0; i < 10; i++) {
            String input = br.readLine();
            for (int j = 0; j < 10; j++) {
                if (input.charAt(j) == 'O') {
                    map[i] |= (1 << j);
                }
            }
        }

        for (int firstRow = 0; firstRow < (1 << 10); firstRow++) {
            int[] tempMap = map.clone();
            int toggleCount = 0;
            
            for (int j = 0; j < 10; j++) {
                if (isLightOn(firstRow, j)) {
                    toggle(tempMap, 0, j);
                    toggleCount++;
                }
            }
            
            for (int i = 1; i < 10; i++) {
                for (int j = 0; j < 10; j++) {
                    if (isLightOn(tempMap[i - 1], j)) {
                        toggle(tempMap, i, j);
                        toggleCount++;
                    }
                }
            }
            
            if (tempMap[9] == 0) {
                minToggle = Math.min(minToggle, toggleCount);
            }
        }
        
        System.out.println(minToggle == Integer.MAX_VALUE ? -1 : minToggle);
    }

    static boolean isLightOn(int row, int col) {
        return (row & (1 << col)) != 0;
    }

    static void toggle(int[] map, int x, int y) {
        map[x] ^= (1 << y);
        
        if (x > 0) map[x - 1] ^= (1 << y);
        if (x < 9) map[x + 1] ^= (1 << y);
        if (y > 0) map[x] ^= (1 << (y - 1));
        if (y < 9) map[x] ^= (1 << (y + 1));
    }
}
```
