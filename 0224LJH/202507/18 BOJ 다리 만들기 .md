```java
import java.awt.*;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;
import java.util.List;

public class Main {

    static StringBuilder sb = new StringBuilder();
    static int target;
    static boolean[] num;

    // 골드바흐의 강한 추측: 2보다 큰 짝수는 항상 두 소수의 합으로 표현할 수 있다.
    // 골드바흐의 약한 추측: 5보다 큰 홀수는 항상 세 소수의 합으로 표현할 수 있다.
    // 8 이상의 짝수는 항상 네 소수의 합으로 표현 가능하다-> 두 소수 + 2 + 2
    // 9 이상의 홀수는 항상 네 소수의 합으로 표현 가능하다.-> 세 소수 + 2
    // 즉 8이상은 항상 표현이 가능하다.
    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        target = Integer.parseInt(br.readLine());
        num = new boolean[target + 1];
        Arrays.fill(num, true);
        num[0] = false;
        num[1] = false;
    }

    private static void process() {
        if (target < 8) {
            sb.append(-1);
            return;
        }

        getPrimes();
        int curNum = target;
        if ( target % 2 == 0){
            sb.append("2 2 ");
            curNum -= 4;
        } else {
            sb.append("2 3 ");
            curNum -= 5;
        }

        for (int i = 2; i <= curNum/2; i++) {
            if (num[i] && num[ curNum - i]) {
                sb.append(i).append(" ").append(curNum-i);
                return;
            }
        }
    }

    private static void getPrimes() {
        for (int i = 2; i * i <= target; i++) {
            if (num[i]) {
                int temp = i*2;
                while ( temp <= target ) {
                    num[temp] = false;
                    temp += i;
                }
            }

        }
    }


    private static void print()  {
        System.out.println(sb.toString());
    }



}


```