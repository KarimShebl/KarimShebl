## **Mid 1 - Problem A (Math + Number Theory):**

```c++
#include <bits/stdc++.h>

using namespace std;
#define int long long
#define vi vector<int>
#define vp vector<pair<int, int>>
#define pb(x) push_back(x)
#define all(x) x.begin(), x.end()
#define FastIO ios_base::sync_with_stdio(false);cin.tie(nullptr);cout.tie(nullptr);
#define mem(a, x) memset(a, x, sizeof a)
#define Ones(n) __builtin_popcountll(n)
#define endl '\n'
const int N = 1e6 + 1;
int n;
vi d(N);
void pre()
{
    for (int i = 1; i <= n; ++i) {
        for (int j = 1; i * j <= n; j++)
            d[i * j]++;
    }
}
void solve() {
    cin >> n;
    pre();
    int ans = 0;
    for (int x = 1; x <= n; ++x) {
        // y = (n - 3x) / 7z
        if(n - 3 * x <= 0)
            break;
        if((n - 3 * x) % 7)
            continue;
        ans += d[(n - 3 * x) / 7];
    }
    cout << ans << endl;
}

signed main() {
    FastIO
    int T = 1;
//    cin >> T;
    while (T--) {
        solve();
    }
    return 0;
}
```











## **Mid 1 - Problem B (Approach 1: Two Pointers):**

```c++
#include <bits/stdc++.h>

using namespace std;
#define int long long
#define vi vector<int>
#define vp vector<pair<int, int>>
#define pb(x) push_back(x)
#define all(x) x.begin(), x.end()
#define FastIO ios_base::sync_with_stdio(false);cin.tie(nullptr);cout.tie(nullptr);
#define mem(a, x) memset(a, x, sizeof a)
#define Ones(n) __builtin_popcountll(n)
#define endl '\n'
void solve() {
    int n;
    cin >> n;
    vi a(n);
    for (int i = 0; i < n; ++i) {
        cin >> a[i];
    }

    int l = 0, r = 0, val = 0, ans = 0;
    while (l < n)
    {
        if(r < n && (val | a[r]) == (val ^ a[r]))
        {
            val ^= a[r];
            r++;
        }
        else
        {
            ans += r - l;
            val ^= a[l];
            l++;
        }
    }
    cout << ans << endl;
}

signed main() {
    FastIO
    int T = 1;
//    cin >> T;
    while (T--) {
        solve();
    }
    return 0;
}
```











## **Mid 1 - Problem B (Approach 2: Binary Search):**

```c++
#include <bits/stdc++.h>

using namespace std;
#define int long long
#define vi vector<int>
#define vp vector<pair<int, int>>
#define pb(x) push_back(x)
#define all(x) x.begin(), x.end()
#define FastIO ios_base::sync_with_stdio(false);cin.tie(nullptr);cout.tie(nullptr);
#define mem(a, x) memset(a, x, sizeof a)
#define Ones(n) __builtin_popcountll(n)
#define endl '\n'
void solve() {
    int n;
    cin >> n;
    vi a(n);
    for (int i = 0; i < n; ++i) cin >> a[i];
    int ans = 0;
    for (int i = 0; i < n; ++i) {
        int l = i, r = n - 1, dist = 0;
        while (l <= r)
        {
            int mid = (l + r) / 2;
            int ORing = 0, XORing = 0;
            for (int j = i; j <= mid; ++j) {
                ORing |= a[j];
                XORing ^= a[j];
            }
            if(ORing == XORing)
                dist = mid - i + 1, l = mid + 1;
            else
                r = mid - 1;
        }
        ans += dist;
    }
    cout << ans << endl;
}

signed main() {
    FastIO
    int T = 1;
//    cin >> T;
    while (T--) {
        solve();
    }
    return 0;
}
```











## **Mid 1 - Problem C (Number Theory + Prefix Sum + Static Range Queries):**

```c++
#include <bits/stdc++.h>

using namespace std;
#define int long long
#define vi vector<int>
#define vp vector<pair<int, int>>
#define pb(x) push_back(x)
#define all(x) x.begin(), x.end()
#define FastIO ios_base::sync_with_stdio(false);cin.tie(nullptr);cout.tie(nullptr);
#define mem(a, x) memset(a, x, sizeof a)
#define Ones(n) __builtin_popcountll(n)
#define endl '\n'
const int sz = 1e6 + 1;
bool compo[sz + 1];
vector<int> primes(sz);
void sieve()
{
    compo[0] = compo[1] = true;
    for (int i = 2; i * i <= sz; ++i)
    {
        if(!compo[i])
        {
            primes[i]++;
            for (int j = i * i; j <= sz; j += i) {
                compo[j] = true;
            }
        }
    }
    for (int i = 1; i < sz; ++i) primes[i] += primes[i - 1];
}
void solve() {
    int l, r; cin >> l >> r;
    cout << primes[r] - primes[l - 1] << endl;
}

signed main() {
    FastIO
    sieve();
    int T = 1;
    cin >> T;
    while (T--) {
        solve();
    }
    return 0;
}
```











## **Mid 1 - Problem D(Pure Binary Search):**

```c++
#include <bits/stdc++.h>

using namespace std;
#define int long long
#define vi vector<int>
#define vp vector<pair<int, int>>
#define pb(x) push_back(x)
#define all(x) x.begin(), x.end()
#define FastIO ios_base::sync_with_stdio(false);cin.tie(nullptr);cout.tie(nullptr);
#define mem(a, x) memset(a, x, sizeof a)
#define Ones(n) __builtin_popcountll(n)
#define endl '\n'

void solve() {
    int n;
    cin >> n;
    vi a(n);
    for (int i = 0; i < n; ++i) cin >> a[i];
    sort(all(a), greater());
    int q;
    cin >> q;
    while (q--) {
        int x;
        cin >> x;
        int l = 0, r = n - 1, ans = -1;
        while (l <= r) {
            int mid = (l + r) / 2;
            if (a[mid] > x)
                ans = mid, l = mid + 1;
            else
                r = mid - 1;
        }
        cout << ans + 1 << ' ';
    }
    cout << endl;
}

signed main() {
    FastIO
    int T = 1;
    cin >> T;
    while (T--) {
        solve();
    }
    return 0;
}
```











## **Mid 1 - Problem E(Complete Search using Backtracking):**

```c++
#include <bits/stdc++.h>

using namespace std;
#define int long long
#define vi vector<int>
#define vp vector<pair<int, int>>
#define pb(x) push_back(x)
#define all(x) x.begin(), x.end()
#define FastIO ios_base::sync_with_stdio(false);cin.tie(nullptr);cout.tie(nullptr);
#define mem(a, x) memset(a, x, sizeof a)
#define Ones(n) __builtin_popcountll(n)
#define endl '\n'
int n;
string chars;
vector<string> ans;

void slv(string s) {
    if (s.size() > n)
        return;
    for (int i = 0; i < chars.size(); ++i) {
        s += chars[i];
        slv(s);
        s.pop_back();
    }
    ans.pb(s);
}

void solve() {
    ans.clear();
    cin >> n >> chars;
    slv("");
    sort(all(ans));
    for (int i = 0; i < ans.size(); ++i) {
        cout << ans[i] << endl;
    }
}

signed main() {
    FastIO
    int T = 1;
    cin >> T;
    int c = 1;
    while (T--) {
        cout << "Case " << c++ << ":" << endl;
        solve();
    }
    return 0;
}
```









## **Mid 2 - Problem B(Two Pointers):**

```c++
#include <bits/stdc++.h>

using namespace std;
#define int long long
#define vi vector<int>
#define vp vector<pair<int, int>>
#define pb(x) push_back(x)
#define all(x) x.begin(), x.end()
#define FastIO ios_base::sync_with_stdio(false);cin.tie(nullptr);cout.tie(nullptr);
#define mem(a, x) memset(a, x, sizeof a)
#define Ones(n) __builtin_popcountll(n)
#define endl '\n'

void solve() {
    int n, t;
    cin >> n >> t;
    vi a(n), b(n);

    for (int i = 0; i < n; ++i) {
        cin >> a[i];
    }

    for (int i = 0; i < n; ++i) {
        cin >> b[i];
    }

    int l = 0, r = 0, curr = 0, sum = 0, ans = 0, ansl = 0, ansr = 0;
    while (l < n) {
        if (r < n && curr + a[r] <= t) {
            curr += a[r];
            sum += b[r];
            r++;
        } else {
            if (sum >= ans) ans = sum, ansl = l + 1, ansr = r;
            curr -= a[l];
            sum -= b[l];
            l++;
        }
    }
    cout << ansl << ' ' << ansr << endl;
}

signed main() {
    FastIO
    int T = 1;
//    cin >> T;
    while (T--) {
        solve();
    }
    return 0;
}
```
