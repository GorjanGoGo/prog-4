#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int n, m, s, t;
ll cap[105][105];
bool vis[105];

ll dfs(int u, ll f) {
    if (u == t) return f;
    vis[u] = true;
    for (int v = 0; v < n; v++) {
        if (!vis[v] && cap[u][v] > 0) {
            ll p = dfs(v, min(f, cap[u][v]));
            if (p > 0) {
                cap[u][v] -= p;
                cap[v][u] += p;
                return p;
            }
        }
    }
    return 0;
}

int main() {
    cin >> n >> m >> s >> t;
    while (m--) {
        int u, v; ll c;
        cin >> u >> v >> c;
        cap[u][v] += c;
    }
    ll flow = 0, f;
    while (memset(vis, 0, sizeof vis), (f = dfs(s, LLONG_MAX)) > 0) flow += f;
    cout << flow << endl;
}