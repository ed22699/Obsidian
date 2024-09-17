
## Example
```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int[] totals = new int[amount+1];
        Arrays.fill(totals, amount+1);
        totals[0] = 0;
        for(int i = 1; i <= amount; i++){
            for(int coin: coins){
                if(i - coin >= 0){
                    totals[i] = Math.min(totals[i], totals[i-coin]+1);
                }
            }
        }
        if(totals[amount] > amount) return -1;
        return totals[amount];
    }
}

```