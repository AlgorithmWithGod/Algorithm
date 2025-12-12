```java
import java.util.*;
import java.io.*;

public class Main {
    
    static int treeCnt, ans;
    static Tree[] trees;
    static Tree[] sortedByX;
    static Tree[] sortedByY;
    
    static class Tree {
        int y, x, cost;
        
        public Tree(int y, int x, int cost) {
            this.y = y;
            this.x = x;
            this.cost = cost;
        }
    }
    
    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }
    
    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        treeCnt = Integer.parseInt(br.readLine());
        trees = new Tree[treeCnt];
        ans = treeCnt-1; 
        
        for (int i = 0; i < treeCnt; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());
            int cost = Integer.parseInt(st.nextToken());
            trees[i] = new Tree(y, x, cost);
        }
        
        // x 기준 정렬
        sortedByX = Arrays.copyOf(trees, treeCnt);
        Arrays.sort(sortedByX, (a, b) -> a.x - b.x);
        
        // y 기준 정렬
        sortedByY = Arrays.copyOf(trees, treeCnt);
        Arrays.sort(sortedByY, (a, b) -> a.y - b.y);
    }
    
    private static void process() {
        // 모든 가능한 직사각형에 대해 시도
        for (int i = 0; i < treeCnt; i++) {
            for (int j = i; j < treeCnt; j++) {  
                for (int k = 0; k < treeCnt; k++) {
                    for (int l = k; l < treeCnt; l++) {  
                        int minX = sortedByX[i].x;
                        int maxX = sortedByX[j].x;
                        int minY = sortedByY[k].y;
                        int maxY = sortedByY[l].y;
                        
                        checkRectangle(minX, maxX, minY, maxY);
                    }
                }
            }
        }
    }
    
    private static void checkRectangle(int minX, int maxX, int minY, int maxY) {
        // 둘레 계산
        int width = maxX - minX;
        int height = maxY - minY;
        int perimeter = (width + height) * 2;
        
        // 직사각형 내부의 나무들 찾기
        List<Integer> insideCosts = new ArrayList<>();
        int sum = 0;
        int cutCount = 0;
        for (int i = 0; i < treeCnt; i++) {
            if (trees[i].x >= minX && trees[i].x <= maxX &&
                trees[i].y >= minY && trees[i].y <= maxY) {
                insideCosts.add(trees[i].cost);
            } else {
            	sum += trees[i].cost;
            	cutCount++;
            }
        }
        
        if (sum >= perimeter) {
            ans = Math.min(ans, cutCount);
            return;
        }
        
        // cost 큰 순으로 정렬
        Collections.sort(insideCosts, Collections.reverseOrder());

        for (int cost : insideCosts) {
            sum += cost;
            cutCount++;
            if (sum >= perimeter) {
                ans = Math.min(ans, cutCount);
                break;
            }
        }
    }
    
    private static void print() {
        System.out.println(ans);
    }
}
```
