```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int G = Integer.parseInt(br.readLine());
		long old = 1;
		long now = 2;
		boolean isFind = false;

		while (now <= 100000 && old < now) {
			long diff = now * now - old * old;
			if (diff == G) {
				System.out.println(now);
				isFind = true;
				old++;
			} else if (diff < G) {
				now++;
			} else {
				old++;
			}
		}

		
		if (!isFind) {
			System.out.println(-1);
		}
	}
}

```
