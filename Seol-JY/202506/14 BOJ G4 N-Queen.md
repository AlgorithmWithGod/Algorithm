```java
import java.io.*;

public class Main {
    private static int N;
    private static int count = 0;
    private static int cols = 0;
    private static int diag1 = 0;
    private static int diag2 = 0;
    
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        
        solve(0);
        System.out.println(count);
    }
    
    private static void solve(int row) {
        if (row == N) {
            count++;
            return;
        }
        
        for (int col = 0; col < N; col++) {
            int colBit = 1 << col;
            int diag1Bit = 1 << (row + col);
            int diag2Bit = 1 << (row - col + N - 1);
            
            if ((cols & colBit) == 0 && (diag1 & diag1Bit) == 0 && (diag2 & diag2Bit) == 0) {
                cols |= colBit;
                diag1 |= diag1Bit;
                diag2 |= diag2Bit;
                
                solve(row + 1);
                
                cols &= ~colBit;
                diag1 &= ~diag1Bit;
                diag2 &= ~diag2Bit;
            }
        }
    }
}
``` 
