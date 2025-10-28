```cpp
#include <bits/stdc++.h>
using namespace std;

class Dice {
	int east, west, south, north, top, bot;
public:
	Dice() {
		top = 0;
		bot = 0;
		east = 0;
		west = 0;
		south = 0;
		north = 0;
	}

	int getTop() { return top; }
	int getBot() { return bot; }
	void setBot(int bot) { this->bot = bot; }

	void right() {
		int newEast = top;
		int newWest = bot;
		int newTop = west;
		int newBot = east;
		east = newEast, west = newWest, top = newTop, bot = newBot;
	}

	void left() {
		int newEast = bot;
		int newWest = top;
		int newTop = east;
		int newBot = west;
		east = newEast, west = newWest, top = newTop, bot = newBot;
	}

	void up() {
		int newTop = south;
		int newBot = north;
		int newSouth = bot;
		int newNorth = top;
		top = newTop, bot = newBot, south = newSouth, north = newNorth;
	}

	void down() {
		int newTop = north;
		int newBot = south;
		int newSouth = top;
		int newNorth = bot;
		top = newTop, bot = newBot, south = newSouth, north = newNorth;
	}

	void command(int num) {
		if (num == 1) right();
		else if (num == 2) left();
		else if (num == 3) up();
		else down();
	}

	// for debug
	void print() {
		cout << "= INFO =\n";
		cout << "========\n";
		cout << "  " << north << '\n';
		cout << west << ' ' << top << ' ' << east << '\n';
		cout << "  " << south << '\n';
		cout << "  " << bot << '\n';
	}
};

int N, M, x, y, K;
int arr[20][20]{};
int dx[5] = { 0,0,0,-1,1 };
int dy[5] = { 0,1,-1,0,0 };

int main() {
	cin.tie(0)->sync_with_stdio(0);

	cin >> N >> M >> x >> y >> K;
	for (int i = 0; i < N; i++) for (int j = 0; j < M; j++) cin >> arr[i][j];

	Dice* dice = new Dice();
	for (int cmd; K--;) {
		cin >> cmd;

		x += dx[cmd], y += dy[cmd];
		if (x < 0 || x >= N || y < 0 || y >= M) {
			x -= dx[cmd], y -= dy[cmd];
			continue;
		}

		dice->command(cmd);
		cout << dice->getTop() << '\n';

		if (arr[x][y] == 0) {
			arr[x][y] = dice->getBot();
		}
		else {
			dice->setBot(arr[x][y]);
			arr[x][y] = 0;
		}

	}

}
```
