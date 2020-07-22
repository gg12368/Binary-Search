441. 排列硬币
你总共有 n 枚硬币，你需要将它们摆成一个阶梯形状，第 k 行就必须正好有 k 枚硬币。
给定一个数字 n，找出可形成完整阶梯行的总行数。
n 是一个非负整数，并且在32位有符号整型的范围内。

示例 1:
n = 5
硬币可排列成以下几行:
¤
¤ ¤
¤ ¤
因为第三行不完整，所以返回2.

示例 2:
n = 8
硬币可排列成以下几行:
¤
¤ ¤
¤ ¤ ¤
¤ ¤
因为第四行不完整，所以返回3.

class Solution {
    public int arrangeCoins(int n) {
        
        long low=1;
        long height =n;
        while(low<=height){

            long mid =low+height>>1;
            // 先计算出来 避免重复计算
            long sum= help(mid);
            if(sum==n) return (int) mid;
            else if (sum>n) height=mid-1;
            else low=mid+1;
        }
        // 这里返回low-1的其实可以推到一下，如果当low=height 的时候当前的和大于n了，也就意味着help(low)>n了 所以 low需要减一
        // 同理可以推到出 当前和小于n的情况
        return (int) low-1;
    }
    // 等差数列前n项和公式
    private long help(long n) {      
        return n * (n + 1) >> 1;
    }
}

