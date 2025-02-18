```java
import java.io.*;
import java.util.*;
import java.math.BigInteger;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder input = new StringBuilder(br.readLine());
        int n = input.length();

        // target은 input + 1부터 시작한다.
        BigInteger addOne = new BigInteger(input.toString()).add(BigInteger.ONE);
        StringBuilder target = new StringBuilder(addOne.toString());

        // 팰린드롬 만들기
        makePalindrome(target);

        // input보다 큰 팰린드롬이 만들어지지 않은 경우
        // mid를 기준으로 앞부분을 자르고, +1을 수행해 앞부분을 증가시켜본다.
        BigInteger inputBigInt = new BigInteger(String.valueOf(input));
        BigInteger targetBigInt = new BigInteger(String.valueOf(target));
        if (inputBigInt.compareTo(targetBigInt) >= 0) {
            int mid;
            if (n % 2 == 0) {
                mid = n/2;
            } else {
                mid = n/2 + 1;
            }

            String head = target.substring(0, mid);
            String newHead = new BigInteger(head).add(BigInteger.ONE).toString();
            
            for (int i = 0; i < mid; i++) {
                target.setCharAt(i, newHead.charAt(i));
            }
            // 앞부분을 증가시킨 target으로 다시 팰린드롬을 만든다.
            makePalindrome(target);
        }
        System.out.println(target.toString());
        br.close();
    }

    private static void makePalindrome(StringBuilder target) {
        int n = target.length();
        int mid;
        if (n % 2 == 0) {
            mid = n/2;
        } else {
            mid = n/2 + 1;
        }
        // mid를 기준으로 뒤에 있는 숫자들을 앞에 있는 숫자들에 맞춘다.
        for ( int i = 0; i < mid ; i++ ) {
            if (target.charAt(i) == target.charAt(n-1-i)) { continue; }
            target.setCharAt(n-1-i, target.charAt(i));
        }
    }
}
```
