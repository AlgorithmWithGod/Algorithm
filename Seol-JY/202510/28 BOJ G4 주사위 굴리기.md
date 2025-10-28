```java
import java.io.*;
import java.util.*;

public class Main {
    static class Dice {
        int top, bottom, front, back, left, right;
        
        public Dice() {
            this.top = 0;
            this.bottom = 0;
            this.front = 0;
            this.back = 0;
            this.left = 0;
            this.right = 0;
        }
        
        public void rollEast() {
            int temp = top;
            top = left;
            left = bottom;
            bottom = right;
            right = temp;
        }
        
        public void rollWest() {
            int temp = top;
            top = right;
            right = bottom;
            bottom = left;
            left = temp;
        }
        
        public void rollNorth() {
            int temp = top;
            top = front;
            front = bottom;
            bottom = back;
            back = temp;
        }
        
        public void rollSouth() {
            int temp = top;
            top = back;
            back = bottom;
            bottom = front;
            front = temp;
        }
        
        public int getTop() {
            return top;
        }
        
        public int getBottom() {
            return bottom;
        }
        
        public void setBottom(int value) {
            this.bottom = value;
        }
    }
    
    static class Position {
        int x, y;
        
        public Position(int x, int y) {
            this.x = x;
            this.y = y;
        }
        
        public Position move(int direction) {
            switch(direction) {
                case 1:
                    return new Position(x, y + 1);
                case 2:
                    return new Position(x, y - 1);
                case 3:
                    return new Position(x - 1, y);
                case 4:
                    return new Position(x + 1, y);
                default:
                    return this;
            }
        }
        
        public boolean isValid(int n, int m) {
            return x >= 0 && x < n && y >= 0 && y < m;
        }
    }
    
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        
        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());
        int x = Integer.parseInt(st.nextToken());
        int y = Integer.parseInt(st.nextToken());
        int k = Integer.parseInt(st.nextToken());
        
        int[][] map = new int[n][m];
        for (int i = 0; i < n; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < m; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        
        Dice dice = new Dice();
        Position pos = new Position(x, y);
        
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < k; i++) {
            int direction = Integer.parseInt(st.nextToken());
            Position nextPos = pos.move(direction);
            
            if (!nextPos.isValid(n, m)) {
                continue;
            } 
            
            switch(direction) {
                case 1:
                    dice.rollEast();
                    break;
                case 2:
                    dice.rollWest();
                    break;
                case 3:
                    dice.rollNorth();
                    break;
                case 4:
                    dice.rollSouth();
                    break;
            }
            
            pos = nextPos;
            
            if (map[pos.x][pos.y] == 0) {
                map[pos.x][pos.y] = dice.getBottom();
            } else {
                dice.setBottom(map[pos.x][pos.y]);
                map[pos.x][pos.y] = 0;
            }
            
            bw.write(dice.getTop() + "\n");
        }
        
        bw.flush();
        bw.close();
        br.close();
    }
}
```
