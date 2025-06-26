```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
    
    static int n, answer;
    static int[][] map;
    
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine());
        answer = 0;
        map = new int[n][n];
        
        for (int i = 0; i < n; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 0; j < n; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        
        game(0);
        System.out.println(answer);
    }
    
    public static void game(int count) {
        if (count == 5) {
            findMax();
            return;
        }
        
        int[][] backup = new int[n][n];
        for (int i = 0; i < n; i++) {
            backup[i] = map[i].clone();
        }
        
        for (int dir = 0; dir < 4; dir++) {
            move(dir);
            game(count + 1);
            
            for (int i = 0; i < n; i++) {
                map[i] = backup[i].clone();
            }
        }
    }
    
    public static void move(int dir) {
        if (dir == 0) {
            for (int j = 0; j < n; j++) {
                int index = 0;
                int prev = 0;
                for (int i = 0; i < n; i++) {
                    if (map[i][j] != 0) {
                        if (prev == map[i][j]) {
                            map[index - 1][j] = prev * 2;
                            prev = 0;
                        } else {
                            prev = map[i][j];
                            map[index][j] = prev;
                            index++;
                        }
                        if (i != index - 1) map[i][j] = 0;
                    }
                }
            }
        } else if (dir == 1) {
            for (int j = 0; j < n; j++) {
                int index = n - 1;
                int prev = 0;
                for (int i = n - 1; i >= 0; i--) {
                    if (map[i][j] != 0) {
                        if (prev == map[i][j]) {
                            map[index + 1][j] = prev * 2;
                            prev = 0;
                        } else {
                            prev = map[i][j];
                            map[index][j] = prev;
                            index--;
                        }
                        if (i != index + 1) map[i][j] = 0;
                    }
                }
            }
        } else if (dir == 2) {
            for (int i = 0; i < n; i++) {
                int index = 0;
                int prev = 0;
                for (int j = 0; j < n; j++) {
                    if (map[i][j] != 0) {
                        if (prev == map[i][j]) {
                            map[i][index - 1] = prev * 2;
                            prev = 0;
                        } else {
                            prev = map[i][j];
                            map[i][index] = prev;
                            index++;
                        }
                        if (j != index - 1) map[i][j] = 0;
                    }
                }
            }
        } else {
            for (int i = 0; i < n; i++) {
                int index = n - 1;
                int prev = 0;
                for (int j = n - 1; j >= 0; j--) {
                    if (map[i][j] != 0) {
                        if (prev == map[i][j]) {
                            map[i][index + 1] = prev * 2;
                            prev = 0;
                        } else {
                            prev = map[i][j];
                            map[i][index] = prev;
                            index--;
                        }
                        if (j != index + 1) map[i][j] = 0;
                    }
                }
            }
        }
    }
    
    public static void findMax() {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                answer = Math.max(answer, map[i][j]);
            }
        }
    }
}
```
