# minimum-swaps-to-array-a-binary-grid
leetcode problem No:1536class Solution {
    public int minSwaps(int[][] grid) {
        int n = grid.length;
        int[] trailing = new int[n];

        // Count trailing zeros for each row
        for (int i = 0; i < n; i++) {
            int count = 0;
            for (int j = n - 1; j >= 0; j--) {   // MUST be >= 0
                if (grid[i][j] == 0) {
                    count++;
                } else {
                    break;
                }
            }
            trailing[i] = count;
        }

        int swaps = 0;

        for (int i = 0; i < n; i++) {
            int need = n - i - 1;
            int j = i;

            while (j < n && trailing[j] < need) {
                j++;
            }

            if (j == n) return -1;

            while (j > i) {
                int temp = trailing[j];
                trailing[j] = trailing[j - 1];
                trailing[j - 1] = temp;
                j--;
                swaps++;
            }
        }

        return swaps;
    }
}
