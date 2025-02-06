```java
package com.one;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.HashSet;
import java.util.Objects;
import java.util.Set;
import java.util.StringTokenizer;

public class Main {
	
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        int startX = 0; 
        int startY = 0;
        
        int M = Integer.parseInt(br.readLine());
        Set<Star> mSet = new HashSet<>();
        for (int i = 0; i < M; i++) {
        	st = new StringTokenizer(br.readLine());
        	int x = Integer.parseInt(st.nextToken());
        	int y = Integer.parseInt(st.nextToken());
        	
        	startX = x;
        	startY = y;
        	mSet.add(Star.of(x, y));
        }
        int N = Integer.parseInt(br.readLine());
        Set<Star> nSet = new HashSet<>();
        for (int i = 0; i < N; i++) {
        	st = new StringTokenizer(br.readLine());
        	int x = Integer.parseInt(st.nextToken());
        	int y = Integer.parseInt(st.nextToken());

        	nSet.add(Star.of(x, y));        
        }
        
        for(Star star: nSet) {
		    int dx = star.x - startX;
		    int dy = star.y - startY;
			if (adjustAndDetermine(mSet , nSet, dx, dy)) {
				System.out.println(dx + " " + dy);
				return;
			}
        }
    }
    
    private static boolean adjustAndDetermine(Set<Star> a, Set<Star> b, int dx, int dy) {
    	for(Star star : a) {
    		star.adjust(dx, dy);
    	}
    	if (determine(a, b)) {
    		return true;
    	}
    	
    	for(Star star : a) {
    		star.recover(dx, dy);
    	}
		return false;
    }
    
    private static boolean determine(Set<Star> a, Set<Star> b) {
        return b.containsAll(a);
    }

    private static class Star {
    	private int x;
    	private int y;
    	
    	private Star(int x, int y) {
    		this.x = x;
    		this.y = y;
    	}
    	
    	public static Star of(int x, int y) {
    		return new Star(x, y);
    	}
    	
    	public void adjust(int dx, int dy) {
    		x+=dx;
    		y+=dy;
    	}
    	public void recover(int dx, int dy) {
    		x-=dx;
    		y-=dy;
    	}

		@Override
		public int hashCode() {
			return Objects.hash(x, y);
		}

		@Override
		public boolean equals(Object obj) {
			if (this == obj)
				return true;
			if (obj == null)
				return false;
			if (getClass() != obj.getClass())
				return false;
			Star other = (Star) obj;
			return x == other.x && y == other.y;
		}
    }
}


```
