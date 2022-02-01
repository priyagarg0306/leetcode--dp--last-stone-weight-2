# leetcode--dp--last-stone-weight-2

**----> problem:**

You are given an array of integers stones where stones[i] is the weight of the ith stone.

We are playing a game with the stones. On each turn, we choose any two stones and smash them together. Suppose the stones have weights x and y with x <= y. The result of this smash is:

If x == y, both stones are destroyed, and
If x != y, the stone of weight x is destroyed, and the stone of weight y has new weight y - x.
At the end of the game, there is at most one stone left.

Return the smallest possible weight of the left stone. If there are no stones left, return 0.

 

Example 1:

Input: stones = [2,7,4,1,8,1]
Output: 1
Explanation:
We can combine 2 and 4 to get 2, so the array converts to [2,7,1,8,1] then,
we can combine 7 and 8 to get 1, so the array converts to [2,1,1,1] then,
we can combine 2 and 1 to get 1, so the array converts to [1,1,1] then,
we can combine 1 and 1 to get 0, so the array converts to [1], then that's the optimal value.
Example 2:

Input: stones = [31,26,33,21,40]
Output: 5
 

Constraints:

1 <= stones.length <= 30
1 <= stones[i] <= 100

**-----> code:**

class Solution {
public:
    int lastStoneWeightII(vector<int>& v) {
        
        int n=v.size(),sum=0,sum1=0;
        
        for(int i=0;i<n;i++){
            sum+=v[i];
        }
        
        sum1=sum/2;
        
        vector<vector<int>> dp(n+1,vector<int>(sum1+1));
        
        for(int i=0;i<=n;i++){
            for(int j=0;j<=sum1;j++){
                if(i==0 ||j==0){
                    dp[i][j]=0;
                }else{
                    if(v[i-1]<=j){
                        dp[i][j]=max(dp[i-1][j],dp[i-1][j-v[i-1]]+v[i-1]);
                    }else{
                        dp[i][j]=dp[i-1][j];
                    }
                }
                
            }
        }
        
        return sum-2*dp[n][sum1];
        
    }
};
