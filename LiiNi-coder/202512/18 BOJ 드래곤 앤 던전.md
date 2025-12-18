```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;
/*
1 3 100 -> 천장(100/현 용사의 공격력)번을 공격해야 몬스터가 죽는다.
현 용사의 공격력이 10이면 10번때려야 몬스터가 죽는다. -> 따라서 용사는 몬스터공격력 * (10-1)공격을 견뎌야한다.
-> 이때 해당 용사의 현재체력이 최소 몬스터공격력 * 9 + 1 이어야함.
현 용사의 공격력이 6이라면 천장(100/6) 17 때려야 몬스터가 죽는다. -> 따라서 용사는 몬스터공격력 * (17 - 1) 공격을 견뎌야한다.
-> 이때 해당 용사의 현재체력이 최소 몬스터공격력 * 16 + 1 이어야함.
 */
public class Main{
	private static int N;
	private static int InitialAttack;

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		ArrayList<int[]> MonsterRooms = new ArrayList<>();
		// [0]: 해당 방에서의 현 공격력
		// [1]: 해당 방 몬스터의 공격력
		// [2]: 해당 방 몬스터의 초기체력
		// [3]: 해당 방까지 입장하였을때 회복한 체력의 총수
		String[] temp = br.readLine().split(" ");
		N = Integer.parseInt(temp[0]);
		InitialAttack = Integer.parseInt(temp[1]);
		int attack = InitialAttack;
		int diffHp = 0;
		for(int i = 0; i < N; i++){
			temp = br.readLine().split(" ");
			switch(temp[0] ){
				case "1" ->{
					MonsterRooms.add(new int[]{attack, Integer.parseInt(temp[1]), Integer.parseInt(temp[2]), diffHp});
					diffHp = 0;
				}
				case "2" ->{
					diffHp += Integer.parseInt(temp[2]);
					attack += Integer.parseInt(temp[1]);
				}
			}
		}

		int mustEndMinHp = 0; // 다음 방을 클리어하기위해 현재 방에서 반드시 끝마칠때 최소 이 hp는 넘어야함
		for(int i = MonsterRooms.size() - 1; i>=0; i--){
			int[] m = MonsterRooms.get(i);
			int attack = m[0];
			int monsterAttack = m[1];
			int initialMonsterHp = m[2];
			int healedHp = m[3];

			int mustAttackCount = (int)Math.ceil(initialMonsterHp / (double)attack);
			int minHp = (mustAttackCount - 1) * monsterAttack + 1;//해당 방을 클리어하기 위해 필요한 최소 hp
			mustEndMinHp = minHp - healedHp;
		}
		br.close();
	}
}
/*
1 1 20 에 mustEndMinHp 가 39여야함. -> 몬스터를 잡고나서 남은 체력이 반드시 39이상이어야한다는뜻
몬스터를 7번때려야함.따라서 용사는 6번 공격을 버텨야하고, 몬스터공격력 * 6의 총 데미지를 받음.
따라서 초기 체력이 mustEndMinHp + 1*6 = 45여야함.
 */
```
