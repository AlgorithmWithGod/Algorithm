```java
import java.io.*;
import java.util.*;

public class boj23254 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}

	public static void main(String[] args) throws Exception {
		nextLine();
		int N = nextInt();
		int M = nextInt();
		int answer = 0;
		int[] base = new int[M];
		int[] up = new int[M];
		int time = 24 * N;
		PriorityQueue<Node> pq = new PriorityQueue<>(
                (x,y) -> y.plus - x.plus
        );
		nextLine();
		for (int i = 0; i < M; i++) {
			base[i] = nextInt();
			answer += base[i];
		}
		nextLine();
		for (int i = 0; i < M; i++) {
			up[i] = nextInt();
			pq.add(new Node(100 - base[i], up[i]));
		}

        while(!pq.isEmpty()){
            Node cur = pq.poll();

            if(time >= (cur.rest / cur.plus)){
                time -= cur.rest / cur.plus;

                answer += cur.plus * (cur.rest / cur.plus);

                if(cur.rest % cur.plus >= 1){
                    pq.add(new Node(cur.rest % cur.plus,cur.rest % cur.plus));
                }
            }else if(time > 0 && (cur.rest >= time * cur.plus)){
            	answer += time * cur.plus;
                time = 0;
            }
        }

        System.out.println(answer);
	}
	static class Node{
	    int rest;
	    int plus;

	    Node(int rest,int plus){
	        this.rest = rest;
	        this.plus = plus;
	    }
	}
}
```
