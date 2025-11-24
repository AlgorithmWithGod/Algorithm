```cpp
#include <bits/stdc++.h>
using namespace std;

class Node {
    public:
    int cnt;
    Node *left, *right; // left = 1, right = 0
    
    Node() {
        cnt = 0;
        left = nullptr;
        right = nullptr;
    }
};

class Trie {
    Node *root;

    public:
    Trie() {
        root = new Node();
    }

    void insert(int x) {
        Node *now = root;
        for(int dep=25;--dep>=0;) {
            int bit = x & (1<<dep);
            if(bit) {
                if(now->left == nullptr) now->left = new Node();
                now = now->left;
            }
            else {
                if(now->right == nullptr) now->right = new Node();
                now = now->right;
            }
            now->cnt++;
        }
    }

    int find(int x, int tar) {
        int ret = 0;
        Node *now = root;
        for(int dep=25;--dep>=0;) {
            int bit = x & (1<<dep) ? 1 : 0;
            int need = bit ^ tar;
            int res = 0;
            if(need) {
                if(now->left == nullptr) now = now->right;
                else now = now->left, res = (1<<dep);
            }
            else {
                if(now->right == nullptr) now = now->left, res = (1<<dep);
                else now = now->right;
            }
            ret |= res;
        }
        return x^ret;
    }

    int find_min(int x) {
        return find(x, 0);
    }

    int find_max(int x) {
        return find(x, 1);
    }
    
    void remove(int x) {
        Node *now = root;
        stack<pair<Node *, char>> st;
        st.emplace(now, 'L');
        for(int dep=25;--dep>=0;) {
            int bit = x & (1<<dep);
            if(bit) {
                now = now->left;
                st.emplace(now, 'L');
            }
            else {
                now = now->right;
                st.emplace(now, 'R');
            }
        }
        bool l = 0, r = 0;
        while(!st.empty()) {
            auto cur = st.top(); st.pop();
            if(l) cur.first->left = nullptr;
            if(r) cur.first->right = nullptr;
            l = 0, r = 0;
            if(!--cur.first->cnt) {
                cur.first = nullptr;
                if(cur.second == 'L') l = 1, r = 0;
                else l = 0, r = 1;
            }
        }
    }
};

Trie *trie;
set<int> s;

int add(int x) {
    if(!s.count(x)) {
        s.insert(x);
        trie->insert(x);
    }
    return s.size();
}

int remove_min() {
    if(s.empty()) return -1;
    int x = *s.begin();
    trie->remove(x);
    s.erase(x);
    return x;
}

int remove_max() {
    if(s.empty()) return -1;
    int x = *s.rbegin();
    trie->remove(x);
    s.erase(x);
    return x;
}

int main(){
    cin.tie(0)->sync_with_stdio(0);

    
    int T;
    for(cin>>T;T--;) {
        int N, Q;
        cin>>N>>Q;
        trie = new Trie();
        s = set<int>();

        for(int i=0,x;i<N;i++) {
            cin>>x;
            add(x);
        }

        for(int o,x;Q--;) {
            int ret = -1;
            cin>>o;
            if(o >= 4) {
                if(o == 4) ret = remove_min();
                else ret = remove_max();
            }
            else {
                cin>>x;
                if(o == 1) ret = trie->find_min(x);
                else if(o == 2) ret = trie->find_max(x);
                else ret = add(x);
            }
    
            cout<<ret<<'\n';
        }
    }

}
```
