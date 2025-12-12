import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine().trim());

        int[] arr = new int[n];
        StringTokenizer st = new StringTokenizer(br.readLine());

        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        // LIS using binary search
        ArrayList<Integer> lis = new ArrayList<>();

        for (int a : arr) {
            int pos = Collections.binarySearch(lis, a);
            if (pos < 0) pos = -(pos + 1);

            if (pos == lis.size()) {
                lis.add(a);
            } else {
                lis.set(pos, a);
            }
        }

        System.out.println(n - lis.size());
    }
}
