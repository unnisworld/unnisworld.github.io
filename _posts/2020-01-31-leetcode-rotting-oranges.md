---
layout: post
title:  "Rotting Oranges"
date:   2020-02-08 10:30:00 +0530
categories: leetcode-easy leetcode grid
---

Solution to [Rotting Oranges problem][leetcode]. 

{% highlight java %}
class Solution {
    static int[] dr = new int[]{-1, 0, 1, 0};
    static int[] dc = new int[]{0, -1, 0, 1};

    public int orangesRotting(int[][] grid) {
        int R = grid.length, C = grid[0].length;

        // fill the queue with all starting cells with rotten oranges
        Queue<int[]> queue = new ArrayDeque();
        for (int r = 0; r < R; ++r)
            for (int c = 0; c < C; ++c)
                if (grid[r][c] == 2) {
                    queue.add(new int[] {r, c, 0});
                }

        int ans = 0;
        while (!queue.isEmpty()) {
            int[] code = queue.remove();
            int r = code[0], c = code[1], depth = code[2];
            for (int k = 0; k < 4; ++k) {
                int nr = r + dr[k];
                int nc = c + dc[k];
                if (isValidCell(R, C, nr, nc) && isFreshOrange(grid[nr][nc])) {
                    grid[nr][nc] = 2;
                    queue.add(new int[] {nr, nc, depth + 1});
                    ans = depth + 1;
                }
            }
        }

        // if there are fresh oranges left, return -1.
        for (int[] row: grid)
            for (int v: row)
                if (v == 1)
                    return -1;

        return ans;
    }

    private static boolean isFreshOrange(int i) {
        return i == 1;
    }

    private static boolean isValidCell(int r, int c, int nr, int nc) {
        return (nr > -1 && nc > -1) && (nr < r && nc < c);
    }

}
{% endhighlight %}

# Algorithm

We can use a breadth-first search to model this process. Because we always explore nodes (oranges) with the smallest depth first, we're guaranteed that each orange that becomes rotten does so with the lowest possible depth number.

The solution given here is a slightly simplified version of the original solution [provided by leetcode][leetcode-article].

[leetcode]: https://leetcode.com/problems/rotting-oranges/
[leetcode-article]: https://leetcode.com/articles/rotting-oranges/
