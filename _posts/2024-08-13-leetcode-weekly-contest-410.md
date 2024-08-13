---
layout: post
title: Weekly Contest 410
categories: [Leetcode, Competitive Programming]
description: Leetcode contest speedrun 100%
keywords: Leetcode, CP
mermaid: false
sequence: false
flow: false
mathjax: false
mindmap: false
mindmap2: false
---

## [Snake in matrix](https://leetcode.com/problems/snake-in-matrix/description/)

Problem summary: Given a $n \times n$ grid, starts from (0, 0), move like instruction, and return the cell after the last instruction.

Return the cell by calculate its id with the formula (i * n + j);

Solution: when moving on a grid (one step at a time), only x or y change by one. So we must imagine the movements in head and implement it:

```c++
class Solution {
public:
    int finalPositionOfSnake(int n, vector<string>& commands) {
        int cur_x = 0, cur_y = 0;
        for (string& s : commands) {
            if (s == "UP") cur_x--;
            else if (s == "DOWN") cur_x++;
            else if (s == "LEFT") cur_y--;
            else if (s == "RIGHT") cur_y++;
        }
        return (cur_x * n + cur_y);
    }
};
```

## [Count the Number of good Nodes](https://leetcode.com/problems/count-the-number-of-good-nodes/description/)

Problem summary: Given a tree with $n$ nodes, count the number of **good** nodes. A node is good if all the **subtrees** rooted at its children have the same size.

Solution: Obviously, for all tree problem, we should just use DFS with a template some what like this:

```c++
const int N = 1e5 + 11;
vector<int> adj[N];

void dfs(int u, int p = -1) {
    // do smth here
    for (int v : adj[u]) {
        if (v == p) continue;
        // do smth here
        dfs(v, u);
        // do smth here
    }
    // do smth here
}
```

And for this problem, we need to calculate the number of children for each node, thus we will keep `nChild[u]` as number of children is subtree of `u`, and do it like this:

```c++
int nChild[100011];
vector<int> adj[100011];

class Solution {
private:
    int ans = 0;
public:
    void dfs(int u, int p = -1) {
        nChild[u] = 1;
        
        int z = -1;
        bool all_equal = true;
        for (int v : adj[u]) {
            if (v == p) continue;
            dfs(v, u);
            if (z == -1) z = nChild[v];
            else if (z != nChild[v]) all_equal = false;
            nChild[u] += nChild[v];
        }
        if (all_equal) ++ans;        
    }
    
    int countGoodNodes(vector<vector<int>>& edges) {
        int n = edges.size();
        for (int i = 0; i <= n; i++) {
            adj[i].clear();
            nChild[i] = 0;
        }
        for (auto &v : edges) {
            adj[v[0]].push_back(v[1]);
            adj[v[1]].push_back(v[0]);
        }
        dfs(0);
        return ans;
    }
};
```

## [Find the Count of monotonic Pairs II](https://leetcode.com/problems/find-the-count-of-monotonic-pairs-ii/description/)

Problem summary: Too lazy, read problem statement for me please :(

Solution: My experience tells me that most of the problems where we need to **count numbers of ways** to do something, it should be either a combinatorics problem or a DP problem (or both, DP combinatorics).

Since I cannot think of anyway to apply combinatorics into this problem, it must be a DP problem. Notice that $n$ is only 2000, so my guess it we should implement a somewhat $O(n^2)$ DP problem.

Continue with using DP, so if I want to build up the array with $n$ elements, I should keep a param as **current index position**, and from the problem statement, I should keep something as **previous element that I build in the first array** (because we simply can get the second element by a minus calculation) to control the monotonic property of both array. 

So I **must** keep 2 parameters like above (which should be $O(n^2)$ already) -> I need to find a way to transition DP in $O(1)$. So, after scribble for about 1 or 2 minutes, I thought of this:

```
1. dp(i, p1) -> dp(i, p1 + 1)
Increase the current first element by one

2. dp(i, p1) -> dp(i + 1, max(p1, nums[i + 1] - p2))
If we move to the next position, we must build the first element from at least p1, or from nums[i + 1] - p2 to keep the non-increasing property for second array.
```

So... transition $O(1)$, number of states $O(n^2)$ -> Overall $O(n^2)$

Thus I come up with the solution:

```c++
int f[2011][2011];
bool g[2011][2011];

const int mod = 1e9 + 7;
class Solution {
private:
    int n;
    vector<int> num;
public:
    int dp(int pos, int p1) {
        if (pos >= n)
            return 0;
        if (p1 > num[pos])
            return 0;
        if (g[pos][p1])
            return f[pos][p1];
        int ans = (pos == n - 1);
        (ans += dp(pos, p1 + 1)) %= mod;
        int p2 = num[pos] - p1;
        if (pos < n - 1)
            (ans += dp(pos + 1, max(p1, num[pos + 1] - p2))) %= mod;
        g[pos][p1] = true;
        return f[pos][p1] = ans;
    }
    
    int countOfPairs(vector<int>& nums) {
        n = nums.size();
        num = nums;
        for (int i = 0; i <= n; i++)
            for (int j = 0; j <= 1011; j++)
                g[i][j] = false;
        return dp(0, 0);
    }
};
```