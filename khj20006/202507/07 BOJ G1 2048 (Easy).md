```java
import java.util.*;
import java.io.*;

class IOController {
    BufferedReader br;
    BufferedWriter bw;
    StringTokenizer st;

    public IOController() {
        br = new BufferedReader(new InputStreamReader(System.in));
        bw = new BufferedWriter(new OutputStreamWriter(System.out));
        st = new StringTokenizer("");
    }

    String nextLine() throws Exception {
        String line = br.readLine();
        st = new StringTokenizer(line);
        return line;
    }

    String nextToken() throws Exception {
        while (!st.hasMoreTokens()) nextLine();
        return st.nextToken();
    }

    int nextInt() throws Exception {
        return Integer.parseInt(nextToken());
    }

    long nextLong() throws Exception {
        return Long.parseLong(nextToken());
    }

    double nextDouble() throws Exception {
        return Double.parseDouble(nextToken());
    }

    void close() throws Exception {
        bw.flush();
        bw.close();
    }

    void write(String content) throws Exception {
        bw.write(content);
    }

}

public class Main {

    static IOController io;

    //

    static int N;
    static int[][] board;
    static int ans = 0;
    static String[] dirs = {"left", "right", "up", "down"};

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        board = new int[N][N];
        for(int i=0;i<N;i++) for(int j=0;j<N;j++) board[i][j] = io.nextInt();

    }

    static void solve() throws Exception {

        backtracking(0);
        io.write(ans + "\n");

    }

    static void backtracking(int turn) {

        for(int i=0;i<N;i++) for(int j=0;j<N;j++) ans = Math.max(ans, board[i][j]);

        if(turn >= 5) return;

        for(String dir : dirs) {

            int[][] copy = new int[N][N];
            for(int i=0;i<N;i++) for(int j=0;j<N;j++) copy[i][j] = board[i][j];
            move(dir);
            backtracking(turn+1);
            for(int i=0;i<N;i++) for(int j=0;j<N;j++) board[i][j] = copy[i][j];

        }

    }

    static void move(String direction) {

        if(direction.equals("left")) {
            for(int i=0;i<N;i++) {
                List<Integer> list = new ArrayList<>();
                for(int j=0;j<N;j++) if(board[i][j] != 0) {
                    list.add(board[i][j]);
                }
                List<Integer> newList = compress(list);
                for(int j=0;j<N;j++) {
                    board[i][j] = j >= newList.size() ? 0 : newList.get(j);
                }
            }
        }
        else if(direction.equals("right")) {
            for(int i=0;i<N;i++) {
                List<Integer> list = new ArrayList<>();
                for(int j=N-1;j>=0;j--) if(board[i][j] != 0) {
                    list.add(board[i][j]);
                }
                List<Integer> newList = compress(list);
                for(int j=N-1;j>=0;j--) {
                    board[i][j] = N-j > newList.size() ? 0 : newList.get(N-j-1);
                }
            }
        }
        else if(direction.equals("up")) {
            for(int j=0;j<N;j++) {
                List<Integer> list = new ArrayList<>();
                for(int i=0;i<N;i++) if(board[i][j] != 0) {
                    list.add(board[i][j]);
                }
                List<Integer> newList = compress(list);
                for(int i=0;i<N;i++) {
                    board[i][j] = i >= newList.size() ? 0 : newList.get(i);
                }
            }
        }
        else {
            for(int j=0;j<N;j++) {
                List<Integer> list = new ArrayList<>();
                for(int i=N-1;i>=0;i--) if(board[i][j] != 0) {
                    list.add(board[i][j]);
                }
                List<Integer> newList = compress(list);
                for(int i=N-1;i>=0;i--) {
                    board[i][j] = N-i > newList.size() ? 0 : newList.get(N-i-1);
                }
            }
        }

    }

    static List<Integer> compress(List<Integer> list) {

        List<Integer> newList = new ArrayList<>();
        for(int j=0;j<list.size();j++) {
            int prev = list.get(j);
            if(j == list.size()-1) {
                newList.add(prev);
                break;
            }
            int next = list.get(j+1);
            if(prev == next) {
                newList.add(prev<<1);
                j++;
            }
            else newList.add(prev);
        }

        return newList;

    }

}
```
