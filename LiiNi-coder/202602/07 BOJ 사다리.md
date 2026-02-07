```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main{
	private static double X, Y, C;

	public static void main(String[] args) throws IOException{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		String[] t = br.readLine().split(" ");
		X = Double.parseDouble(t[0]);
		Y = Double.parseDouble(t[1]);
		C = Double.parseDouble(t[2]);
		double l = 0; // check(l) = true
		double r = Math.min(X, Y); // check(r) = false
		for(int i=0; i<100; i++){ //l, r 이 실수면 그냥 100번정도 하면 오차 내로 수렴하는 방식
			double mid = (l + r) / 2.0;
			if(check(mid)){
				l = mid;
			}else{
				r = mid;
			}
		}

		System.out.printf("%.3f\n", l);
	}

	private static boolean check(double w){
		double h1 = Math.sqrt(X * X - w*w);
		double h2 = Math.sqrt(Y * Y - w*w);
		double cross = (h1 * h2) / (h1 + h2);
		return cross >= C;
	}
}

```
