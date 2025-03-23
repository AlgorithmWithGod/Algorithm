```java
package com.one;
import java.io.BufferedReader;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
	private static final int[] dx = {-1, 0, 1, 1};
	private static final int[] dy = {1, 1, 1, 0};
	
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int map[][] = new int[20][20];
        for (int i = 1; i <= 19; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= 19; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        for (int i = 1; i <= 19; i++) {
            for (int j = 1; j <= 19; j++) {
        		int target = map[i][j];
        		
                for (int k = 0; k < 4; k++) {
                	int cnt1 = 0;
                	int cnt2 = 0;
                	for (int m = 0; m < 5; m++) {
                		int nx = i + dx[k]*m;
                		int ny = j + dy[k]*m;
                		
                		if (canMove(nx, ny)) {
                			if (map[nx][ny] == 1 && target == 1) {cnt1++;}
                			if (map[nx][ny] == 2 && target == 2) {cnt2++;}
                		}
                	}

                	if (cnt1 == 5) {
                		int nx = i - dx[k];
                		int ny = j - dy[k];
                		if (canMove(nx, ny) && map[nx][ny] == 1) continue;
                		nx = i + dx[k]*5;
                		ny = j + dy[k]*5;
                		if (canMove(nx, ny) && map[nx][ny] == 1) continue;
                		System.out.println(1);
                		System.out.println(i + " " + j);
                		return;
                	}
                	if (cnt2 == 5) {
                		int nx = i - dx[k];
                		int ny = j - dy[k];
                		if (canMove(nx, ny) && map[nx][ny] == 2) continue;
                		nx = i + dx[k]*5;
                		ny = j + dy[k]*5;
                		if (canMove(nx, ny) && map[nx][ny] == 2) continue;
                		System.out.println(2);
                		System.out.println(i + " " + j);
                		return;
                	}
                }
            }
        }
        System.out.println(0);
    }


    private static boolean canMove(int x, int y) {
	    if (x < 1 || y < 1 || x > 19 || y > 19) {
	        return false;
	    }
    	return true;
	}
}


```
