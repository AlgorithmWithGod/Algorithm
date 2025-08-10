```java
import java.awt.*;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;
import java.util.List;


public class Main {
    static String target,goal;

    static int size,ans;
    static int[] arr;

    static List<Character> list = new ArrayList<>();

    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        target = br.readLine();
        goal = br.readLine();
        ans = 0;
    }

    private static void process() throws IOException {

        int goalIdx = goal.length()-1;

        for (int i = target.length()-1; i >= 0; i--) {
            if (target.charAt(i) == goal.charAt(goalIdx)) {
                goalIdx--;
            } else {
                list.add(target.charAt(i));
                ans++;
            }
        }

        if (goalIdx == -1) return;

        Outer:
        while (goalIdx >= 0) {
            for (int i = 0; i < list.size(); i++) {
                Character c = list.get(i);
                if (c==goal.charAt(goalIdx)) {
                    goalIdx--;
                    list.remove(i);
                    continue Outer;
                }
            }

            goalIdx--;

        }

        if (list.size() != 0) ans = -1;

    }


    private static void print() {
        System.out.println(ans);
    }
}
```