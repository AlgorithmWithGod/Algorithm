```cpp

#include <iostream>
#include <vector>
#include <algorithm>
#include <map>
using namespace std;

vector<bool> poss(2000);

struct Node{
    map<int, Node *> next;
    bool last;
    Node(){
        this->last = false;
    }
};

struct Trie{
    Node *root;
    Trie(){
        root = new Node();
    }
    void insert(string &s){
        Node *now = root;
        for(int i=0;i<s.size();i++){
            int idx = s[i] - 'a';
            bool isLast = i==s.size()-1;
            if(!now->next[idx]) now->next[idx] = new Node();
            now = now->next[idx];
        }
        now->last = true;

    }
    bool find(string &s, bool reverse){
        Node *now = root;
        int id = reverse ? s.size() : 0;
        for(int i=0;i<s.size()-1;i++) {
            int idx = s[i] - 'a';
            if(now->next.find(idx) == now->next.end()) return false;
            now = now->next[idx];
            if(reverse) id--;
            else id++;

            if(reverse && poss[id] && now->last) return true;
            poss[id] = now->last;
        }
        return false;
    }
};

int main(){
    cin.tie(0)->sync_with_stdio(0);
    
    Trie *colors = new Trie();
    Trie *names = new Trie();
    int N, M, Q;
    cin>>N>>M;
    for(int i=0;i<N;i++) {
        string s;
        cin>>s;
        colors->insert(s);
    }
    for(int i=0;i<M;i++){
        string s;
        cin>>s;
        reverse(s.begin(), s.end());
        names->insert(s);
    }

    for(cin>>Q;Q--;){
        string s;
        cin>>s;
        poss = vector<bool>(s.size());
        colors->find(s, 0);
        reverse(s.begin(), s.end());
        bool res = names->find(s, 1);
        cout<<(res ? "Yes\n" : "No\n");
    }

}

```
