```java
import java.util.*;

class Solution {
    static class Coords {
        int x1, y1, x2, y2;
        public Coords(int x1,int y1, int x2, int y2){
            this.x1 = x1;
            this.y1 = y1;
            this.x2 = x2;
            this.y2 = y2;
        }
        @Override
        public boolean equals(Object o){
            if(!(o instanceof Coords))
                return false;
            Coords c = (Coords)o;
            return (this.x1 == c.x1 && this.y1 == c.y1 && this.x2 == c.x2 && this.y2 == c.y2) || (this.x1 == c.x2 && this.y1 == c.y2 && this.x2 == c.x1 && this.y2 == c.y1);
        }

        @Override
        public int hashCode(){
            // 이렇게 순서를 맞춰줘야 함
            int sx1 = Math.min(x1, x2);
            int sx2 = Math.max(x1, x2);
            int sy1 = Math.min(y1, y2);
            int sy2 = Math.max(y1, y2);
            return Objects.hash(sx1, sy1, sx2, sy2);
            // return Objects.hash(x1, x2, y1, y2);
        }
    }

    public int solution(String dirs) {
        int answer = 0;
        HashSet<Coords> set = new HashSet<>();
        int x = 0;
        int y = 0;
        for(char d: dirs.toCharArray()){
            int nx = x;
            int ny = y;
            if(d == 'U')
                ny++;
            else if(d == 'D')
                ny--;
            else if(d == 'R')
                nx++;
            else if(d == 'L')
                nx--;

            if(nx < -5 || nx > 5 || ny < -5 || ny > 5)
                continue;
            set.add(new Coords(x, y, nx, ny));
            x = nx;
            y = ny;
        }
        answer = set.size();
        return answer;
    }
}

```
