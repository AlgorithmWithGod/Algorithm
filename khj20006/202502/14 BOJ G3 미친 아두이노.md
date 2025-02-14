```java

import java.util.*;
import java.io.*;

class Main {
	
	// IO field
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st;

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static long nextLong() {return Long.parseLong(st.nextToken());}
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
    static int R, C;
    static char[][] arr;
    static char[] command;
    static int x, y;
    static List<int[]> crazy;
    static int[] dx = {0,1,1,1,0,0,0,-1,-1,-1};
    static int[] dy = {0,-1,0,1,-1,0,1,-1,0,1};
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		nextLine();
        R = nextInt();
        C = nextInt();
        arr = new char[R][C];
        crazy = new ArrayList<>();

        for(int i=0;i<R;i++) {
            char[] temp = br.readLine().toCharArray();
            for(int j=0;j<C;j++){
                arr[i][j] = temp[j];
                if(temp[j] == 'I') {
                    x = i;
                    y = j;
                }
                if(temp[j] == 'R') crazy.add(new int[]{i,j});
            }
        }
        command = br.readLine().toCharArray();

	}
	
	static void solve() throws Exception{
		
        int cnt = 0;
        for(char i:command){
            cnt++;
            if(!move(i-'0')) {
                bw.write("kraj "+cnt+"\n");
                return;
            }
        }

        arr = new char[R][C];
        for(int i=0;i<R;i++) Arrays.fill(arr[i], '.');
        arr[x][y] = 'I';
        for(int[] arduino:crazy) arr[arduino[0]][arduino[1]] = 'R';

        for(int i=0;i<R;i++){
            for(int j=0;j<C;j++) bw.write(arr[i][j]);
            bw.write("\n");
        }
		
	}

    static boolean move(int dir){
        
        x += dx[dir];
        y += dy[dir];

        int[][] cnt = new int[R][C];

        for(int[] arduino:crazy){

            if(arduino[0] > x) arduino[0]--;
            else if(arduino[0] < x) arduino[0]++;

            if(arduino[1] > y) arduino[1]--;
            else if(arduino[1] < y) arduino[1]++;

            cnt[arduino[0]][arduino[1]]++;

            if(arduino[0] == x && arduino[1] == y) return false;
        }


        crazy = new ArrayList<>();

        for(int i=0;i<R;i++) for(int j=0;j<C;j++){
            if(cnt[i][j] == 1) crazy.add(new int[]{i,j});
        }

        return true;

    }
	
}

```
