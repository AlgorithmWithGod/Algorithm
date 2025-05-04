```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,M;
    static boolean[] knowingPeople;

    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        st = new StringTokenizer(br.readLine());
        int temp = Integer.parseInt(st.nextToken());
        knowingPeople = new boolean[N+1];
        for (int i = 0; i < temp; i++) {
            knowingPeople[Integer.parseInt(st.nextToken())] = true;
        }

        List<List<Integer>> party = new ArrayList<>();
        for (int i = 0; i < M; i++) {
            List<Integer> l = new ArrayList<>();
            st = new StringTokenizer(br.readLine());
            int num = Integer.parseInt(st.nextToken());
            for (int j = 0; j < num; j++) {
                int people = Integer.parseInt(st.nextToken());
                l.add(people);
            }
            party.add(l);
        }


        int prev;
        int curr = party.size();
        do{
            prev = curr;
            curr = 0;
            
            for (int i = 0; i < party.size(); i++) {
                boolean found = false;
                for (int j = 0; j < party.get(i).size(); j++) {
                    if(knowingPeople[party.get(i).get(j)]){
                        found = true;
                        break;
                    }
                }
                if(found){
                    for (int j = 0; j < party.get(i).size(); j++) {
                        knowingPeople[party.get(i).get(j)] = true;
                    }
                    party.remove(i--);
                }else{
                    curr++;
                }
            }
        }while(!party.isEmpty() && prev != curr);

        bw.write(curr + "");
        bw.close();
    }
}
```
