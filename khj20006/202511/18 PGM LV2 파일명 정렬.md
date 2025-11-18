```cpp
#include <bits/stdc++.h>
using namespace std;

class CustomString {
public:
	string str, head;
	int number, order;
	CustomString(string a, int ord) {
		this->str = a;
		this->order = ord;
		int idx = 0;
		this->head = "";
		string num = "";
		while (idx < a.size()) {
			if ('0' <= a[idx] && a[idx] <= '9') {
				num += a[idx];
			}
			else {
				if (!num.empty()) break;
				if ('A' <= a[idx] && a[idx] <= 'Z') head += (char)(a[idx] + 32);
				else head += a[idx];
			}
			idx++;
		}
		this->number = stoi(num);
	}
};


vector<string> solution(vector<string> files) {
	vector<CustomString*> customFiles;
	int ord = 0;
	for (string file : files) {
		customFiles.push_back(new CustomString(file, ++ord));
	}

	sort(customFiles.begin(), customFiles.end(), [](CustomString* a, CustomString* b) -> bool {
		if (a->head != b->head) return a->head < b->head;
		if (a->number != b->number) return a->number < b->number;
		return a->order < b->order;
	});

	vector<string> answer;
	for (CustomString* cs : customFiles) {
		answer.push_back(cs->str);
	}
	
	return answer;
}
```
