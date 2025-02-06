```java
import java.util.*;
import java.io.*;

public class Main {

    static int N;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        char[] A = br.readLine().toCharArray();
        char[] B = br.readLine().toCharArray();
        N = A.length;

        if (isValidOperation(A, B)) {
            int cnt = 0;
            int aPtr = N-1;
            int bPtr = N-1;

            // 뒤에서부터 확인
            while (0 <= aPtr && 0 <= bPtr) {
                if (A[aPtr] == B[bPtr]) {
                    bPtr--;
                } else {
                    cnt++;
                }
                aPtr--;
            }
            bw.write(cnt + "\n");
        } else {
            bw.write(-1 + "\n");
        }

        br.close();
        bw.flush();
        bw.close();
    }

    private static boolean isValidOperation(char[] current, char[] target) {
        // current, target의 글자 수가 같지 않으면 불가능
        int[] cnt = new int['Z' - 'A' + 1];
        for (int i = 0; i < N; i++) {
            cnt[current[i] - 'A'] += 1;
            cnt[target[i] - 'A'] -= 1;
        }
        // cnt[i]가 0이 아닌 것이 하나라도 있다면 불가능
        for (int i = 0; i < 'Z' - 'A' + 1; i++) {
            if (cnt[i] != 0) return false;
        }
        return true;
    }
}

```

- 머리가 안돌아가서 구글링했다 😥

- A를 B로 바꿀 수 없는 경우를 판단하는 것은 쉽다.

- 모든 문자를 바꿔보지 않아도 된다.

- A와 B의 포인터를 뒤에서부터 설정해주고 일치 여부를 확인한다.
    - `A[A포인터] == B[B포인터]`라면 일치하므로 연산을 수행하지 않고 넘어간다.
        - `A포인터--`, `B포인터--` 수행
    - `A[A포인터] != B[B포인터]`라면 `A포인터` 자리에 있던 문자를 현재 자리에서 치워줘야 B 문자와 가까워지겠다. 연산을 수행한다.
        - `A포인터--` 수행
        - `B포인터`는 그대로 두고, 다음에 `A포인터`가 가리킬 문자는 일치하기를 바란다. 두근두근~

- 예제 입력 5를 에시로 들자면 아래와 같은 동작을 하며 최소 연산 횟수를 구한다.
    > <span style="color:red">(빨간 괄호)</span>로 표시된 부분은 연산을 수 시 앞으로 오게 되는 문자를 나타낸 것인데, 문제 풀이 시 실제로 앞으로 옮겨주는 동작은 안해도 된다. 이해를 위한 표현임.<br>
    중요한 건 최소 연산 횟수를 구하는 것.
    - 동작 1: 연산횟수 0
        - A: DCAB**A** `일치`
        - B: DACB**A**
    - 동작 2: 연산횟수 0
        - A: DCA**B** `일치`
        - B: DAC**B**
    - 동작 3: 연산횟수 <span style="color:red">1</span>
        - A: DC**A** `불일치` -> <span style="color:red">(A)</span>DC
        - B: DA**C**
    - 동작 4: 연산횟수 1
        - A: <span style="color:red">(A)</span>D**C** `일치`
        - B: DA**C**
    - 동작 5: 연산횟수 <span style="color:red">2</span>
        - A: <span style="color:red">(A)</span>**D** `불일치`-> <span style="color:red">(DA)</span>
        - B: D**A**
    - A 포인터가 더는 움직일 곳이 없으므로 종료!