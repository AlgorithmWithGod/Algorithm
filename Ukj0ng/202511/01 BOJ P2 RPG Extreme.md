```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final String WIN = "YOU WIN!";
    private static final String DEAD = "YOU HAVE BEEN KILLED BY ";
    private static final String SPIKE = "SPIKE TRAP";
    private static final String FININPUT = "Press any key to continue.";
    private static final int TRAPDAMAGE = 5;
    private static final int LOWWERTRAPDAMAGE = 1;
    private static int[] dx = {0, 0, -1, 1};
    private static int[] dy = {-1, 1, 0, 0};
    private static Player player;
    private static int[] startPos, bossPos;
    private static Map<String, Monster> monsters;
    private static Map<String, Item> items;
    private static char[][] map;
    private static char[] command;
    private static String dyingMessage;
    private static int N, M;
    private static int finished;

    public static void main(String[] args) throws IOException {
        init();
        int turns = play();
        if (finished == 0) {
            dyingMessage = WIN;
            map[player.x][player.y] = '@';
        }
        else if (finished == 2) {
            dyingMessage = FININPUT;
            map[player.x][player.y] = '@';
        }

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                bw.write(map[i][j]);
            }
            bw.write("\n");
        }

        bw.write("Passed Turns : " + turns + "\n");
        bw.write("LV : " + player.lv + "\n");
        bw.write("HP : " + player.hp + "/" + player.maxHp + "\n");
        bw.write("ATT : " + player.baseW + "+" + player.weapon + "\n");
        bw.write("DEF : " + player.baseA + "+" + player.armor + "\n");
        bw.write("EXP : " + player.exp + "/" + (player.lv*5) + "\n");
        bw.write(dyingMessage + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        finished = -1;
        startPos = new int[2];
        bossPos = new int[2];
        int K = 0;
        int L = 0;

        map = new char[N][M];
        monsters = new HashMap<>();
        items = new HashMap<>();

        for (int i = 0; i < N; i++) {
            map[i] = br.readLine().toCharArray();
            for (int j = 0; j < M; j++) {
                if (map[i][j] == '@') {
                    map[i][j] = '.';
                    player = new Player(i, j);
                    startPos[0] = i;
                    startPos[1] = j;
                } else if (map[i][j] == '&' || map[i][j] == 'M') {
                    K++;
                    if (map[i][j] == 'M') {
                        bossPos[0] = i;
                        bossPos[1] = j;
                    }
                } else if (map[i][j] == 'B') {
                    L++;
                }
            }
        }

        command = br.readLine().toCharArray();

        for (int i = 1; i <= K; i++) {
            st = new StringTokenizer(br.readLine());
            int R = Integer.parseInt(st.nextToken())-1;
            int C = Integer.parseInt(st.nextToken())-1;
            String S = st.nextToken();
            int W = Integer.parseInt(st.nextToken());
            int A = Integer.parseInt(st.nextToken());
            int H = Integer.parseInt(st.nextToken());
            int E = Integer.parseInt(st.nextToken());

            if (map[R][C] == 'M') monsters.put(R+","+C, new Monster(S, 'M', W, A, H, E));
            else monsters.put(R+","+C, new Monster(S, '&', W, A, H, E));
        }

        for (int i = 0; i < L; i++) {
            st = new StringTokenizer(br.readLine());
            int R = Integer.parseInt(st.nextToken())-1;
            int C = Integer.parseInt(st.nextToken())-1;
            char T = st.nextToken().charAt(0);

            if (T == 'O') items.put(R+","+C, new Item(T, st.nextToken()));
            else items.put(R+","+C, new Item(T, Integer.parseInt(st.nextToken())));
        }
    }

    private static int play() {
        int turns = 0;
        for (int i = 0; i < command.length; i++) {
            int d = dir(command[i]);
            int nx = player.x + dx[d];
            int ny = player.y + dy[d];

            if (OOB(nx, ny) || map[nx][ny] == '#') {
                nx = player.x;
                ny = player.y;
            }

            turn(nx, ny);
            turns++;
            if (checkFin()) break;
        }

        if (finished == -1) finished = 2;
        return turns;
    }

    private static boolean checkFin() {
        if (finished > -1) return true;
        return false;
    }

    private static void turn(int nx, int ny) {
        move(nx, ny);

        if (map[nx][ny] == 'B') {
            getO(nx, ny);
        } else if (map[nx][ny] == '^') {
            onTrap();
            if (player.hp <= 0) {
                if (player.oSet.contains("RE")) {
                    player.oSet.remove("RE");
                    player.revive();
                } else {
                    finished = 1;
                    dyingMessage = DEAD + SPIKE+ "..";
                }
            }
        } else if (map[nx][ny] == '&') {
            battle(nx, ny);
            if (player.hp <= 0) {
                if (player.oSet.contains("RE")) {
                    player.oSet.remove("RE");
                    player.revive();
                    monsters.get(nx+","+ny).maxHeal();
                } else {
                    finished = 1;
                    player.hp = 0;
                    dyingMessage = DEAD + monsters.get(nx+","+ny).name + "..";
                }
            }
        } else if (map[nx][ny] == 'M'){
            battle(nx, ny);
            if (player.hp > 0) finished = 0;
            else {
                if (player.oSet.contains("RE")) {
                    player.oSet.remove("RE");
                    player.revive();
                    monsters.get(nx+","+ny).maxHeal();
                } else {
                    finished = 1;
                    player.hp = 0;
                    dyingMessage = DEAD + monsters.get(nx+","+ny).name+ "..";
                }
            }
        }
    }

    private static void getO(int nx, int ny) {
        map[nx][ny] = '.';
        Item item = items.get(nx+","+ny);

        if (item.type == 'W') {
            player.weapon = item.value;
        } else if (item.type == 'A') {
            player.armor = item.value;
        } else {
            if (player.oSet.size() >= 4 || player.oSet.contains(item.name)) return;
            player.oSet.add(item.name);
        }
    }

    // 난 무조건 이동시키고 배틀, 문제에선 배틀에서 이기면 이동
    private static void battle(int nx, int ny) {
        Monster monster = monsters.get(nx+","+ny);
        if (monster.role == 'M' && player.oSet.contains("HU")) {
            player.maxHeal();
        }
        int playerOff = player.baseW + player.weapon;
        int enhanceOff = player.baseW + player.weapon;
        if (player.oSet.contains("CO")) {
            if (player.oSet.contains("DX")) {
                enhanceOff *= 3;
            } else {
                enhanceOff *= 2;
            }
        }
        int playerDef = player.baseA + player.armor;
        int count = 0;

        while (true) {
            int playerDamage = 0;
            if (count == 0) playerDamage = Math.max(1, enhanceOff-monster.baseA);
            else playerDamage = Math.max(1, playerOff-monster.baseA);
            monster.hp -= playerDamage;
            if (monster.hp <= 0) break;
            int monsterDamage = 0;
            if (!(monster.role == 'M' && player.oSet.contains("HU") && count == 0)) {
                monsterDamage = Math.max(1, monster.baseW-playerDef);
            }
            player.hp -= monsterDamage;
            if (player.hp <= 0) break;
            count++;
        }

        if (player.hp > 0) {
            player.exp += calExp(monster.exp);
            if (player.oSet.contains("HR")) player.hp = Math.min(player.hp+3, player.maxHp);
            if (player.exp >= player.lv*5) {
                player.levelUp();
            }
            map[nx][ny] = '.';
        }
    }

    private static int calExp(int exp) {
        if (player.oSet.contains("EX")) return (int)(exp*(1.2));
        return exp;
    }
    private static void onTrap() {
        if (player.oSet.contains("DX")) player.hp -= LOWWERTRAPDAMAGE;
        else player.hp -= TRAPDAMAGE;
    }

    private static void move(int nx, int ny) {
        player.x = nx;
        player.y = ny;
    }

    private static boolean OOB(int nx, int ny) {
        return nx < 0 || nx > N-1 || ny < 0 || ny > M-1;
    }

    private static int dir(char d) {
        if (d == 'L') return 0;
        if (d == 'R') return 1;
        if (d == 'U') return 2;
        return 3;
    }

    static abstract class Living {
        protected int baseW;
        protected int baseA;
        protected int maxHp;
        protected int hp;
        protected int exp;

        public Living(int w, int a, int h, int e) {
            baseW = w;
            baseA = a;
            maxHp = h;
            hp = h;
            exp = e;
        }

        public Living() {
        }

        public void maxHeal() {
            this.hp = this.maxHp;
        }
    }

    static class Player extends Living {
        int x;
        int y;
        int lv;
        int weapon;
        int armor;
        Set<String> oSet;

        public Player(int x, int y) {
            this.x = x;
            this.y = y;
            this.baseW = 2;
            this.baseA = 2;
            this.maxHp = 20;
            this.hp = 20;
            this.lv = 1;
            this.weapon = 0;
            this.armor = 0;
            this.oSet = new HashSet<>();
            this.exp = 0;
        }

        public void levelUp() {
            this.lv++;
            this.exp = 0;
            this.maxHp += 5;
            this.hp = this.maxHp;
            this.baseW += 2;
            this.baseA += 2;
        }

        public void revive() {
            this.hp = this.maxHp;
            this.x = startPos[0];
            this.y = startPos[1];
        }
    }

    static class Monster extends Living {
        String name;
        char role;

        public Monster(String name, char role, int w, int a, int h, int e) {
            super(w, a, h, e);
            this.name = name;
            this.role = role;
        }
    }

    static class Item {
        char type;
        int value;
        String name;

        public Item(char type, String name) {
            this.type = type;
            this.name = name;
        }

        public Item(char type, int value) {
            this.type = type;
            this.value = value;
        }
    }
}
```
