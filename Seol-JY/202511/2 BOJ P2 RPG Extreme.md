```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());

        Game game = new Game(N, M);

        for (int i = 0; i < N; i++) {
            String line = br.readLine();
            for (int j = 0; j < M; j++) {
                game.setCell(i, j, line.charAt(j));
            }
        }

        String commands = br.readLine();

        String line;
        while ((line = br.readLine()) != null && !line.isEmpty()) {
            st = new StringTokenizer(line);
            int r = Integer.parseInt(st.nextToken()) - 1;
            int c = Integer.parseInt(st.nextToken()) - 1;
            String third = st.nextToken();
            
            int remainingTokens = st.countTokens();
            
            if (remainingTokens == 4) {
                String name = third;
                int w = Integer.parseInt(st.nextToken());
                int a = Integer.parseInt(st.nextToken());
                int h = Integer.parseInt(st.nextToken());
                int exp = Integer.parseInt(st.nextToken());
                Monster monster = new Monster(name, w, a, h, exp);
                game.setMonster(r, c, monster);
            } else {
                Item item;
                if (third.equals("W")) {
                    int power = Integer.parseInt(st.nextToken());
                    item = new Weapon(power);
                } else if (third.equals("A")) {
                    int defense = Integer.parseInt(st.nextToken());
                    item = new Armor(defense);
                } else {
                    String effect = st.nextToken();
                    item = new Accessory(effect);
                }
                game.setItem(r, c, item);
            }
        }

        game.play(commands);
        System.out.print(game.getResult());
    }

    static class Game {
        private int N, M;
        private char[][] grid;
        private char[][] originalGrid;
        private Player player;
        private int startR, startC;
        private Map<String, Monster> monsters;
        private Map<String, Item> items;
        private int turns;
        private String endReason;
        private String killedBy;

        public Game(int N, int M) {
            this.N = N;
            this.M = M;
            this.grid = new char[N][M];
            this.originalGrid = new char[N][M];
            this.monsters = new HashMap<>();
            this.items = new HashMap<>();
            this.turns = 0;
            this.player = new Player();
        }

        public void play(String commands) {
            for (int i = 0; i < commands.length(); i++) {
                if (!executeCommand(commands.charAt(i))) {
                    break;
                }
            }
        }

        private boolean executeCommand(char command) {
            int dr = 0, dc = 0;
            switch (command) {
                case 'U': dr = -1; break;
                case 'D': dr = 1; break;
                case 'L': dc = -1; break;
                case 'R': dc = 1; break;
            }

            int newR = player.r + dr;
            int newC = player.c + dc;

            if (newR < 0 || newR >= N || newC < 0 || newC >= M || grid[newR][newC] == '#') {
                newR = player.r;
                newC = player.c;
            }

            player.setPosition(newR, newC);
            turns++;

            char cell = grid[newR][newC];
            String key = newR + "," + newC;

            switch (cell) {
                case 'B':
                    Item item = items.get(key);
                    if (item != null) {
                        player.obtainItem(item);
                        grid[newR][newC] = '.';
                    }
                    break;
                case '^':
                    int damage = player.hasAccessory("DX") ? 1 : 5;
                    boolean revived = player.takeDamage(damage, startR, startC);
                    if (player.isDead() && !revived) {
                        endReason = "KILLED";
                        killedBy = "SPIKE TRAP";
                        return false;
                    }
                    break;
                case '&':
                case 'M':
                    Monster monster = monsters.get(key);
                    if (monster != null && monster.isAlive()) {
                        boolean isBoss = (cell == 'M');
                        int fightResult = player.fight(monster, isBoss, startR, startC);

                        if (fightResult == 1) {
                            grid[newR][newC] = '.';
                            if (isBoss) {
                                endReason = "WIN";
                                return false;
                            }
                        } else if (fightResult == -1) {
                            endReason = "KILLED";
                            killedBy = monster.name;
                            return false;
                        }
                    }
                    break;
            }

            return true;
        }

        public void setCell(int r, int c, char ch) {
            grid[r][c] = ch;
            originalGrid[r][c] = ch;
            if (ch == '@') {
                startR = r;
                startC = c;
                player.setPosition(r, c);
                grid[r][c] = '.';
                originalGrid[r][c] = '.';
            }
        }

        public void setMonster(int r, int c, Monster monster) {
            monsters.put(r + "," + c, monster);
        }

        public void setItem(int r, int c, Item item) {
            items.put(r + "," + c, item);
        }

        public String getResult() {
            StringBuilder sb = new StringBuilder();

            for (int i = 0; i < N; i++) {
                for (int j = 0; j < M; j++) {
                    if (player.isAlive() && i == player.r && j == player.c) {
                        sb.append('@');
                    } else {
                        sb.append(grid[i][j]);
                    }
                }
                sb.append('\n');
            }

            sb.append("Passed Turns : ").append(turns).append('\n');

            sb.append("LV : ").append(player.level).append('\n');
            sb.append("HP : ").append(Math.max(0, player.hp)).append('/').append(player.maxHp).append('\n');
            sb.append("ATT : ").append(player.baseAttack).append('+').append(player.weaponPower).append('\n');
            sb.append("DEF : ").append(player.baseDefense).append('+').append(player.armorDefense).append('\n');
            sb.append("EXP : ").append(player.exp).append('/').append(player.level * 5).append('\n');

            if (endReason == null) {
                sb.append("Press any key to continue.\n");
            } else if (endReason.equals("WIN")) {
                sb.append("YOU WIN!\n");
            } else if (endReason.equals("KILLED")) {
                sb.append("YOU HAVE BEEN KILLED BY ").append(killedBy).append("..\n");
            }

            return sb.toString();
        }
    }

    static class Player {
        int r, c;
        int level;
        int hp, maxHp;
        int baseAttack;
        int baseDefense;
        int exp;
        int weaponPower;
        int armorDefense;
        Set<String> accessories;

        public Player() {
            this.level = 1;
            this.hp = 20;
            this.maxHp = 20;
            this.baseAttack = 2;
            this.baseDefense = 2;
            this.exp = 0;
            this.weaponPower = 0;
            this.armorDefense = 0;
            this.accessories = new HashSet<>();
        }

        public void setPosition(int r, int c) {
            this.r = r;
            this.c = c;
        }

        public void obtainItem(Item item) {
            if (item instanceof Weapon) {
                weaponPower = ((Weapon) item).power;
            } else if (item instanceof Armor) {
                armorDefense = ((Armor) item).defense;
            } else if (item instanceof Accessory) {
                String effect = ((Accessory) item).effect;
                if (accessories.size() < 4 && !accessories.contains(effect)) {
                    accessories.add(effect);
                }
            }
        }

        public boolean hasAccessory(String effect) {
            return accessories.contains(effect);
        }

        public int fight(Monster monster, boolean isBoss, int startR, int startC) {
            if (isBoss && hasAccessory("HU")) {
                hp = maxHp;
            }

            boolean firstPlayerAttack = true;
            boolean firstMonsterAttack = true;

            while (true) {
                int attack = (baseAttack + weaponPower);

                if (firstPlayerAttack && hasAccessory("CO")) {
                    if (hasAccessory("DX")) {
                        attack *= 3;
                    } else {
                        attack *= 2;
                    }
                }

                int damage = Math.max(1, attack - monster.defense);
                monster.takeDamage(damage);

                if (!monster.isAlive()) {
                    int earnedExp = monster.exp;
                    if (hasAccessory("EX")) {
                        earnedExp = (int) (earnedExp * 1.2);
                    }
                    gainExp(earnedExp);

                    if (hasAccessory("HR")) {
                        hp = Math.min(maxHp, hp + 3);
                    }

                    return 1;
                }

                firstPlayerAttack = false;

                int monsterDamage;
                if (isBoss && firstMonsterAttack && hasAccessory("HU")) {
                    monsterDamage = 0;
                } else {
                    monsterDamage = Math.max(1, monster.attack - (baseDefense + armorDefense));
                }

                firstMonsterAttack = false;

                hp -= monsterDamage;

                if (hp <= 0) {
                    if (hasAccessory("RE")) {
                        accessories.remove("RE");
                        hp = maxHp;
                        r = startR;
                        c = startC;
                        monster.resetHp();
                        return 0;
                    }
                    return -1;
                }
            }
        }

        public boolean takeDamage(int damage, int startR, int startC) {
            hp -= damage;
            if (hp <= 0 && hasAccessory("RE")) {
                accessories.remove("RE");
                hp = maxHp;
                r = startR;
                c = startC;
                return true;
            }
            return false;
        }

        public void gainExp(int amount) {
            exp += amount;
            int requiredExp = level * 5;
            if (exp >= requiredExp) {
                levelUp();
                exp = 0;
            }
        }

        public void levelUp() {
            level++;
            maxHp += 5;
            baseAttack += 2;
            baseDefense += 2;
            hp = maxHp;
        }

        public boolean isAlive() {
            return hp > 0;
        }

        public boolean isDead() {
            return hp <= 0;
        }
    }

    static class Monster {
        String name;
        int attack;
        int defense;
        int hp;
        int maxHp;
        int exp;

        public Monster(String name, int attack, int defense, int hp, int exp) {
            this.name = name;
            this.attack = attack;
            this.defense = defense;
            this.hp = hp;
            this.maxHp = hp;
            this.exp = exp;
        }

        public void takeDamage(int damage) {
            hp -= damage;
        }

        public void resetHp() {
            hp = maxHp;
        }

        public boolean isAlive() {
            return hp > 0;
        }
    }

    interface Item {
    }

    static class Weapon implements Item {
        int power;

        public Weapon(int power) {
            this.power = power;
        }
    }

    static class Armor implements Item {
        int defense;

        public Armor(int defense) {
            this.defense = defense;
        }
    }

    static class Accessory implements Item {
        String effect;

        public Accessory(String effect) {
            this.effect = effect;
        }
    }
}
```
