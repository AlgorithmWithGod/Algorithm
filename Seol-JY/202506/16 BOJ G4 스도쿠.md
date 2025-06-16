```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

class Main {
    private static int[] horizontalBit = new int[9];
    private static int[] verticalBit = new int[9];
    private static int[] sectionBit = new int[9];
    
    private static int[][] map = new int[9][9];
    
    private static int[] emptyRows = new int[81];
    private static int[] emptyCols = new int[81];
    private static int emptyCount = 0;
    
    private static StringBuilder result = new StringBuilder();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        for (int i = 0; i < 9; i++) {
            String line = br.readLine();
            for (int j = 0; j < 9; j++) {
                int num = line.charAt(j) - '0';
                map[i][j] = num;

                if (num == 0) {
                    emptyRows[emptyCount] = i;
                    emptyCols[emptyCount] = j;
                    emptyCount++;
                    continue;
                }

                int bitMask = 1 << (num - 1);
                horizontalBit[i] |= bitMask;
                verticalBit[j] |= bitMask;
                sectionBit[getSectionNumber(i, j)] |= bitMask;
            }
        }
        
        solve(0);
        
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                result.append(map[i][j]);
            }
            result.append('\n');
        }
        System.out.print(result);
    }

    private static boolean solve(int index) {
        if (index == emptyCount) {
            return true;
        }

        int row = emptyRows[index];
        int col = emptyCols[index];
        int sectionNum = getSectionNumber(row, col);
        
        int usedBits = horizontalBit[row] | verticalBit[col] | sectionBit[sectionNum];
        
        for (int num = 1; num <= 9; num++) {
            int bitMask = 1 << (num - 1);
            
            if ((usedBits & bitMask) == 0) {
                map[row][col] = num;
                horizontalBit[row] |= bitMask;
                verticalBit[col] |= bitMask;
                sectionBit[sectionNum] |= bitMask;
                
                if (solve(index + 1)) {
                    return true;
                }
                
                map[row][col] = 0;
                horizontalBit[row] &= ~bitMask;
                verticalBit[col] &= ~bitMask;
                sectionBit[sectionNum] &= ~bitMask;
            }
        }
        
        return false;
    }

    private static int getSectionNumber(int row, int col) {
        return (row / 3) * 3 + (col / 3);
    }
}
```
