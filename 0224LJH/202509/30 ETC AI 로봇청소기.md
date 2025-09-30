```java
import java.io.*;
import java.util.*;

public class Main {
    /*
    1. 맨 위 왼쪽이 1,1 맨 오른쪽 아래가 N,N
    이동 우선순위는 위 (행번호 감소) , 그 다음 왼쪽 (열 번호 감소)
    이동거리가 가장 가깝고, 물건이나 청소기가 없는 오염된 격자로 이동
    
    2. 청소는 자신이 바라보는 방향의 뒷쪽을 제외한 네 칸. 
    가장 먼지량이 큰 방향을 바라보고 청소 시작. 최대 한 격자당 20청소

    합이 같은 방향이 여러개면 오른쪽,아래쪽,왼쪽,위쪽 순


    3. 먼지가 있는 모든 격자에 5씩 추가 


    4. 깨끗한 격자는 주변 4방향 격자의 먼지량 합/10의 먼지가 확산됨. 확산은 동시에 진행됨 
    -> 한번에 반영

    5/ 총 먼지량 출력

    900  * 50 * 50 = 90000 * 25 = 225만 -> 완탐 된다.

    각각의 청소기에서 bfs를 진행하며 최단 거리의 먼지를 찾는다.
    */

    static class Cleaner{
        int y,x;

        public Cleaner(int y, int x){
            this.y = y;
            this.x = x;
        }
    }

    static StringBuilder sb = new StringBuilder();
    static int[][] arr;
    static boolean[][] hasCleaner;
    static int[] dy = {-1,0,1,0};
    static int[] dx = {0,-1,0,1};
    static int[] dy2 = {0,-1,0,1,0};
    static int[] dx2 = {-1,0,1,0,0};    



    static Cleaner[] cleaners;
    static int ans, size, cleanerCnt, testCnt;

    
    public static void main(String[] args) throws IOException  {
        
        init();
        for (int i = 0; i < testCnt; i++){
            process();
            print();
        }

    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer  st = new StringTokenizer(br.readLine());

        size = Integer.parseInt(st.nextToken());
        cleanerCnt = Integer.parseInt(st.nextToken());
        testCnt = Integer.parseInt(st.nextToken());

        arr = new int[size+2][size+2];
        hasCleaner = new boolean[size+2][size+2];
        cleaners = new Cleaner[cleanerCnt];

        for (int i = 1 ; i <= size; i++){
            st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= size; j++){
                arr[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        for (int i = 0; i < cleanerCnt; i++){
            st = new StringTokenizer(br.readLine());
            int y = Integer.parseInt(st.nextToken());
            int x = Integer.parseInt(st.nextToken());
            cleaners[i] = new Cleaner(y,x);
            hasCleaner[y][x] = true;
        }

    }

    private static void process(){
        ans = 0;

        // 1. 움직임
        for (int i = 0; i < cleanerCnt; i++)move(i);

        //2. 청소
        for (int i = 0; i < cleanerCnt; i++)clean(i); 


        //  3. 먼지가 있는 모든 격자에 5씩 추가
        for (int i = 1 ; i <= size; i++){
            for (int j = 1; j <= size; j++){
                if (arr[i][j] > 0) arr[i][j] += 5;
            }
        }

        // 4. 먼지 확산
        dustDiffuse();


        // 5. 답 구해서 출력
        for (int i = 1 ; i <= size; i++){
            for (int j = 1; j <= size; j++){
                if (arr[i][j] < 0) continue;
                ans += arr[i][j];
            }
        }
    }

    private static void clean(int num){
        Cleaner c = cleaners[num];
        int max = 0;
        int maxDir= -1;
        int sum = 0;
        for (int i = 0; i < 5; i++) {
            int ny = c.y + dy2[i];
            int nx = c.x + dx2[i];
            int newNum = Math.min(arr[ny][nx],20);

            if (newNum > 0) {
                sum += newNum;
            }
        }
        for (int i = 0; i < 4; i++){
            int ny = c.y + dy2[i];
            int nx = c.x + dx2[i];
            int newNum = Math.min(arr[ny][nx],20);
            int temp = sum - newNum;
            if (temp > max){
                max = temp;
                maxDir = i;
            }
        }

        for (int i = 0; i < 5; i++){
            if (maxDir == i) continue;
            int ny = c.y + dy2[i];
            int nx = c.x + dx2[i];
            if (arr[ny][nx] == -1) continue;
            arr[ny][nx] = Math.max(arr[ny][nx] - 20, 0);

        }
    }

    private static void move(int num ){
        Cleaner c = cleaners[num];
        if (arr[c.y][c.x] != 0) return;
        Queue<Integer> qY = new LinkedList<>();
        Queue<Integer> qX = new LinkedList<>();
        boolean[][] visited = new boolean[size+1][size+1];

        int ansY = 500;
        int ansX = 500;

        visited[c.y][c.x] = true;
        qY.add(c.y);
        qX.add(c.x);

        
        while(!qY.isEmpty() && ansY == 500){
            int qSize = qY.size();
            for (int j = 0; j < qSize; j++){
                int y = qY.poll();
                int x = qX.poll();
                
                for (int i = 0 ; i < 4 ; i++){
                    int ny = y + dy[i];
                    int nx = x + dx[i];
                    if ( ny <= 0 || nx <= 0 || ny > size || nx > size) continue;
                    if (hasCleaner[ny][nx] || visited[ny][nx] || arr[ny][nx] == -1) continue;
                    
                    visited[ny][nx] = true;
                    if (arr[ny][nx] > 0){
                        if (ny < ansY || (ny == ansY && nx < ansX ) ){
                            ansY = ny;
                            ansX = nx;
                        }
                        continue;
                        
                    }
                    qY.add(ny);
                    qX.add(nx);
                }
            }



        }

        if (ansY == 500) return;
        hasCleaner[c.y][c.x] = false;
        c.y = ansY;
        c.x = ansX;
        hasCleaner[c.y][c.x] = true;

    }

    private static void dustDiffuse(){
        int[][] temp = new int[size+2][size+2];

        for (int i =  1; i <= size; i++){
            for (int j = 1; j <= size; j++){
                if (arr[i][j] == 0){
                    for (int k = 0 ; k < 4; k++){
                        int ny = i + dy[k];
                        int nx = j + dx[k];
                        if (arr[ny][nx] == -1) continue;
                        temp[i][j] += arr[ny][nx];
                    }
                }
            }
        }
        for (int i =  1; i <= size; i++){
            for (int j = 1; j <= size; j++){
                arr[i][j] += temp[i][j]/10;
            }
        }
    }

    private static void print(){
        System.out.println(ans);
    }
}
```
