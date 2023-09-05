# 算法leetcode题解

## 待整理
- [1499. 满足不等式的最大值](https://leetcode.cn/problems/max-value-of-equation/)

## 数学
### 204. 计数质数
- [原题](https://leetcode.cn/problems/count-primes/)
- 关键：判断质数（素数）
- 方法
  - 方法1 - 暴力解法，超时
  - 方法2 - 判断质数 区间[2, 根号n]
  - 方法3 - 埃氏筛
  - 方法4 - 线性筛，参考官方题解
- 时空复杂度
  - 方法1 - 暴力解法：O(n * n), O(1)
  - 方法2 - 缩减区间：O(n * √n), O(1)
  - 方法3 - 埃氏筛：O(n * loglogn), O(n)
  - 方法4 - 线性筛：O(n), O(n)

```js
// 方法1 - 暴力解法，超时
var countPrimes = function(n) {
  if (n < 2) return 0;
  let res = 0;
  // 判断正整数num是否为质数，除了1和本身，如果还有[2, num-1]的因数，则不是质数
  var isPrime = (num) => {
    if (n < 2) return false;
    let res = true;
    for (let i = 2; i < num - 1; i++) {
      if (num % i === 0) {
        res = false;
        break;
      }
    }
    return res;
  }
  for (let i = 2; i < n; i++) {
    if (isPrime(i)) res++;
  }
  return res;
};

// 方法2 - 判断质数 区间[2, 根号n]
var countPrimes = function(n) {
  if (n < 2) return 0;
  let res = 0;
  // 判断正整数num是否为质数
  var isPrime = (num) => {
    // 若存在 i 是 num 的 因数，那么 num / i 也是num的因数，我们只需要遍历到 min(i, num/i) 就可以判断了
    // 因为 abs(i - num/i) > 0 所以因数的较小者必然落在 [2, 根号num] 中
    if (num < 2) return false;
    for (let i = 2; i * i <= num; i++) {
      if (num % i === 0) {
        return false;
      }
    }
    return true;
  }
  for (let i = 2; i < n; i++) {
    if (isPrime(i)) res++;
  }
  return res;
};

// 方法3 - 埃氏筛
var countPrimes = function(n) {
  if (n < 2) return 0;
  let res = 0;
  let isPrime = Array(n).fill(true); // 默认每个数都标记为质数
  // 然后质数的倍数都排除掉，例如质数 2 对应的 4、6、8... 质数3 对应的 6、9、12...
  // 都排除掉后，剩下的就是真正的质数
  for (let i = 2; i < n; i++) {
    if (isPrime[i]) {
      for (let j = 2 * i; j < n; j += i) {
        isPrime[j] = false;
      }
    }
  }
  // 统计质数个数
  for (let i = 2; i < n; i++) {
    if (isPrime[i]) res++;
  }
  return res;
  // 优化1：统计质数个数的循环可以合并到前面，参考官方题解
  // 优化2：前面嵌套循环的内外层for循环都可以缩减范围，参考：https://labuladong.github.io/algo/di-san-zha-24031/shu-xue-yu-659f1/ru-he-gao--e19ec/
};
```



## 正则
### 468. 验证IP地址
- [原题](https://leetcode.cn/problems/validate-ip-address/)
- 方法
  - 方法1 - 暴力解法，依次判断，参考官方题解
  - 方法2 - 正则

```js
// 方法2 - 正则
var validIPAddress = queryIP =>
    queryIP.match(/^((25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)($|(?!\.$)\.)){4}$/) ? "IPv4":
    queryIP.match(/^(([\da-fA-F]{1,4})($|(?!:$):)){8}$/) ? "IPv6" : "Neither";
```

## 链表
### 143. 重排链表
- [原题](https://leetcode.cn/problems/reorder-list/)

## 二维数组
### 48. 旋转图像
- [原题](https://leetcode.cn/problems/rotate-image/)
- 分析：顺时针旋转二维数组，其实就是把每一列变成没每一行，但因为是原地修改，不能采取这种直接改变数组元素的思路，否则第一列变成第一行的时候，第二列的原始信息就丢失了，只能使用交换数组元素的方法，具体参考思路
- [思路](https://labuladong.github.io/algo/di-yi-zhan-da78c/shou-ba-sh-48c1d/er-wei-shu-150fb/)
```js
ar rotate = function(matrix) {
    var n = matrix.length;
    // 先沿对角线镜像对称二维矩阵
    for (var i = 0; i < n; i++) {
        for (var j = i; j < n; j++) {
            // swap(matrix[i][j], matrix[j][i]);
            var temp = matrix[i][j];
            matrix[i][j] = matrix[j][i];
            matrix[j][i] = temp;
        }
    }
    // 然后反转二维矩阵的每一行
    for (var row of matrix) {
        reverse(row);
    }
}

var reverse = function(arr) {
    var i = 0, j = arr.length - 1;
    while (j > i) {
        // swap(arr[i], arr[j]);
        var temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        i++;
        j--;
    }
}
```

## 双指针
### 141. 环形链表
- [原题](https://leetcode.cn/problems/linked-list-cycle/)
- 解题思路
	- 借助生活中的经验：如果是跑圈并且一直跑，跑得快的一定会再次追上跑得慢的
	- 新建fast slow指针，遍历链表，fast每次走两步，slow每次走一步
	- 当两者相遇，说明有环
	- 如果遍历到null指针，说明无环

- 特殊情况：
	- 链表无环：快指针先结束遍历
- 时间复杂度：O(n)  即使是跑m圈，也是O(n)  
- 空间复杂度：O(1) 

```js
var hasCycle = function(head) {
  if (!head || !head.next) return false;
  let slow = head;
  let fast = head;
  while (slow && fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
    if (slow === fast) {
      return true;
    }
  }
  return false;
};
```

## 前缀和、差分数组、线段树
### 2569. 更新数组后处理求和查询
- [原题](https://leetcode.cn/problems/handling-sum-queries-after-update/)
- [官方题解：线段树](https://leetcode.cn/problems/handling-sum-queries-after-update/solution/geng-xin-shu-zu-hou-chu-li-qiu-he-cha-xu-kv6u/)

```js
// 方法1 - 暴力解法，超时
var handleQuery = function(nums1, nums2, queries) {
  let res = [];
  for (let ops of queries) {
    if (ops[0] === 1) {
      for (let i = ops[1]; i<=ops[2]; i++) {
        nums1[i] = nums1[i] === 1 ? 0 : 1;
      }
    } else if (ops[0] === 2) {
      for (let i = 0; i < nums2.length; i++) {
        nums2[i] = nums2[i] + nums1[i] * ops[1];
      }
    } else if (ops[0] === 3) {
      let tmp = nums2.reduce((acc, cur) => acc + cur, 0);
      res.push(tmp);
    }
  }
  return res;
};

// 方法2 - 线段树，参考官方题解
```

## 回溯
### 剑指 Offer 38. 字符串的排列
- [原题](https://leetcode.cn/problems/zi-fu-chuan-de-pai-lie-lcof/description/)
- 方法
  - 方法1-回溯+去重
  - 方法2-回溯剪枝
- 代码

```js
// 方法1-回溯+去重
var permutation = function(s) {
  let arr = s.split('')
  let res = [];
  let track = [];
  let used = [];
  let backtrack = (track) => {
    if (track.length === arr.length) {
      res.push(track.join(''))
    }
    for (let i = 0; i<arr.length; i++) {
      if (used.includes(i)) continue;
      track.push(arr[i]);
      used.push(i);
      backtrack(track);
      track.pop(arr[i]);
      used.pop(i);
    }
  }
  backtrack(track);
  return [...new Set(res)];
};

// 方法2-回溯剪枝
var permutation = function(s) {
  // 参考 47. 全排列 II 的逻辑
  let arr = s.split('').sort(); // 需要让字母排序
  let res = [];
  let track = [];
  let used = [];
  let backtrack = (track) => {
    if (track.length === arr.length) {
      res.push(track.join(''))
    }
    for (let i = 0; i<arr.length; i++) {
      // 不重复选元素
      if (used.includes(i)) continue;
      // 不选择相同的元素，避免生成相同的排列
      if (i > 0 && arr[i] === arr[i - 1] && !used.includes(i - 1)) continue;
      track.push(arr[i]);
      used.push(i);
      backtrack(track);
      track.pop(arr[i]);
      used.pop(i);
    }
  }
  backtrack(track);
  return res;
};
```

## 动态规划
### 70. 爬楼梯
- [原题](https://leetcode.cn/problems/climbing-stairs/)
- 理解题目：
- 方法
	- 方法1 - 动态规划 - 自底向上
  - 方法2 - 动态规划 - 自顶向下，超时
  - 方法3 - 动态规划 - 自顶向下 + 备忘录

```js
// 方法1 - 动态规划 - 自底向上
var climbStairs = function(n) {
  // dp数组定义: 每次爬1或2层，爬n层楼梯的方法数
  let dp = Array(n + 1).fill(null); // 保证能访问dp[n]
  // base case
  dp[0] = 0;
  dp[1] = 1;
  dp[2] = 2;
  for (let i = 3; i<= n; i++) {
    // 理解题意，得出状态转换方程
    dp[i] = dp[i - 1] + dp [i - 2];
  }
  return dp[n];
};

// 方法2 - 动态规划 - 自顶向下，超时
var climbStairs = function(n) {
  // 目标状态：阶梯层数 n
  // 选择：每次爬 1 或 2 层
  // dp函数定义: 传入 n ，返回爬n层楼梯的方法数
  var dp = function(n) {
    // base case
    if (n === 1) return 1;
    if (n === 2) return 2;
    let res = 0;
    // 状态转换方程：因为一次可以爬1层或2层，所以爬n层阶梯的方法数 = 爬n-1层方法数 再加上 爬n-2层方法数
    res = dp(n - 1) + dp(n - 2);
    return res;
  }
  return dp(n);
};

// 方法3 - 动态规划 - 自顶向下 + 备忘录
var climbStairs = function(n) {
  // 备忘录，memo[n]表示爬n层楼梯的方法数
  let memo = {
    1: 1,
    2: 2
  };
  // 目标状态：阶梯层数 n
  // 选择：每次爬 1 或 2 层
  // dp函数定义: 传入 n ，返回爬n层楼梯的方法数
  var dp = function(n) {
    // base case
    if (n === 1 || n === 2) return memo[n];
    let res = 0;
    // 状态转换方程：因为一次可以爬1层或2层，所以爬n层阶梯的方法数 = 爬n-1层方法数 再加上 爬n-2层方法数
    let step1 = memo[n - 1] !== undefined ? memo[n - 1] : dp(n - 1);
    let step2 = memo[n - 2] !== undefined ? memo[n - 2] : dp(n - 2);
    res = step1 + step2;
    memo[n] = res;
    return res;
  }
  return dp(n);
};
```

### 509. 斐波那契数
- [原题](https://leetcode.cn/problems/fibonacci-number/)
- 理解题目：
- 方法
	- 方法一：最直观的方法
	- 方法二：自顶向下
	- 方法三：自底向上
	- 方法四：方法三基础上，根据题目特性，进一步优化空间复杂度

```js
// 方法一：最直观的方法
var fib = function(n) {
  if (n === 0) return 0;
  if (n === 1) return 1;
  return fib(n - 1) + fib(n - 2);
};

// 方法二：自顶向下的顺序：f(4) -> f(3) -> f(2) -> ...
var fib = function(n) {
  let memo = [0, 1]; // 备忘录
  var traverse = function(n) {
    if (memo[n] === undefined) {
      memo[n] = traverse(n - 1) + traverse(n - 2); // 状态转换方程
    }
    return memo[n];
  }
  return traverse(n);
};

// 方法三：自底向上的顺序：... -> f(2) -> f(3) -> f(4)
var fib = function(n) {
  let dp = [0, 1];
  // 逐步使用循环直到算出dp[n]
  for (let i = 2; i<=n; i++) {
    dp[i] = dp[i-1] + dp[i-2];
  }
  return dp[n];
};

// 方法四：方法三基础上，进一步优化空间复杂度
var fib = function(n) {
  // 由于fib(n)只和前面两个元素有关，所以可以直接用两个变量取代dp数组
  let pre = 0, cur = 1;
  // 逐步使用循环直到算出dp[n]
  for (let i = 2; i<=n; i++) {
    let sum = pre + cur;
    pre = cur;
    cur = sum;
  }
  return n < 2 ? n : cur;
};
```

### 322. 零钱兑换
- [原题](https://leetcode.cn/problems/coin-change/)
- 理解题目：
	- 详见方法一的注释
- 方法
	- 方法一：动态规划-暴力穷举-自顶向下，超时
	- 方法二：在方法一的基础上添加备忘录，去掉重复子问题的冗余计算。
	- 方法三：动态规划-自底向上
- 时间复杂度
	- 递归的时间复杂度 = 递归次数 * 递归函数的时间复杂度
	- 方法一：由递归树可知，指数级
	- 方法二：O(amount * n)，其中n为coins的元素个数

```js
// 方法一：动态规划-暴力穷举-自顶向下，超时
var coinChange = function(coins, amount) {
  // 状态：目标金额 amount
  // 选择：coins中的硬币面额
  // dp函数定义：传入coins和amount，返回凑出amount所需要的最少硬币枚数
  // base case：amount等于0，返回0枚硬币；amount<0，返回-1枚硬币；
  // 状态转换方程：amount所需最小硬币枚数 = 1 + (amount - coins[i])所需最小硬币枚数
  // 例子：dp([1,2,5], 11) = 1 + Math.min(dp([1,2,5], 10), dp([1,2,5], 9), dp([1,2,5], 6))
  var dp = function(coins, amount) {
    // base case
    if (amount === 0) return 0;
    if (amount < 0) return -1;
    // res可以初始化为最大值，然后通过Math.min()不断变小
    let res = Number.MAX_VALUE;
    // 遍历子问题的情况
    for (let coin of coins) {
      let subAmount = amount - coin;
      let subMin = dp(coins, subAmount); // 计算子问题的结果
      if (subMin === -1) continue;
      res = Math.min(res, 1 + subMin); // 状态转换方程
    }
    return res === Number.MAX_VALUE ? -1 : res;
  }
  return dp(coins, amount);
};

// 方法二：方法一基础上，添加备忘录
var coinChange = function(coins, amount) {
  let memo = {}; // 备忘录
  var dp = function(coins, amount) {
    if (amount === 0) return 0;
    if (amount < 0) return -1;
    if (memo[amount] !== undefined) return memo[amount]; // 如果备忘录有值，直接返回
    let res = Number.MAX_VALUE;
    for (let coin of coins) {
      let subAmount = amount - coin;
      let subMin = dp(coins, subAmount);
      if (subMin === -1) continue;
      res = Math.min(res, 1 + subMin);
    }
    memo[amount] = res === Number.MAX_VALUE ? -1 : res; // 更新备忘录
    return memo[amount];
  }
  return dp(coins, amount);
};


// 方法三：动态规划-自底向上
var coinChange = function(coins, amount) {
  // dp数组定义：凑出amount，至少需要dp[amount]枚硬币
  let dp = Array(amount + 1).fill(Number.MAX_VALUE); // 因为要取到dp[amount]，所以数组个数为amount + 1
  // base case
  dp[0] = 0;
  // 逐步完善dp数组
  for (let i = 1; i<=amount; i++) {
    // 遍历子问题
    for (let coin of coins) {
      let subAmount = i - coin;
      if (subAmount < 0) continue;
      dp[i] = Math.min(dp[i], 1 + dp[subAmount]); // 状态转换方程
    }
  }
  return dp[amount] === Number.MAX_VALUE ? -1 : dp[amount];
};
```

### 72. 编辑距离
- [原题](https://leetcode.cn/problems/edit-distance/)
- 理解题目：
	- 详见
- 方法
	- 方法一：动态规划-自顶向下 + 备忘录
- 时间复杂度
	- 方法一：

```js
// 方法一：动态规划-自顶向下 + 备忘录
var minDistance = function(word1, word2) {
  // 备忘录
  let memo = {};
  // 目标状态 word1 -> word2 的最小操作次数
  // 选择：插入、删除、替换一个字符
  // dp函数定义：dp(i, j)表示 word1[0, i] -> word2[0, j]的最小操作次数
  var dp = function(i, j) {
    // base case
    if (i === -1) return j + 1;
    if (j === -1) return i + 1;
    // 查备忘录
    let key = `${i}->${j}`;
    if (key in memo) {
      return memo[key];
    }
    // 状态转换方程：双指针i和j分别从word1和word2的最后一个元素往前移，遇到相同的就一起 -1，不同的话根据情况修改i和j
    if (word1[i] === word2[j]) {
      memo[key] =  dp(i - 1, j - 1);
    } else {
      memo[key] = Math.min(
        dp(i, j - 1) + 1, // 插入
        dp(i - 1, j) + 1, // 删除
        dp(i - 1, j - 1) + 1 // 替换
      )
    }
    return memo[key];
  }
  return dp(word1.length - 1, word2.length - 1);
};
```

## BFS
### 111. 二叉树的最小深度
- [原题](https://leetcode.cn/problems/minimum-depth-of-binary-tree/)
- 理解题目：
- 方法
	- 方法一：BFS
- 时间复杂度
	- 方法一：
```js
var minDepth = function(root) {
  if (!root) return 0;
  let q = [root]; // 队列存储每一层的节点
  let depth = 1; // 返回值
  while (q.length) { // 从上往下遍历每一层
    let len = q.length;
    for (let i = 0; i < len; i++) { // 对于每一层，从左往右遍历每一个节点
      let cur = q.shift();
      if (cur.left === null && cur.right === null) return depth;
      // 将cur相邻的未访问过的结点放到下一层，对于二叉树就是它的左右子节点
      if (cur.left) q.push(cur.left);
      if (cur.right) q.push(cur.right);
    }
    depth++; // 遍历完一层后增加深度
  }
  return depth;
}
```