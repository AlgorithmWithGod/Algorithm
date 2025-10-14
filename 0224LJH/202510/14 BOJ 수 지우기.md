```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
	
	static int len;
	static int[] arr,numCnt,eraseCnt;
	static String ans;
    
    public static void main(String[] args) throws IOException {
    	init();
    	process();
    	print();
    }
    private static void init() throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        String input = br.readLine();
        len = input.length();
        arr = new int[len];
        
        numCnt = new int[10];
        for (int i = 0; i < len; i++) {
            arr[i] = input.charAt(i) - '0';
            numCnt[arr[i]]++;
        }
        
        String erase = br.readLine();
        eraseCnt = new int[10];
        for (int i = 0; i < erase.length(); i++) {
            eraseCnt[erase.charAt(i) - '0']++;
        }
    }
    
    private static void process() {        
        // 남을 숫자 개수
        int[] remaining = new int[10];
        int totalRemain = 0;
        for (int i = 0; i < 10; i++) {
            remaining[i] = numCnt[i] - eraseCnt[i];
            totalRemain += remaining[i];
        }
        
        // suffix count 전처리
        int[][] suffixCnt = new int[len + 1][10];
        for (int i = len - 1; i >= 0; i--) {
            for (int d = 0; d < 10; d++) {
                suffixCnt[i][d] = suffixCnt[i + 1][d];
            }
            suffixCnt[i][arr[i]]++;
        }
        
        StringBuilder sb = new StringBuilder();
        int pos = 0;
        
        // 결과 길이만큼 반복
        for (int resultPos = 0; resultPos < totalRemain; resultPos++) {
            // 가장 큰 숫자부터 시도
            for (int num = 9; num >= 0; num--) {
                if (remaining[num] == 0) continue;
                
                // 원본에서 num을 찾기
                boolean found = false;
                for (int i = pos; i < len; i++) {
                    if (arr[i] == num) {
                        // 이 num을 선택했을 때, i+1부터 나머지를 만들 수 있는지 확인
                        remaining[num]--;
                        
                        boolean canMake = true;
                        for (int d = 0; d < 10; d++) {
                            if (suffixCnt[i + 1][d] < remaining[d]) {
                                canMake = false;
                                break;
                            }
                        }
                        
                        if (canMake) {
                            sb.append(num);
                            pos = i + 1;
                            found = true;
                            break;
                        } else {
                            remaining[num]++;
                        }
                    }
                }
                
                if (found) break;
            }
        }
        
        ans = sb.toString();
    }
    

    
    private static void print() {
        System.out.println(ans);
    }
}
```
