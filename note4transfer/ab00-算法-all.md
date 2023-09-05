# 算法

## 参考资料
- [力扣刷题平台](https://leetcode-cn.com/problemset/all/)
- 刷题语言选择
  - [C++基础](https://www.w3cschool.cn/cpp/)
  - [java基础](https://labuladong.github.io/algo/zhun-bei-g-8db77/xue-xi-ben-47278/)
  - JavaScript
  - Python
- 算法教程
  - [labuladong的算法小抄](https://github.com/labuladong/fucking-algorithm)
- 算法可视化
  - [visualgo](https://visualgo.net/zh)
  - [Visualizations](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html)
  - [algorithm-visualizer](https://github.com/algorithm-visualizer/algorithm-visualizer)
  - [leetcode动画题解](https://github.com/bayidatianshi/LeetCodeAnimation)
- 其他
  - [面试高频题，刷题交流，面经求职](https://github.com/afatcoder/LeetcodeTop)
  - [leetcode题解](https://github.com/azl397985856/leetcode)
  - [代码随想录](https://github.com/youngyangyang04/leetcode-master)
  - [多语言实现算法](https://github.com/doocs/leetcode)
  - [JavaScript 算法与数据结构](https://github.com/trekhleb/javascript-algorithms/blob/master/README.zh-CN.md)
  - [开源算法库](https://the-algorithms.com/zh_Hans)
  - [zip压缩算法](https://www.cnblogs.com/esingchan/p/3958962.html)

## 算法复杂度
[参考](https://github.com/youngyangyang04/leetcode-master)

### 一、时间复杂度
1. 作用：定性描述该算法的运行时间。

2. 概念：假设算法的问题规模为n，那么操作单元数量便用函数f(n)来表示，随着数据规模n的增大，算法执行时间的增长率和f(n)的增长率相同，这称作为算法的渐近时间复杂度，简称时间复杂度，记为 O(f(n))。

3. 大O：数学上用来表示上界。算法最坏情况下运行时间的上界，就是对任意数据输入的运行时间的上界。但是算法上大O代表的是一般情况，而不是严格的上界。
![大O](https://img-blog.csdnimg.cn/20210408130000855.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R1YW5nX2FuZw==,size_16,color_FFFFFF,t_70)

4. 化简：**默认数据规模足够大**的条件下，去掉常数项、常数系数和低阶项  
例一：O(2*n^2 + 10*n + 1000)  => O(n^2)  
例二：时间复杂度logn可忽略底数  
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021040813133621.png)

5. 排行：O(1)常数阶 < O(logn)对数阶 < O(n)线性阶 < O(n^2)平方阶 < O(n^3)(立方阶) < O(2^n) (指数阶)

6. 实例分析：找出n个字符串中相同的两个字符串
- 方法一：暴力枚举，n^2 次的遍历加上每次字符串比较所需的m次操作（假设字符串的长度m）  
时间复杂度：O(m * n * n)
- 方法二：先使用快速排序进行比较 O(m * n * logn），得出按字母顺序的字符串集合；这时相同的字符串会挨在一起，所以只需要再遍历一次即可O(n * m)   
时间复杂度：O(m * n * logn + n * m)  => O(m * n * logn) 
- 通过时间复杂度的比较，方法二更优。

7.实际体验算法性能：https://mp.weixin.qq.com/s/73ryNsuPFvBQkt6BbhNzLA  
测试结果：2.7 GHz的CPU，一秒脉冲27亿次（有27亿个时钟周期），忽略其他因素的影响下，一秒可以在O(n)算法下处理的规模大约为5*10^8。

8.递归算法的时间复杂度：递归的次数 * 每次递归中的操作次数（每次递归中的时间复杂度）  
例子：求x的n次方  
方法一：非递归，O(n)  
```cpp
int function1(int x, int n) {
    int result = 1;  // 注意 任何数的0次方等于1
    for (int i = 0; i < n; i++) { result = result * x; }
    return result;
}
```
方法二：直接递归，递归了n次，每次一个乘法，时间复杂度是 n * 1 = O(n)
```cpp
int function2(int x, int n) {
    if (n == 0) { return 1; }
    return function2(x, n - 1) * x;
}
```
方法三：将x二分后再递归相乘，这个递归算法的时间复杂度依然是O(n)，分析如下
```cpp
int function3(int x, int n) {
    if (n == 0) { return 1; }
    if (n % 2 == 1) { return function3(x, n / 2) * function3(x, n / 2)*x; }
    return function3(x, n / 2) * function3(x, n / 2);
}
```
可以用二叉树显示递归过程，这棵树上每一个节点就代表着一次递归并进行了一次相乘操作，所以进行了多少次递归的话，就是看这棵树上有多少个节点。当n为16时如下图：
![递归时间复杂度分析](https://img-blog.csdnimg.cn/20210412102617403.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R1YW5nX2FuZw==,size_16,color_FFFFFF,t_70)
![递归时间复杂度计算](https://img-blog.csdnimg.cn/20210412102838650.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R1YW5nX2FuZw==,size_16,color_FFFFFF,t_70)

方法四：通过记录中间递归结果优化方法三，减少递归次数，时间复杂度是 log2n * 1 = O(logn)
```cpp
int function4(int x, int n) {
    if (n == 0) { return 1; }
    int t = function4(x, n / 2);// 这里相对于function3，是把这个递归操作抽取出来并记录
    if (n % 2 == 1) { return t * t * x; } // 后续使用不需要再次递归了
    return t * t;
}
```

### 二、空间复杂度
1.概念与作用：对一个算法在运行过程中占用内存空间大小的量度

2.注意：有很多因素会影响程序真正内存使用大小，例如编译器的内存对齐，编程语言容器的底层实现等等这些都会影响到程序内存的开销。所以空间复杂度是预先大体评估程序内存使用的大小。

3.例子：
O(1)：随着n的变化，所需开辟的内存空间并不会随着n的变化而变化。
```cpp
int j = 0;
for (int i = 0; i < n; i++) { j++; }
```
O(n)：消耗空间和输入参数n保持线性增长
```cpp
int* a = new int(n);
for (int i = 0; i < n; i++) { a[i] = i; }
```
O(n^2)：消耗空间和输入参数n的平方保持线性增长，例如二维数组

递归算法的空间复杂度 = 每次递归的空间复杂度 * 递归深度

可见，空间复杂度与数据结构关系很大


4.内存管理：不同的编程语言各自的内存管理方式  
C/C++这种内存堆空间的申请和释放完全靠自己管理，不规范的写法容易导致内存泄漏或内存溢出；而Java、Python正常情况下则不需要程序员去考虑内存泄漏的问题，虚拟机都做了这些事情。
![C/C++程序运行所需内存空间](https://img-blog.csdnimg.cn/20210412112539424.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R1YW5nX2FuZw==,size_16,color_FFFFFF,t_70)

想要算出自己程序会占用多少内存就一定要了解自己定义的数据类型的大小
![C/C++的数据类型大小](https://img-blog.csdnimg.cn/20210412113815906.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R1YW5nX2FuZw==,size_16,color_FFFFFF,t_70)

注意指针所占字节的变化，1个字节占8个比特，那么4个字节就是32个比特，可存放数据的大小为2^32，也就是4G空间的大小，即：可以寻找4G空间大小的内存地址。安装64位的操作系统的计算机内存都已经超过了4G，也就是指针大小如果还是4个字节的话，就已经不能寻址全部的内存地址，所以64位编译器使用8个字节的指针才能寻找所有的内存地址。

5.内存对齐：牺牲内存（通常影响不会太大）提高运行速度的技术  
为什么要有内存对齐？  
平台原因：不是所有的硬件平台都能访问任意内存地址上的任意数据，某些硬件平台只能在某些地址处取某些特定类型的数据，否则抛出硬件异常。为了同一个程序可以在多平台运行，需要内存对齐。  
硬件原因：经过内存对齐后，CPU访问内存的速度大大提升。  

例子说明：

```cpp
struct node{
   char cha;
   int num;
}st;
int main() {
    int a[100];
    char b[100];
    node st;
    cout << sizeof(int) << endl; // 4
    cout << sizeof(char) << endl; // 1
    cout << sizeof(a) << endl; // 400
    cout << sizeof(b) << endl; // 100
    cout << sizeof(st) << endl; // 8（由于内存对齐，所以结果不是5）
}
```
CPU读取内存不是一次读取单个字节，而是一块一块的来读取内存，块的大小可以是2，4，8，16个字节，具体取多少个字节取决于硬件。假设CPU把内存划分为4字节大小的块：  
![内存对齐](https://img-blog.csdnimg.cn/20210412114746970.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R1YW5nX2FuZw==,size_16,color_FFFFFF,t_70)

直接将地址4，5，6，7处的四个字节数据读取到即可，只需要一次寻址。  
![非内存对齐](https://img-blog.csdnimg.cn/20210412114829646.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R1YW5nX2FuZw==,size_16,color_FFFFFF,t_70)

首先CPU读取0，1，2，3处的四个字节数据  
CPU读取4，5，6，7处的四个字节数据  
合并地址1，2，3，4处四个字节的数据才是本次操作需要的int数据  
此时一共需要两次寻址，一次合并的操作。  

### 三、算法性能分析
例子一：斐波那契数的递归写法

```cpp
int fibonacci(int i) {
       if(i <= 0) return 0;
       if(i == 1) return 1;
       return fibonacci(i-1) + fibonacci(i-2);
}
```
时间复杂度分析：递归的次数 * 每次递归的时间复杂度
![斐波那契时间复杂度分析](https://img-blog.csdnimg.cn/20210412122432703.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R1YW5nX2FuZw==,size_16,color_FFFFFF,t_70)

一棵深度（按根节点深度为1）为k的二叉树最多可以有 2^k - 1 个节点，每次递归都是O(1)的操作，所以该递归算法的时间复杂度为 O(2^n)  
测试耗时：随着n的增大，耗时的增长也越来越快  
```cpp
#include <iostream>
#include <chrono>
#include <thread>
using namespace std;
using namespace chrono;
int fibonacci(int i) {
       if(i <= 0) return 0;
       if(i == 1) return 1;
       return fibonacci(i - 1) + fibonacci(i - 2);
}
void time_consumption() {
    int n;
    while (cin >> n) {
        milliseconds start_time = duration_cast<milliseconds >(
            system_clock::now().time_since_epoch()
        );

        fibonacci(n);

        milliseconds end_time = duration_cast<milliseconds >(
            system_clock::now().time_since_epoch()
        );
        cout << milliseconds(end_time).count() - milliseconds(start_time).count()
            <<" ms"<< endl;
    }
}
int main()
{
    time_consumption();
    return 0;
}
```
优化算法：用first和second来记录当前相加的两个数值，减少递归的次数，递归了n次，所以时间复杂度是 O(n)

```cpp
int fibonacci(int first, int second, int n) {
    if (n <= 0) { return 0; }
    if (n < 3) { return 1; }
    else if (n == 3) { return first + second; }
    else { return fibonacci(second, first + second, n - 1); }
}
```
测试耗时：比优化前的耗时少了很多

```cpp
#include <iostream>
#include <chrono>
#include <thread>
using namespace std;
using namespace chrono;
int fibonacci_3(int first, int second, int n) {
    if (n <= 0) { return 0; }
    if (n < 3) { return 1; }
    else if (n == 3) { return first + second; }
    else { return fibonacci_3(second, first + second, n - 1); }
}

void time_consumption() {
    int n;
    while (cin >> n) {
        milliseconds start_time = duration_cast<milliseconds >(
            system_clock::now().time_since_epoch()
        );
        fibonacci_3(0, 1, n);
        milliseconds end_time = duration_cast<milliseconds >(
            system_clock::now().time_since_epoch()
        );
        cout << milliseconds(end_time).count() - milliseconds(start_time).count()
            <<" ms"<< endl;
    }
}
int main()
{
    time_consumption();
    return 0;
}
```
空间复杂度分析：递归算法的空间复杂度 = 每次递归的空间复杂度 * 递归深度  
每次递归所需的空间都被压到调用栈里（这是内存管理里面的数据结构，和算法里的栈原理是一样的），一次递归结束，这个栈就是就是把本次递归的数据弹出去。所以这个栈最大的长度就是递归的深度。  
此时可以分析这段递归的空间复杂度，从代码中可以看出每次递归所需要的空间大小都是一样的，所以每次递归中需要的空间是一个常量，并不会随着n的变化而变化，每次递归的空间复杂度就是O(1)。  
![递归空间复杂度](https://img-blog.csdnimg.cn/20210412180907476.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R1YW5nX2FuZw==,size_16,color_FFFFFF,t_70)

递归第n个斐波那契数的话，递归调用栈的深度就是n。那么每次递归的空间复杂度是O(1)， 调用栈深度为n，所以这段递归代码的空间复杂度就是O(n)。

例子二：二分查找

```cpp
int binary_search( int arr[], int l, int r, int x) {
    if (r >= l) {
        int mid = l + (r - l) / 2;
        if (arr[mid] == x)
            return mid;
        if (arr[mid] > x)
            return binary_search(arr, l, mid - 1, x);
        return binary_search(arr, mid + 1, r, x);
    }
    return -1;
}
```
时间复杂度：O(logn)  
空间复杂度：每次递归的空间复杂度可以看出主要就是参数里传入的这个arr数组，即O(n)。再来看递归的深度，二分查找的递归深度是logn ，递归深度就是调用栈的长度，那么这段代码的空间复杂度为 n * logn = O(nlogn)。

空间复杂度优化：把arr数组写成全局变量

```cpp
int arr[] = {2, 3, 4, 5, 8, 10, 15, 17, 20};
int binary_search(int l, int r, int n) {
    if (r >= l) {
        int mid = l + (r - l) / 2;
        if (arr[mid] == n)
            return mid;
        if (arr[mid] > n)
            return binary_search(l, mid - 1, n);
        return binary_search(mid + 1, r, n);
    }
    return -1;
}
```
这份代码将arr数组定义为全局变量，而不放在递归循环里，那么每层递归的空间复杂度是O(1)，递归深度为O(logn)，整体空间复杂度为 1 * logn = O(logn)。

### 手动计算时间和空间
- 不同机器不同情况下，得出的结果可能会有所区别
```js
// 时间
let now = Date.now();
fun();
console.log('fun函数用时：', Date.now() - now)

// 空间
// const {Blob} = require('buffer'); // 如果是node环境需要先引入Blob，浏览器则可以直接用
let val = [1, 2, 3]
console.log('val变量占用字节数：', new Blob([val]).size);
```


## 数据结构

### 数据结构比较
- [各种数据结构操作复杂度](https://github.com/trekhleb/javascript-algorithms/blob/master/README.zh-CN.md#%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E6%93%8D%E4%BD%9C%E7%9A%84%E5%A4%8D%E6%9D%82%E6%80%A7)

- 评判依据
  - 性能：增删查改、遍历
  - 使用场景
  - 逻辑是否简易（一般可以通过熟练度克服）
  - 功能是否强大
  - ...

- 数组
  - 优点：查改、简易
  - 缺点：增删
  - 变种：
    - 栈：后进先出场景
    - 队列：先进先出场景

- 对象
  - 优点：增删查改、简易强大
  - 缺点：遍历不按顺序（可先转为map）、
  - 变种：
    - 链表
    - 树
    - 图

- 链表
  - 优点：增删
  - 缺点：查改

### 栈
- 特点：后进先出
- 应用场景：需要后进先出的场景
  - 十进制转二进制
  - 计算器支持表达式计算
  - 判断字符串中的括号是否有效
  - 函数调用堆栈
- JS 实现
  ```js
  // 定义
  let stack = [];
  // 增：入栈
  stack.push(1);
  // 删：出栈
  stack.pop();
  // 查：栈顶
  let top1 = stack.pop();
  let top2 = stack[stack.length - 1]; // 长度为0时,undefined
  // 改：栈顶
  stack[stack.length - 1] = 2;
  // 遍历：同数组遍历，例如
  for(let item of stack) { console.log(item) }
  ```
- LeetCode 题目
  - [20.有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)

### 队列

- 特点：先进先出
- 场景：需要先进先出的场景
  - 排队
  - JS 异步中的任务队列
  - 计算最近请求次数
- JS 实现
  ```js
  // 定义
  let queue = [];
  // 增：入队
  queue.push(1);
  // 删：出队
  queue.shift();
  // 查：队头队尾
  let head1 = queue.shift();
  let head2 = queue[0];
  let tail = queue[queue.length - 1];
  // 改：队头队尾
  queue[0] = 0;
  queue[queue.length - 1] = 9;
  // 遍历：同数组遍历
  
  ```
- LeetCode 题目
  - [933. 最近的请求次数](https://leetcode-cn.com/problems/number-of-recent-calls/)

### 优先级队列 - 待补充
- [leetcode中默认已经加载，但不推荐用](https://leetcode.cn/circle/discuss/aVs6F0/view/9A0ZLn/)
- [leetcode中的优先级队列的API](https://github.com/datastructures-js/priority-queue)
- [原理](https://labuladong.github.io/algo/di-yi-zhan-da78c/shou-ba-sh-daeca/er-cha-dui-1a386/)
- [实现](https://juejin.cn/post/7045279421334290446)

```js
class PriorityQueue {
  constructor(compare) {
    this.data = [];
    this.compare = typeof compare === "function" ? compare : null;
  }
  // 二分寻找插入位置
  search(target) {
    let low = 0, high = this.data.length;
    while (low < high) {
      let mid = low + ((high - low) >> 1);
      if (this.compare(this.data[mid], target) > 0) {
        high = mid;
      } else {
        low = mid + 1;
      }
    }
    return low;
  }
  push(elem) {
    let index = this.search(elem);
    this.data.splice(index, 0, elem);
    return this.data.length;
  }
  shift() {
    return this.data.shift();
  }
  isEmpty() {
    return this.data.length === 0;
  }
  head() {
    return this.data.length ? this.data[0] : null;
  }
  tail() {
    return this.data.length ? this.data[this.data.length - 1] : null;
  }
}
```

### 链表

- 特点：增删方便
- 场景：
- JS 实现
  ```js
  // 定义链表
  let a = { val: "a" };
  let b = { val: "b" };
  let c = { val: "c" };
  a.next = b;
  b.next = c;
  c.next = null;

  // 增：插入节点
  let b1 = { val: "b1" };
  b.next = b1;
  b1.next = c;

  // 删：删除节点
  b.next = c;

  // 遍历链表
  let p = a;
  while (p) {
    console.log(p.val);
    p = p.next;
  }

  // 链表节点的定义：通常题目会提供
  function ListNode(val, next) {
    this.val = (val===undefined ? 0 : val)
    this.next = (next===undefined ? null : next)
  }
  // 通过数组创建链表
  function createList(arr) {
    let dummy = new ListNode(-1); // 虚拟头节点
    let p = dummy;
    arr.forEach(x => {
      let tmp = new ListNode(x);
      p.next = tmp;
      p = p.next;
    })
    return dummy.next; // 返回虚拟头节点的next
  }
  // 输出链表
  function showList(p) {
    let res = '';
    while (p) {
      res += p.val + ','
      p = p.next;
    }
    console.log(`[${res}]`);
  }
  // 找倒数第n个节点
  const findFromEnd = (head, n) => {
    // 最简单的方法是先遍历一遍得到链表长度len，然后再遍历一遍找到第len - n + 1个节点
    // 用双指针的方法可以只遍历一遍：
    let fast = head;
    let step = n;
    // 先让fast走n步，此时离fast走到链尾还有len - n步
    while(step && fast) {
      fast = fast.next;
      step--;
    }
    // 此时让快慢指针同时前进，当fast走到链尾时，slow刚好走了len - n步
    let slow = head;
    while (fast) {
      fast = fast.next;
      slow = slow.next;
    }
    return slow;
  }


  // 完全体链表：增删查改、双向、虚拟头节点、反转、环、去重、

  ```
- 原型链instanceof实现
- LeetCode 题目
  - [707. 设计链表](https://leetcode.cn/problems/design-linked-list/)
  - [237. 删除链表中的节点](https://leetcode-cn.com/problems/delete-node-in-a-linked-list/)
  - [206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)
  - [2. 两数相加](https://leetcode-cn.com/problems/add-two-numbers/)
  - [83. 删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)
  - [141. 环形链表](https://leetcode-cn.com/problems/linked-list-cycle/)

### 集合
- 特点：唯一且无序
- 场景：
- JS实现
  ```js
  // 新建
  let set1 = new Set();
  // 添加元素
  set1.add(1);
  // 判断是否包含
  let flag = set1.has(1);
  // 删除
  set1.delete(1);
  // 长度
  console.log(set1.size);
  // 遍历
  for (item of set1) console.log(item)
  // 集合转数组
  let arr1 = [...set1]; // 也可以用Array.from(set1)
  // 数组转集合
  let set2 = new Set([1, 2, 3]);
  // 求两个集合的交集
  let interSet = new Set( [...set2].filter( x => set1.has(x) ) )
  let differSet = new Set( [...set2].filter( x => !set1.has(x) ) )

  ```
- LeetCode 题目
  - [349. 两个数组的交集](https://leetcode-cn.com/problems/intersection-of-two-arrays/)

### 字典
- 特点：以键值对存储的数据结构，增删查改方便，键不会重复
- 场景：
- JS实现
  ```js
  // 新建
  let m = new Map();

  // 增
  m.set('a', 'aa');
  m.set(/a|b/g, 'reg');

  // 删除
  m.delete('a');

  // 查
  m.get(/a|b/g);
  m.has('a')

  // 改
  m.set(/a|b/g, 'RegExp');

  // 遍历
  for (let key of m.keys()) {
    console.log(key);
  }

  for (let value of m.values()) {
    console.log(value);
  }
  ```
- LeetCode 题目
  - [349. 两个数组的交集](https://leetcode-cn.com/problems/intersection-of-two-arrays/)
  - [20.有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)
  - [1. 两数之和](https://leetcode-cn.com/problems/two-sum/)
  - [3. 无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)
  - [76. 最小覆盖子串]

### 树
- 特点：分层数据的抽象模型
- 场景：DOM树、树形控件、
- 二叉树的JS实现
```js
// 二叉树节点定义：通常题目会提供
function TreeNode(val, left, right) {
  this.val = (val===undefined ? 0 : val)
  this.left = (left===undefined ? null : left)
  this.right = (right===undefined ? null : right)
}
```
- JS实现（时间复杂度？）
  - 树定义、深度优先遍历、广度优先遍历
    ```js
    // 树的定义
    let tree = {
      val: 'a',
      children: [
        {
          val: 'b',
          children: [
            { val: 'd', children: [] },
            { val: 'e', children: [] }
          ]
        },
        {
          val: 'c',
          children: [
            { val: 'f', children: [] },
            { val: 'g', children: [] }
          ]
        }
      ]
    }
    // 深度优先遍历：
    // 1.访问根节点
    // 2.对根节点的children挨个进行深度优先遍历，递归
    const dfs = (root) => {
      console.log(root.val);
      root.children.forEach(dfs); // 相当于root.children.forEach(child => {dfs(child)});
    }
    dfs(tree); // a b d e c f g

    // 广度优先遍历：
    // 1.新建一个队列，将根节点入队
    // 2.把队头出队并访问
    // 3.把队头的children挨个入队
    // 4.重复2、3步，直到队列为空
    const bfs = (root) => {
      let q = [root];
      while (q.length) {
        let qh = q.shift();
        console.log(qh.val);
        qh.children.forEach((child) => {q.push(child)});
      }
    }
    bfs(tree); // a b c d e f g
    ```

  - 二叉树、先中后序遍历

    ```js
    // 整颗二叉树
    /*
        A
      B     C
    D   E     F
      G
    */
    let btree = {
      val: "A",
      left: {
        val: "B",
        left: { val: "D", left: null, right: null, },
        right: {
          val: "E",
          left: { val: "G", left: null, right: null, },
          right: null,
        },
      },
      right: {
        val: "C",
        left: null,
        right: { val: "F", left: null, right: null, },
      },
    };

    // 先序遍历
    /*
        A1
      B2     C6
    D3   E4     F7
        G5
    */
    // 方法一：递归（根 - 左 - 右）
    // 1.访问根节点
    // 2.对根节点的左子树进行先序遍历
    // 3.对根节点的右子树进行先序遍历
    const preorder = (root) => {
      if (!root) return;
      console.log(root.val);
      preorder(root.left);
      preorder(root.right);
    };
    // preorder(btree);
    // 方法二：循环（通过栈模拟函数递归调用）
    const preorder2 = (root) => {
      if (!root) return;
      let stack = [root];
      while (stack.length) {
        let sh = stack.pop();
        console.log(sh.val);
        // 由于栈后进先出的特性，所以在入栈顺序与递归顺序相反
        if (sh.right) stack.push(sh.right);
        if (sh.left) stack.push(sh.left);
      }
    };
    // preorder2(btree);

    // 中序遍历
    /*
        A5
      B2     C6
    D1   E4     F7
      G3
    */
    // 方法一：递归（左 - 根 - 右）
    // 1.对根节点的左子树进行中序遍历
    // 2.访问根节点
    // 3.对根节点的右子树进行中序遍历
    const inorder = (root) => {
      if (!root) return;
      inorder(root.left);
      console.log(root.val);
      inorder(root.right);
    };
    // inorder(btree);
    // 方法二：循环（通过栈模拟函数递归调用）
    const inorder2 = (root) => {
      if (!root) return;
      const stack = [];
      let p = root;
      while(stack.length || p) {
        while(p) {
          stack.push(p);
          p = p.left;
        }
        const sh = stack.pop();
        console.log(sh.val);
        p = sh.right;
      }
    };
    // inorder2(btree);

    // 后序遍历
    /*
        A7
      B4     C6
    D1   E3     F5
      G2
    */
    // 方法一：递归（左 - 右 - 根）
    // 1.对根节点的左子树进行后序遍历
    // 2.对根节点的右子树进行后序遍历
    // 3.访问根节点
    const postorder = (root) => {
      if (!root) return;
      postorder(root.left);
      postorder(root.right);
      console.log(root.val);
    };
    // postorder(btree);
    // 方法二：循环（通过栈模拟函数递归调用）
    // 思路：由于后序遍历的顺序与先序相反，可以按先序的操作，然后将输出放到另一个栈进行逆序输出
    const postorder2 = (root) => {
      if (!root) return;
      let outStack = [];
      // 借用先序遍历的逻辑
      let stack = [root];
      while (stack.length) {
        let sh = stack.pop();
        outStack.push(sh);
        // 需要将原本被调换的入栈顺序，再调换回来
        if (sh.left) stack.push(sh.left);
        if (sh.right) stack.push(sh.right);
      }
      // 逆序输出
      while(outStack.length) {
        let osh = outStack.pop();
        console.log(osh.val);
      }
    };
    postorder2(btree);
    ```
- LeetCode 题目

### 图
- 特点：网络结构，由边和节点组成；可以表示二元关系
- 表示方法：邻接矩阵、邻接表、关联矩阵等
- JS实现：图的定义；深度、广度优先遍历（时间复杂度？）

```js
// 图的定义（邻接表）
const graph = {
  0: [1, 2],
  1: [2],
  2: [0, 3],
  3: [3],
};

// 图的深度优先遍历
// 1.访问根节点
// 2.对根节点的没有访问过的相邻节点挨个进行深度优先遍历
const visited = new Set();
const dfs = (graph, start) => {
  visited.add(start);
  console.log(start);
  graph[start].forEach((node) => {
    if (!visited.has(node)) {
      dfs(graph, node);
    }
  });
};
// dfs(graph, 2);

// 图的广度优先遍历
// 1.新建一个队列，把根节点入队
// 2.把队头出队并访问
// 3.把队头的没有访问过的相邻节点入队
// 4.重复第二、三步，直到队列为空
const bfs = (graph, start) => {
  const visited = new Set();
  const queue = [start];
  visited.add(start);
  while (queue.length) {
    const head = queue.shift();
    console.log(head);
    // 注意：加入visited的时机是访问后，而不是输出后
    graph[head].forEach((node) => {
      if (!visited.has(node)) {
        queue.push(node);
        visited.add(node);
      }
    });
  }
};
// bfs(graph, 2);

```
- LeetCode 题目

### 堆
- 特点：一种特殊的完全二叉树，所有节点都大于等于（最大堆）、或小于等于（最小堆）它的子节点
- 表示方法：
  - 数组（按层序遍历的顺序存放val）
  - 左侧子节点的位置：2 * parentIndex + 1
  - 右侧子节点的位置：2 * parentIndex + 2
  - 父节点的位置：(childIndex - 1) / 2
- 应用：
  - 高效地找出最大值或最小值 O(1)
  - 找出第K大个最大值或最小值
- JS实现：最小堆类

```js
```
- LeetCode 题目



## 方法技巧

### 排序 - 冒泡/选择/插入
- [各种排序](http://ddrv.cn/docs/SortingAlgorithm/index.html)
- [912.排序数组](https://leetcode.cn/problems/sort-an-array/)

```js
let arr1 = [1, 2, 3, 4, 5];

// 冒泡排序 O(n^2)
// 从头开始比较相邻两个数的值，如果前面的数大于后面的数就交换，直到最后一个数，最后最大的数就冒泡到了最后（内层循环）
// 比较完一轮后，再次从头开始比较相邻两个数的值，直到最后一个没有冒泡过的数，重复n-1轮（外层循环）
Array.prototype.bubbleSort = function () {
  for (let i = 0; i < this.length - 1; i++) {
    for (let j = 0; j < this.length - i - 1; j++) {
      if (this[j] > this[j + 1]) {
        let tmp = this[j];
        this[j] = this[j + 1];
        this[j + 1] = tmp;
      }
    }
  }
  return this; // 如果需要返回的话
};

console.log(arr1.bubbleSort());

// 选择排序 O(n^2)
// 把第一个没有排序过的元素看作最小值，记录minIndex，遍历每个没有排序过的元素，如果遇到更小的元素，则更新minIndex，遍历完后将minIndex对应的元素与第一个没有排序的元素进行交换（内层循环）
// 重复内层循环n-1轮（外层循环）
Array.prototype.selectionSort = function () {
  for (let i = 0; i < this.length - 1; i++) {
    let minIndex = i;
    for (let j = i + 1; j < this.length; j++) {
      if (this[minIndex] > this[j]) {
        minIndex = j;
      }
    }
    // 优化：如果minIndex没有更新过，那就不用交换了
    if (minIndex === i) continue;
    let tmp = this[minIndex];
    this[minIndex] = this[i];
    this[i] = tmp;
  }
  return this;
};
// console.log(arr1.selectionSort());

// 插入排序 O(n^2) 排序小数组的时候性能比上述两种要好

```

### 排序 - 归并排序
- 分而治之思想
  - 分：把数组从中间一分为二
  - 解：递归地对两个子数组进行归并排序，数组长度为1已经有序
  - 合：合并有序子数组
- 时间复杂度：
  - 分：O(logn)
  - 合：O(n)
  - 总：O(n * logn)

```js
Array.prototype.mergeSort = function () {
  // 通过归并排序得到排序后的数组
  const mergeSort = (arr) => {
    // 递归终点：数组长度为1
    if (arr.length === 1) {
      return arr;
    } else {
      // 将数组从中间一分为二
      const mid = Math.floor(arr.length / 2);
      const left = arr.slice(0, mid);
      const right = arr.slice(mid);
      // 对左右两个字数组再进行归并排序
      const orderLeft = mergeSort(left); // 得到有序的左数组
      const orderRight = mergeSort(right); // 得到有序的右数组
      // 合并两个有序数组
      const res = [];
      while (orderLeft.length || orderRight.length) {
        // 不断比较两个有序数组的队头，把较小的推入res
        // 重复直到两个数组为空
        if (orderLeft.length && orderRight.length) {
          res.push(orderLeft[0] < orderRight[0] ? orderLeft.shift() : orderRight.shift());
        } else if (orderLeft.length) {
          res.push(orderLeft.shift());
        } else if (orderRight.length) {
          res.push(orderRight.shift());
        }
      }
      return res; // 返回合并后的有序数组
    }
  };
  // 修改原数组
  const res = mergeSort(this);
  res.forEach((x, i) => { this[i] = x; });
};
// 示例
let arr = [5, 4, 3, 2, 1];
arr.mergeSort();
console.log(arr);

```

### 排序 - 快速排序
- 分而治之思想
  - 分：选基准，按基准把数组一分为二，比基准小的放前面，大的放后面 
  - 解：递归地对两个子数组进行快速排序，数组长度为1已经有序
  - 合：合并有序子数组
- 时间复杂度
  - 分：O(logn)
  - 合：O(n)
  - 总：O(n * logn)

```js
  Array.prototype.quickSort = function() {
    // 快速排序
    const quickSort = (arr) => {
      // 递归终点：数组长度为1或0
      if (arr.length < 2) {return arr}
      // 随机选取基准
      const left = []
      const right = []
      const mid = []
      const randIndex = Math.floor(Math.random() * arr.length)
      const base = arr[randIndex]
      // 比基准小的放在left；大于的放在right
      for (const item of arr) {
        if (item < base) {
          left.push(item)
        } else if (item > base) {
          right.push(item)
        } else {
          mid.push(item)
        }
      }
      // 对left和right递归进行快速排序，最后合并成有序数组 
      return [...quickSort(left), ...mid, ...quickSort(right)]
    }
    // 修改原数组
    const res = quickSort(this)
    res.forEach((x, i) => {this[i] = x})
  }
  // 示例
  let arr = [5,2,3,1];
  arr.quickSort();
  // console.log(arr);
```

### 搜索查找算法
- [待处理](https://xie.infoq.cn/article/996cf8899930ae467cc790035)
- [待处理](https://www.cnblogs.com/maybe2030/p/4715035.html)

### 搜索查找算法 - 二分搜索
- 前提：数组有序
- 思路
  - 分而治之（递归）：[704. 二分查找](https://leetcode.cn/problems/binary-search/)
    - 分：把数组从中间一分为二
    - 解：递归地对包含目标值的子数组进行二分搜索
    - 合：无需合并，在拆分的过程中就可以判断中间元素是否为目标值
  - 循环：[374. 猜数字大小](https://leetcode.cn/problems/guess-number-higher-or-lower/)

```js
  var search = function(nums, target) {
    // 数组长度小于2可以直接比较头元素
    if (nums.length < 2) {
      return nums[0] === target ? 0 : -1;
    }
    // 递归二分搜索
    const binarySearch = (low, high, target) => {
      // 异常处理
      if (low > high) { return -1; }
      // 计算中间坐标，采用防止溢出的算法
      let mid = Math.floor((high - low) / 2 + low);
      if (nums[mid] === target) {
        return mid;
      } else if (nums[mid] > target) {
        return binarySearch(low, mid - 1, target);
      } else {
        return binarySearch(mid + 1, high, target);
      }
    }
    return binarySearch(0, nums.length - 1, target);
  };
```


### 算法设计 - 循环

```js
// 计算x的n次方，0 <= n < 内存限制、时间过长
function pow(x, n) {
  let res = 1;
  // for与while，循环n次的写法
  for (let i = 0; i < n; i++) { res *= x; }
  // while (n) { res *= x; n--; }
  return res;
}

// 倒序输出数组
for (let i = arr.length - 1; i >= 0; i--) {
  console.log(arr[i])
}
```

- 衍生出暴力解法：穷举与循环
  - 优点：直观
  - 缺点：效率低、（繁琐、）


### 算法设计 - 递归
- 场景：
  - 问题可以自然地拆分成多个相同类型但更简单的问题
  - 存在相似的嵌套关系（对象、HTML标签）
  - 倒序遍历
- 要点：递归公式、终止条件
- 优点：
  - 简洁
  - 理解后容易维护
  - 更加简洁地实现倒序遍历（利用了函数调用的堆栈，如果用循环的写法则需要手动开辟一个栈来实现倒序遍历）
- 缺点：
  - 递归深度受引擎限制（可以通过尾调用解决）
  - 递归堆栈比较占内存（递归深度*递归函数空间复杂度）
- 相比循环：
  - 通常情况下循环性能更好，递归更简洁易维护
- 任何递归都可以用循环来重写。但有时重写很难（例如：遍历嵌套关系的对象并且最大嵌套层数未知）
- 递归模板：可以划分出前序位置和后序位置 
```js
// 递归数组
var recursion_arr(arr, index) {
  if (index === arr.length) return;
  // 前序位置
  recursion_arr(arr, index + 1);
  // 后序位置，在此处 console.log(arr[index]) 就可以实现倒序输出数组
}

// 递归链表
var recursion_list(node) {
  if (node === null) return;
  // 前序位置
  recursion_list(node.next);
  // 后序位置，在此处 console.log(node.val) 就可以实现倒序输出链表
}
```

- 递归例子
```js
// 计算x的n次方，0 <= n < JS引擎允许的最大递归深度
function pow(x, n) {
  if (n === 0) {
    return 1; // 终止条件 x^0 = 1
  } else {
    return x * pow(x, n - 1); // 递归公式 x^n = x * x^n-1
  }
  // 递归通常可以更加简洁 return n === 0 ? 1 : x * pow(x, n - 1);
  /* 解析
    pow(x, 3)
    x * pow(x, 2)
    x * x * pow(x, 1)
    x * x * x * 1
  */
}

// 遍历嵌套层数未知的对象：计算公司的所有部门及其子部门的所有员工的工资总和
{
  let company = {
    // 没有子部门为数组
    sales: [{name: 'John', salary: 1000}, {name: 'Alice', salary: 1600 }],
    // 有子部门为对象
    development: {
      sites: [{name: 'Peter', salary: 2000}, {name: 'Alex', salary: 1800 }],
      internals: [{name: 'Jack', salary: 1300}]
    }
  };
  // 递归求工资总和
  function sumSalaries(department) {
    if (Array.isArray(department)) {
      return department.reduce((sum, cur) => {return sum + cur.salary}, 0);
    } else {
      return Object.values(department).reduce((sum, cur) => {return sum + sumSalaries(cur)}, 0);
    }
  }
  console.log(sumSalaries(company)); // 7700
}

{
  // 斐波那契数 https://zh.javascript.info/recursion#fei-bo-na-qi-shu
  function fib(n) {
    // 根据定义可以写出，当 n >= 0
    // return n <= 2 ? 1 : fib(n - 1) + fib(n - 2);
    // 但运行速度很慢，fib(50)就可以卡一段时间；虽然递归深度为n，但是递归次数很多，而且每次都要重新计算重复的fib(x)

    // (记忆化递归) 记住中间计算过的值，避免重复计算
    let record = { 1: 1, 2: 1 };
    const recordFib = (n) => {
      if (n in record) {
        return record[n];
      } else {
        return record[n] = recordFib(n - 1) + recordFib(n - 2);
      }
    };
    return recordFib(n);
  }
  console.log(fib(77));
}

// 循环 & 递归 对比
{
  // 正向输出链表
  function pr(head) { // 头节点 head 不为 null
    const cycle4pr = (head) => {
      let cur = head; // 为了不改变head，需要使用临时变量
      while(cur) {
        console.log(cur.val);
        cur = cur.next;
      }
    }
    const recursion4pr = (head) => {
      console.log(head);
      if (head.next) {
        recursion4pr(head.next); // 递归利用堆栈特性，可以不改变head且不用临时变量
      }
    }
    cycle4pr(head); // 此时循环更优，逻辑清晰，步骤简单，空间占用更少
  }

  // 反向输出链表
  function reversePr(head) {
    const cycle4reversePr = (head) => {
      let arr = []
      let cur = head;
      while(cur) {
        arr.push(cur.val)
        cur = cur.next
      }
      for (let i = arr.length - 1; i >= 0; i--) {
        console.log(arr[i])
      }
    }
    const recursion4reversePr = (head) => {
      if (head.next) {
        recursion4reversePr(head.next)
      }
      console.log(head.val)
    }
    recursion4reversePr(head); // 此时递归更简洁，循环需要额外开辟数组，而递归则利用了堆栈的特性
  }
}
```
- 参考：
  - [js递归](https://zh.javascript.info/recursion)
  - [尾递归](https://www.ruanyifeng.com/blog/2015/04/tail-call.html)
  - [尾递归](https://imweb.io/topic/5a244260a192c3b460fce275)


### 算法设计 - 正则
- 优点：简洁的字符串处理、搜索特定格式的子串
- 缺点：容易出错，不适合过于复杂且规律不明显的字符串，不适合循环嵌套匹配
- [640. 求解方程](https://leetcode.cn/problems/solve-the-equation/)

  
### 算法设计 - 数学公式法
- 场景：问题符合数学公式
- 优点：高效
- 缺点：熟练已有公式、能推导新公式

```js
// 计算 1 + 2 + 3 + ... + n
const sumTo = (n) => {return n / 2 * (n + 1)}
```

### 算法设计 - 双指针
- 类型
  - 快慢
  - 头尾
- leetcode
  - [206. 反转链表](https://leetcode.cn/problems/reverse-linked-list/)

### 算法设计 - 分而治之
- 描述：
  - 分：将原问题分为多个小问题
  - 解：递归解决小问题
  - 合：将结果合并，解决原问题
- 场景
  - 归并排序
  - 快速排序
  - 二分搜索
- leetcode
  - [374. 猜数字大小](https://leetcode.cn/problems/guess-number-higher-or-lower/)

### 算法设计 - 贪心


### 算法设计 - 动态规划
```js
// 自下而上的动态规划
function fib(n) {
  // 斐波那契数 https://zh.javascript.info/recursion#fei-bo-na-qi-shu
  let pre = 1;
  let post = 1;
  // 从最初的两个开始相加，保留最近两位的结果，直到n
  for (let i = 2; i < n; i++) {
    let tmp = post;
    post += pre;
    pre = tmp;
  }
  return post;
}
```

### 算法设计 - 回溯


## 算法解题思路
- 理解题目
  - 分析内在逻辑、情况分类、输入输出
  - 实际场景抽象
  - 尝试公式化简
- 选择数据结构
  - 字符串
  - 数组
  - 链表
  - 栈
  - 队列
  - 字典
  - 二叉树
  - 堆
  - 图
  - 哈希表
- 选择算法技巧
  - 暴力解法
  - 数学公式法
  - 正则匹配
  - 排序系列算法 / 搜索系列算法
  - 双指针
  - 前缀和/差分数组
  - 回溯
  - 动态规划
  - dfs/bfs
- 书写 & 调试代码
- 复杂度分析
- 代码优化：常见于暴力解法不通过，需要利用算法技巧进行优化