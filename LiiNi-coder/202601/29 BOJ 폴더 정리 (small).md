```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.HashMap;
import java.util.HashSet;
import java.util.Iterator;
import java.util.List;
import java.util.Map;
import java.util.Set;

public class Main{
	static class Folder{
		String name;
		Set<Folder> folders;
		Set<String> files;
		Map<String, Integer> lowerFileCountAtName;
		Folder(String name){
			this.name = name;
			folders = new HashSet<>();
			files = new HashSet<>();
		}
		void addFolder(Folder target){
			this.folders.add(target);
		}
		void addFile(String fileName){
			this.files.add(fileName);
		}
		Map<String, Integer> getLowerFileCount(){
			if(lowerFileCountAtName == null){
				this.lowerFileCountAtName = new HashMap<>();
				//해당 폴더의 파일 취합
				Iterator<String> iterFile = files.iterator();
				while(iterFile.hasNext()){
					String fileName = iterFile.next();
					lowerFileCountAtName.put(fileName, lowerFileCountAtName.getOrDefault(fileName, 0) + 1);
				}

				//dfs로 가장 안쪽까지 가서 해당 폴더의 lowerFileCountAtName을 구함
				Iterator<Folder> iter = folders.iterator();
				while(iter.hasNext()){
					Folder childFolder = iter.next();
					Map<String, Integer> lfcOfChildFolder = childFolder.getLowerFileCount();
					for(Map.Entry<String, Integer> entry : lfcOfChildFolder.entrySet()){
						lowerFileCountAtName.put(entry.getKey(), lowerFileCountAtName.getOrDefault(entry.getKey(), 0) + entry.getValue());
					}
				}
			}

			return lowerFileCountAtName;
		}
	}
	private static int N, M, Q;
	private static Map<String, Folder> FolderAtName;
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		FolderAtName = new HashMap<>();
		try{
			createFolder("main");
		}catch(NullPointerException e){
			throw new RuntimeException("createFolder 에러");
		}
		String[] tokens = br.readLine().split(" ");
		N = Integer.parseInt(tokens[0]);
		M = Integer.parseInt(tokens[1]);

		for(int i = 0; i<N+M; i++){
			tokens = br.readLine().split(" ");
			String srcName = tokens[0];
			Folder src = FolderAtName.get(srcName);
			if(src == null){
				src = createFolder(srcName);
			}
			String targetName = tokens[1];
			if("1".equals(tokens[2])){
				//폴더
				src.addFolder(createFolder(targetName));
			}else{
				//파일
				src.addFile(targetName);
			}
		}
		Q = Integer.parseInt(br.readLine());
		int q = Q;
		while(q-->0){
			tokens = br.readLine().split("/");
			Folder target = FolderAtName.get(tokens[tokens.length-1]);
			Map<String, Integer> temp = target.getLowerFileCount();
			int answer = 0;
			for(int c : temp.values()){
				answer += c;
			}
			System.out.println(temp.size() + " " + answer);
		}
		br.close();
	}

	private static Folder createFolder(String name) {
		FolderAtName.putIfAbsent(name, new Folder(name));
		return FolderAtName.get(name);
	}
}
```
