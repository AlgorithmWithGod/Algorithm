```java
import java.io.*;
import java.util.*;

public class Main {
	private static int N;
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        N = Integer.parseInt(br.readLine());
       
        File root = File.from("root");
        for (int i = 0; i < N; i++) {
        	root.add(br.readLine().split("\\\\"));
        }
        
        root.printTree();
    }
    
    private static class File implements Comparable<File> {
    	private final String name;
    	private final Set<File> files;
    	
    	private File(String name) {
    		this.name = name;
    		files = new TreeSet<>();
    	}
    	
    	public static File from(String name) {
    		return new File(name);
    	}
    	
    	public void add(String[] names) {
    		add(names, 0);
    	}
    	
    	public void add(String[] names, int index) {
    		if (names.length == index) return;
    		String name = names[index];
    		files.add(File.from(name));
    		
    		for (File file : files) {
    			if (file.isSameName(name)) {
    				file.add(names, index + 1);
    			}
    		}
    	}

    	public boolean isSameName(String name) {
    		return this.name.equals(name);
    	}
    	
    	public Set<File> getFiles() {
    		return files;
    	}
    	

    	public void printTree() {
    		printTree(0);
    	}
    		
    	public void printTree(int tabCount) {
    		if (files.isEmpty()) {
    			return;
    		}
    		
    		for (File file : files) {
    			for (int i = 0; i < tabCount; i++) {
        			System.out.print(" ");
    			}
    			System.out.println(file);
    			
    			file.printTree(tabCount + 1);
    		}
    	}
    	
    	@Override
    	public String toString() {
    		return name;
    	}
    	
    	// 파일이름에 대해서만
		@Override
		public int hashCode() {
			return Objects.hash(name);
		}

		@Override
		public boolean equals(Object obj) {
			if (this == obj)
				return true;
			if (obj == null)
				return false;
			if (getClass() != obj.getClass())
				return false;
			File other = (File) obj;
			return Objects.equals(name, other.name);
		}

		@Override
		public int compareTo(File o) {
			return this.name.compareTo(o.toString());
		}
    }
}


```
