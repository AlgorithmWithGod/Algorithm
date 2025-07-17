```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;

public class Main {
    static int[][] arr;
    static boolean finished = false;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        arr = new int[9][9];
        for (int i = 0; i < 9; i++) arr[i] = Arrays.stream(br.readLine().split("")).mapToInt(Integer::parseInt).toArray();
        process();
        print();
    }



    private static void print() {
        for (int i = 0; i<9; i++) {
            for (int j = 0; j < 9; j++) {
                System.out.print(arr[i][j]);
            }
            System.out.println();
        }
    }

    private static void process() {
        int stY = -1;
        int stX = -1;

        outer:
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                if (arr[i][j] == 0) {
                    stY = i;
                    stX = j;
                    break outer;
                }
            }
        }
        boolean[] nums = findAvailable(stY,stX);
        for (int i = 1; i <= 9; i++) {
            if (finished) return;
            if (!nums[i])continue;
            arr[stY][stX] = i;
            sudoku(stY,stX);

        }

    }


    private static void sudoku(int y, int x) {
        int ny = -1;
        int nx = -1;
        outer:
        for (int i = y; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                if(arr[i][j] != 0) continue;
                else {
                    ny = i;
                    nx = j;
                    break outer;
                }
            }
        }
        if(ny == -1 && nx == -1) {
            finished = true;
            return;
        }

        boolean[] nums = findAvailable(ny,nx);
        for (int i = 1; i <= 9; i++) {
            if (finished) return;
            if (!nums[i])continue;
            arr[ny][nx] = i;
            sudoku(ny,nx);
            if(!finished)arr[ny][nx] = 0;

        }

    }

    private static boolean[] findAvailable(int stY, int stX) {
        boolean[] ans = new boolean[10];
        Arrays.fill(ans, true);
        for (int i = 0; i < 9; i++) {
            ans[arr[stY][i]] = false;
            ans[arr[i][stX]] = false;
        }

        int pY = stY/3;
        int pX = stX/3;
        for (int i = pY*3; i < pY*3 + 3; i++) {
            for (int j = pX*3; j < pX*3+3; j++) {
                ans[arr[i][j]] = false;
            }
        }

        return ans;
    }


}

```