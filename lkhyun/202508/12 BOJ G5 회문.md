```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        int T = Integer.parseInt(br.readLine());
        
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < T; i++) {
            String str = br.readLine();
            sb.append(checkPalindrome(str)).append('\n');
        }
        
        bw.write(sb.toString());
        bw.close();
    }
    private static boolean isPalindrome(String str, int start, int end) {
        while (start < end) {
            if (str.charAt(start) != str.charAt(end)) {
                return false;
            }
            start++;
            end--;
        }
        return true;
    }
    
    private static int checkPalindrome(String str) {
        int left = 0;
        int right = str.length() - 1;
        
        while (left < right) {
            if (str.charAt(left) == str.charAt(right)) {
                left++;
                right--;
            } else {
                if (isPalindrome(str, left + 1, right) || isPalindrome(str, left, right - 1)) {
                    return 1;
                } else {
                    return 2;
                }
            }
        }
        return 0;
    }
}
```
