```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.Iterator;
import java.util.LinkedList;
import java.util.List;
import java.util.Map;
import java.util.Queue;
import java.util.Set;
import java.util.TreeSet;

public class Main{
	// n*n 땅, r c 는 1부터
	// 처음은 모든칸에 양분 5
	// M개의 나무 땅에
	// 한칸에 여러개의 나무 가능
	private static class Tree implements Comparable<Tree>{
		int year;
		Tree(int year){
			this.year = year;
		}

		@Override
		public int compareTo(Tree o){
			return this.year - o.year;
		}
	}

	private static int[][] yangbuns;
	private static int[][] yangbunDelta;
	private static int n;
	private static int m;
	private static int k;
	private static Map<Integer, List<Tree>> treesAt1D;
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		String[] tokens = br.readLine().split(" ");
		n = Integer.parseInt(tokens[0] );
		m = Integer.parseInt(tokens[1] );
		k = Integer.parseInt(tokens[2] );
		yangbuns = new int[n][n];
		yangbunDelta = new int[n][n];
		for(int r = 0; r<n;r++)
			for(int c = 0; c<n;c++)
				yangbuns[r][c] = 5;
		int t = n;
		treesAt1D = new HashMap<>();
		for(int r = 0; r<n; r++){
			tokens = br.readLine().split(" ");
			for(int c = 0; c<n;c++){
				yangbunDelta[r][c] = Integer.parseInt(tokens[c]);
				treesAt1D.putIfAbsent(convert2to1(r, c), new LinkedList<Tree>());
			}
		}
		for(int i = 0; i<m;i++){
			tokens = br.readLine().split(" ");
			int r = Integer.parseInt(tokens[0]) - 1;
			int c = Integer.parseInt(tokens[1]) - 1;
			int year = Integer.parseInt(tokens[2]);
			// treesAt1D.putIfAbsent(convert2to1(r, c), new TreeSet<Tree>());
			treesAt1D.get(convert2to1(r, c)).add(new Tree(year));
		}

		for(Map.Entry<Integer, List<Tree>> entry : treesAt1D.entrySet()){
			int coord1D = entry.getKey();
			int[] temp = convert1to2(coord1D);
			int r = temp[0]; int c = temp[1];
			List<Tree> treeQ = entry.getValue();
			treeQ.sort((o1, o2) -> o1.year - o2.year);
		}

		int kk = k;
		while(kk-->0){
			// 봄-> 자신의 나이만큼 양분 먹음->나이++, 여러개나무-> 나이가 어린 나무부터 먹음
			Queue<int[]> yangbunsForSummer = new ArrayDeque<int[]>();
			Queue<int[]> yangbunsForFall = new ArrayDeque<int[]>();
			for(Map.Entry<Integer, List<Tree>> entry : treesAt1D.entrySet()){
				int coord1D = entry.getKey();
				int[] temp = convert1to2(coord1D);
				int r = temp[0]; int c = temp[1];
				List<Tree> treeQ = entry.getValue();
				Iterator<Tree> iter = treeQ.iterator();
				boolean shouldRemove = false;
				Tree tree = null;
				while(iter.hasNext()){
					tree = iter.next();
					if(shouldRemove){
						yangbunsForSummer.add(new int[]{r, c, tree.year/2});
						iter.remove();
					}else{
						yangbuns[r][c]-= tree.year;
						if(yangbuns[r][c]<0){
							// 먹었더니 양분 값이 음수
							//원상복귀
							yangbuns[r][c]+= tree.year;
							shouldRemove = true;
							yangbunsForSummer.add(new int[]{r, c, tree.year/2});
							iter.remove();
						}else{
							tree.year++;
							if(tree.year % 5 == 0){
								yangbunsForFall.add(new int[]{r, c});
							}
						}
					}
				}
			}
			// 만약 양분 부족-> 나무 바로죽음
			// 여름-> 봄에 죽은 나무-> 양분, 죽은 나무 나이/2 값이 추가
			while(!yangbunsForSummer.isEmpty()){
				int[] yangbunInfo = yangbunsForSummer.poll();
				int r = yangbunInfo[0]; int c = yangbunInfo[1];
				yangbuns[r][c]+= yangbunInfo[2];
			}
			// 가을-> 나이 5의배수인 나무가 번식 -> 인접한 8개칸에 나이1인 나무생김(바운드고려)
			for(int[] coords: yangbunsForFall){
				int r = coords[0];
				int c = coords[1];
				for(int dr = -1; dr <=1; dr++){
					for(int dc = -1; dc <=1; dc++){
						if(dr == 0 && dc == 0) continue;
						int nr = r+dr;
						int nc = c+dc;
						if(nr < 0 || nr >= n || nc < 0 || nc >= n) continue;
						treesAt1D.get(convert2to1(nr, nc)).add(0, new Tree(1));
					}
				}
			}
			// 겨울-> 입력으로 해당 땅에 양분추가됨
			for(int r = 0; r<n; r++)
				for(int c = 0; c<n; c++){
					yangbuns[r][c] += yangbunDelta[r][c];
				}
			// K년이 지난후 살아있는 나무개수
		}
		int answer =0;
		for(Map.Entry<Integer, List<Tree>> entry : treesAt1D.entrySet()){
			answer += entry.getValue().size();
		}
		System.out.println(answer);
		br.close();
	}

	private static int[] convert1to2(int coord1D) {
		return new int[]{coord1D / n, coord1D % n};
	}

	private static Integer convert2to1(int r, int c) {
		return r*n + c;
	}
}
```
