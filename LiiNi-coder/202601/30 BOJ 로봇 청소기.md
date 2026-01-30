```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
public class Main{
	private static int N, M;
	private static int Vd; // 0북 1동 2남
	private static char[][] Map;
	private static int Vr, Vc;
	private static final int[][] Drdcs = {
		{-1, 0},
		{0, 1},
		{1, 0},
		{0, -1}
	};
	public static void main(String[] args) throws IOException {
		/*
		로봇청소기 N*M
		(0, 0) 시작
		N, M <= 50,
		d = 0북 1동 2남
		작동 멈출때까지 청소하는 칸 개수
		 */
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		String[] tokens = br.readLine().split(" ");
		N = Integer.parseInt(tokens[0]);
		M = Integer.parseInt(tokens[1]);
		Map = new char[N+2][M+2];
		tokens = br.readLine().split(" ");
		Vr = Integer.parseInt(tokens[0]) + 1;
		Vc = Integer.parseInt(tokens[1]) + 1;
		Vd = Integer.parseInt(tokens[2]);
		for(int c = 0; c<M+2; c++){
			for(int r : new int[]{0, N+1}){
				Map[r][c] = 'W';
			}
		}
		for(int r=1; r<N+1; r++){
			for(int c: new int[]{0, M+1}){
				Map[r][c] = 'W';
			}
		}
		for(int r = 1; r<N+1; r++){
			tokens = br.readLine().split(" ");
			for(int c = 1; c<M+1; c++){
				int isWall = Integer.parseInt(tokens[c-1]);
				if(isWall == 1){
					Map[r][c] = 'W';
				}else{
					Map[r][c] = 'X';
				}
			}
		}
		int answer = 0;
		while(true) {
			//1. 현재칸 청소X->현재칸 청소
			if(Map[Vr][Vc] == 'X'){
				Map[Vr][Vc] = 'O';
				answer++;
			}
			//2. 현재칸 주변4칸에 청소되지않은 빈칸이없을때
			boolean isNotX = true;
			for(int i = -1; i>= -4; i--){
				int nd = addDirenction(Vd, i);
				int nr = Vr + Drdcs[nd][0];
				int nc = Vc + Drdcs[nd][1];
				if(Map[nr][nc] == 'X'){
					Vd = nd;
					Vr = nr;
					Vc = nc;
					isNotX = false;
					break;
				}
			}
			if(isNotX){
				int nr = Vr + Drdcs[addDirenction(Vd, 2)][0];
				int nc = Vc + Drdcs[addDirenction(Vd, 2)][1];
				if(Map[nr][nc] != 'W'){
					Vr = nr; Vc = nc;
					continue;
				}else{
					break;
				}
			}
			// 2-1.후진가능-> 한칸 후진 후 1로
			// 2-2.후진불가능->작동멈춤
			//3. 현재칸 주변 4칸 중 청소된지않은 빈칸 존재
			// 3-1. 반시계90도회전
			// 3-2.현 방향 앞이 청소되지않았으면 한칸 전진
		}
		System.out.println(answer);
		br.close();
	}
	private static int addDirenction(int vd, int i){
		return (vd + Drdcs.length) % Drdcs.length;
	}

}
```
