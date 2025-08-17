```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static ArrayDeque<Integer> deq = new ArrayDeque<>();
    static int state = 0; //0: 뒤 앞, 1: 앞이 하늘, 2: 앞 뒤, 3: 앞이 아래
    static int ballCnt = 0;
    static int wallCnt = 0;

    public static void main(String[] args) throws IOException {
        int Q = Integer.parseInt(br.readLine());
        

        for (int i = 0; i < Q; i++) {
            st = new StringTokenizer(br.readLine());
            String a = st.nextToken();

            if(a.equals("push")){
                String b = st.nextToken();
                if(b.equals("b")){
                    deq.offer(1);
                    ballCnt++;
                    ballFlush();
                }else if(b.equals("w")){
                    deq.offer(-1);
                    wallCnt++;
                }

            }else if(a.equals("pop")){
                if(!deq.isEmpty()){
                    if(deq.poll() == 1){
                        ballCnt--;
                    }else{
                        wallCnt--;
                    }
                }
                ballFlush();
            }else if(a.equals("rotate")){
                String b = st.nextToken();
                if(b.equals("l")){
                    state = (state+1) % 4;
                }else if(b.equals("r")){
                    state = (state+3) % 4;
                }
                ballFlush();
            }else if(a.equals("count")){
                String b = st.nextToken();
                if(b.equals("b")){
                    bw.write(ballCnt+"\n");
                }else if(b.equals("w")){
                    bw.write(wallCnt+"\n");
                }
            }
        }
        bw.close();
    }
    static void ballFlush(){
        if(state == 1){
            while(!deq.isEmpty() && deq.peekLast() == 1){
                deq.pollLast();
                ballCnt--;
            }
        }else if(state == 3){
            while(!deq.isEmpty() && deq.peek() == 1){
                deq.poll();
                ballCnt--;
            }
        }
    }
}
```
