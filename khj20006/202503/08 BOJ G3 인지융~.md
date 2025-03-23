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

	static int N, C, E;
	static char[][] A;
	static int[] dx = {1,0,-1,0};
	static int[] dy = {0,1,0,-1};
    
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = Integer.parseInt(br.readLine());
		nextLine();
		C = nextInt();
		E = nextInt();
		A = new char[N][N];
		
	}
	
	static void solve() throws Exception{
		
		int G = 1;
		for(int g=0;g<N;g++){
		  if(C == 0) break;
		  int x=0, y=g;
		  for(int k=0;k<=g;k++){
		    if(C == 0) break;
		    A[x++][y--] = '1';
		    C--;
		  }
		}
	  for(int g=1;g<N;g++){
	    if(C == 0) break;
	    int x=g, y=N-1;
	    for(int k=0;k<=N-1-g;k++){
	      if(C == 0) break;
	      A[x++][y--] = '1';
	      C--;
	    }
	  }
		
		
		
		for(int g=N-1;g>=0;g--){
		  if(E == 0) break;
		  int x=N-1, y=g;
		  for(int k=0;k<=N-1-g;k++){
		    if(E == 0) break;
		    if(!safe(x,y)) {
		      bw.write("-1");
		      return;
		    }
		    A[x--][y++] = '2';
		    E--;
		  }
		}
		for(int g=N-2;g>=0;g--){
		  if(E == 0) break;
		  int x=g, y=0;
		  for(int k=0;k<=g;k++){
		    if(E == 0) break;
		    if(!safe(x,y)){
		      bw.write("-1");
		      return;
		    }
		    A[x--][y++] = '2';
		    E--;
		  }
		}
		
		bw.write("1\n");
		for(int i=0;i<N;i++){
		  for(int j=0;j<N;j++) bw.write((A[i][j] >= '1' ? A[i][j] : '0'));
		  bw.write("\n");
		}
		
	}
	
	static boolean safe(int x, int y){
	  for(int i=0;i<4;i++){
	    int xx = x+dx[i], yy = y+dy[i];
	    if(xx<0 || xx>=N || yy<0 || yy>=N) continue;
	    if(A[xx][yy] == '1') return false;
	  }
	  return true;
	}
	
}

```
