# Big O Notation & Logarithm 對數

* [Complexity：Asymptotic Notation(漸進符號)](http://alrightchiu.github.io/SecondRound/complexityasymptotic-notationjian-jin-fu-hao.html)

## Outline
* Why use Big O?
* Asymptotic Notation 漸進符號
* Big O Notation
  Space Complexity 空間複雜度、Time Complexity 時間複雜度
  * Complexity 複雜度
  * Drop the Contents and Non-Dominant Terms ~~丟掉~~刪除常量及非主導項
  * 小結
* 實際案例
  * O(1)
  * O(n)
  * Multi-Part Algorithms: Add vs. Multiply 複合演算法
  * Amortized Time 平攤時間
  * Log(n)
  * Recursive Runtimes 遞迴運行
* 練習 (16題)

## Why use Big O?
當我們需要比較每個演算法的成本時，我們會將每個演算法的工作效率透過函數轉換**複雜度 ( Complexity )**。而在評估演算法的複雜度時，通常使用**漸進符號 ( Asymptotic Notaion )** 來評估。

舉個例子，當你想要在家看某部影片時，你可能有兩種取得影片的方式：租 DVD 或是在網路上下載。這兩個動作的成本大致如下：

* 網路上下載 ( `O(n)` )：`n` 代表文件大小，因為下載的時候傳輸時間會隨著影大小線性增加
* 租 DVD ( `O(1)` )：即便考慮到影片大小，除非數量太多，否則止需要出門一次去拿

因此：

* Big O 代表了某些成本(包含運算時間與記憶體空間)，通常會和「待處理的資料量」有關，當資料量越大，成本會以某種關係 ( 線性、指數等等 ) 跟著提高。

* 當資料量大時，演算法的效率很重要。

## Asymptotic Notation 漸進符號
有 5 種線性符號：

* `O` − Notation，Big-O
一般談論的演算法之複雜度，經常是指Big-O，因為在估算成本時，最想知道的是「上界 ( upper bound )」。簡單來說，就是指「最差」的情況所花費的成本。
<br/>

* `Ω` - Notation，Big-Omega
若想知道某個演算法「至少」需要多少時間時，便可以Big-Omega來估算「下界(lower bound)」。跟 `O` 相反，希望獲得「最好」的情況所花費的成本。
<br/>

* `Θ` −Notation，Big-Theta
  所有能夠描述演算法趨勢的「函數之集合」。也就是說如果複雜度既是 `O(n)` 也是 `Ω(n)`，擇其函式算法可以被視為 `Θ(n)`。

## Big O Notation
Big O 是幫助我們描述某個操作花費的成本，包括：
* **時間複雜度 Time Complexity**
主要用來衡量演算法的速度。
<br/>

* **空間複雜度 Space Complexity**
衡量演算法占用多少輔助內存。

Big O notation 使用傳入的變量表示大小，例如：
1. **O(n)** 可以是遍歷一個長度為 **n** 的陣列所需的時間複雜度
2. **O(n + m)** 也有可能是變歷某個長度為 **n**、集合內的每個個字串的長度為 **m** 的陣列。
<br/>

### Complexity 複雜度
###### 範例 1
下面的這個遞迴 ( recursive ) 將會花費 `O(n)` 的時間複雜度以及 `O(n)` 的空間複雜度。

```java
/* Ex. 1 */
int sum(int n ){
  if(n <= 0){
    return 0;
  }

  return n + sum(n-1);
}
```

根據執行的順序，假設我們呼叫 `sum(4)`，那麼記憶體中的堆疊棧 ( stack ) 將會長的像下面這樣，每個調用 ( call ) 都會被放到 stack 中：
```
1 sum(4)
2   -> sum(3)
3     -> sum(2)
4       -> sum(1)
5         -> sum(0)
```

上面的例子是因為調用了 `n` 次，所以它的空間複雜度是 `O(n)`。

**但!!! However!!! しかし!!!**

**不代表只要調用 `n` 次，它實際所花的空間複雜度就是 `O(n)`。**

讓我看再來看看第二個例子：

###### 範例 2
```java
/* Ex. 2 */
int pairSumSequence(int n){
  int sum = 0;

  for(int i = 0; i < n; i++){
    sum += pairSum(i, i + 1);
  }
  return sum;
}

int pairSum(inta, intb){
  return a + b;
}
```

對於 `pairSum()` 來說，它會被調用 `O(n)` 次，但這些調用並不會同時存在於 stack 中，所以它的空間複雜度是 `O(1)`。


### Drop the Contents and Non-Dominant Terms ~~丟掉~~刪除常量及非主導項
在這些複雜度的表示中，其實不不會看到 `O(2n)` 或是 `O(5)` 的複雜度。對於特定的輸入，像是複雜度為 `O(n)` 的程式碼很有可能較 `O(1)` 的程式碼更有效率。

所以我們真正關心的是，**當處理的資料量 `n` 變大時，程式運行時需要花費成本的增長量**，可以想像成當 `n → ∞` 時最差需要花費多少的時間以及空間複雜度。

舉個例子來說，有一個 f(n) = 2n<sup>2</sup> + 6n + 1，當 `n` 增加時，其實後面的 6n + 1 對我們來說就不是非常的重要，因為我們要的是"最差"的情況，只需要看 2n<sup>2</sup> 的部分。

接下來，同理，當 `n` 增加， f(n) = 2n<sup>2</sup> 中的常數 2，跟 n x n<sup>2</sup> 比較，它也不是影響增長量的關鍵因素，所以也可以捨去。

###### 範例 3
比較下面兩組程式碼，哪一個執行更快?

```java
/* first */
int min = Integer.MAX_VALUE; 
int max = Integer.MIN_VALUE; 

for (int x ： array) {
  if (x < min) min x; 
  if (x > max) max = x;
}
```

```java
/* second */
int min = Integer.MAX_VALUE; 
int max = Integer.MIN_VALUE; 

for (int x ： array) {
  if (x < min) min x; 
}

for (int x ： array) {
  if (x > max) max = x;
}
```
* 第一個因為只跑了一個迴圈，所以其複雜度為 `O(n)`
* 第二個因為跑了兩次的迴圈，其複雜度為 `O(2n)`

不過這也不代表 `O(n)` 一定比 `O(n^2)` 來得有效率。

### 小結
以下是常見的 Big O notation，由最快到最慢的順序為： 

* **Constant**：O(1)<br/>
* **Logarithmic**：O(log(n))<br/>
* **Linear**：O(n)<br/>
* **Log-linear**：O(nlog(n))<br/>
* **Quadratic**：O(n<sup>2</sup>)<br/>
* **Cubic**：O(n<sup>3</sup>)<br/>
* **Exponential**：O(2<sup>n</sup>)<br/>
* **Factorial**：O(n!)<br/>

![](/images/DataStructure/3-1.png)

[圖片來源](http://alrightchiu.github.io/SecondRound/complexityasymptotic-notationjian-jin-fu-hao.html)
<br/>

想要知道其他的時間複雜度，可以參考：
* [Big O Cheat Sheet](https://www.hackerearth.com/practice/notes/big-o-cheatsheet-series-data-structures-and-algorithms-with-thier-complexities-1/)

![](/images/DataStructure/3-3.png)

## 實際案例
### O(1)
> 為何是 O(1)? 1 代表什麼意思?


```java
int array = new int[] {1, 2, 3};

// 取得特定 index 的成本為 O(1)
int x = array[1];
```

### O(n)
```java
// 將資料放入一個長度為 5 的陣列，其時間複雜度為 O(n)
// 因為根據陣列長度 n 影響成本
int[] array = new int[5];

for(int i = 0; i < 4; i++){
  int[i] = i;
}
```

### Multi-Part Algorithms: Add vs. Multiply 複合演算法
假設有一個分為兩個步驟的演算法，什麼情況下需要乘上 runtimes 成本而什麼時候需要相加呢?下面提供了一些範例。

###### O(A + B)
```java
for(int a : arrA){
  print(a);
}

for(int b : arr B){
  print(b);
}
```

###### O(A * B)
```java
for(int a : arrA){
  for(int b : arr B){
    print(a + "," + b);
  }
}
```

### Amortized Time 平攤時間
首先必須知道：
* Array 的長度一旦被用完，就需要重新手動建立一個新的更長的 Array 來裝資料
* ArrayList 則是在資料裝滿後，會由底層的機制自動擴展長度

![](/images/DataStructure/3-4.png)

所以以一個 ArrayList 來說：
* 建立一個長度為 `n` 的 ArrayList，最終所需的空間複雜度為：
  ```
  O(1) + O(2) + O(4) + O(8) + ... + O(n)
  ```

* 但由於不是每一塞資料都需要複製原本的資料再放到新的資料結構當中，所以由初始長度為 `1` 的陣列到長度為 `n` 的陣列，其平均的花費成本為：
  ```
  n + n/2 + n/4 + n/8 + ... 1 ≈ n
  ```

```java
List list = new ArrayList<>();

for(int i = 0; i < 4; i++){
  list.add(i);
}
```

### Log(n)
平常看到的 `O(log n)` 是怎麼來的?

以二元搜尋數為例，在二元搜尋法中，想要在 `n` 有序元素中查找元素 `x`，首先會先找出該元素中找出中位數 ( middle )，接著判斷：

```java
if(x == middle) {
  return x;

} else if(x < middle>) {
  // 往 tree 的左半部搜索
} else {
  // 往 tree 的右半部搜索
}
```

示意圖：
![](/images/DataStructure/3-5.png)


```
search 9 within {1, 5, 8, 9, 11, 13, 15, 19, 21} 
	compare 9 to 11 -> smaller.
	search 9 within {1, 5, 8, 9, 11}
		compare 9 to 8 -> bigger
		search 9 within {9, 11}
			compare 9 to 9
			return
```

也就是每往下一步，需要搜尋的元素就會剩下 `n/2`，再往下一步就會變成 `n/4`。當找到目標值或是只上下最後的 leaf node 時就會停止。所以總運行時間取決於我們執行多少次往下尋找的步驟，直到 `n` 變為 `1`。

```
N = 16
N = 8 	/* divide by 2 */ 
N = 4 	/* divide by 2 */ 
N = 2 	/* divide by 2 */ 
N = 1 	/* divide by 2 */ 
```

反過來看，也就是幾個階層可以由 `2` 到達 `n`，每一個階層增加的量都是兩倍。這個就等同於 log 的定義 `log₂(n)`。

```
N = 1 
N = 2 	/* multiply by 2 */
N = 4 	/* multiply by 2 */
N = 8 	/* multiply by 2 */
N = 16 	/* multiply by 2 */
```

> p.s. 在計算機科學中，log 的底數是 2 而不是 10

### Recursive Runtimes 遞迴運行
這段程式碼的複雜度是多少呢?

```java
int f(int n) {
  if (n <= 1) {
    return 1;
  }
  return f(n - 1) + f(n - 1);
}
```

假設我們現在調用 `f(4)`，那麼它被調用的 stack 大致上可以畫成下面這樣。

![](/images/DataStructure/3-6.png)

這個 Tree 的深度為 `n`，每個 node 有兩個子節點 ( 因為被調用兩次 )，所以每一層調用的次數都是上一層的兩倍。

![](/images/DataStructure/3-7.png)

即每一次的調用結果，均為下一層的調用結果乘以 2。因此共有 2<sup>0</sup> + 2<sup>1</sup> + 2<sup>3</sup> + 2<sup>4</sup> + ... + 2<sup>n</sup> ( = 2<sup>n + 1</sup> - 1  個節點 )

在這個情況下我們可以得到 `O(2^n)`。

不過該算法的空間複雜度其實是 `O(n)`，因為雖然我們在樹中總共有 `O(2n)` 個節點，但在搜尋時實際上只會走其中一條，其複雜度為 `O(n)`。

---
## Practice 練習

###### Ex.3
```java
void printUnorderedPairs(int[] array) {
  for (int i = 0; i < array.length; i++) {
    for (int j = i + 1; j < array.length; j++) {
      System.out.println(array[i] + "," + array[j]);
    }
  }
}
```
![](/images/DataStructure/3-8.png)

Ans. O(n<sup>2</sup>)

###### Ex.4
```java
void printUnorderedPairs(int[] arrayA, int[] arrayB) {
  for (int i = 0; i < arrayA.length; i++) {
    for (int j = 0; j < arrayB.length; j++) {
      if (arrayA[i] < arrayB[j]) {
        System.out.println(arrayA[i] + "," + arrayB[j]);
      }
    }
  }
}
```
Ans. O(n*m)

###### Ex.7
Which of the following are equivalent to O(n)? Why?
(A) `O(n + p), where p < n/2`
(B) `O(2n)`
(C) `O(n + log n)`
(D) `O(n + m)`

Ans. (A)(B)(C)

(D) 則是因為 `m` 跟 `n` 沒有顯著關係，所以 `m` 仍然要留著。

###### Ex.8
假設我們現在要對一個陣列內單獨每個字串排序，再對這個陣列進行排序，整體的運行時間是多少?

```
['apple', 'elephant', 'banana']

['aelpp', 'aeelhntp', 'aaabnn']

['aaabnn', 'aeelhntp', 'aelpp']
```

不少人應該會這樣回答：
* 對陣列中每個字串進行排序：`O(n log n)`，所以整體排序間應該是 `O(n*n log n)`
* 對陣列進行排序：`O(n log(n))`

因此總時間應該是 `O(n*n log n + n log n)` = `O(n*n log n)`。

不過由於不確定陣列內的字串長度與陣列長度是否一樣，所以建議用不同的代號區分。像是 `s` 代表字串長度，`a` 代表陣列長度，所以整體而言其運行時間應該是 `O(a*s (log a + log s))`。

###### Ex.9
```java
int sum(Node node) {
  if (node == null) {
    return 0;
  }
  return sum(node.left) + node.value + sum(node.right);
}
```

原本的 Binary Tree 操作時間為 `log n`，如下。
![](/images/DataStructure/3-11.png)

但因為上面的程式碼需要取得左右兩邊子節點的值相加，所以等於是遍歷了整顆 Tree。

不懂的可以看這段簡單的[影片](https://www.youtube.com/watch?v=b060MHQwUEE)xD

###### Ex.10
假設要檢查一個數字是不是質數，可以像下面這樣做：
```java
boolean isPrime(int n) {
  for (int x = 2; x * x <= n; x++) {
    if (n % X == 0) {
      return false;
    }
  }
  return true;
}
```

例子一：
```
assume n = 15

x = 2
  15 % 2 = 1
x = 3 
  15 % 3 = 0
  return false 
```

例子二：
```
assume n = 17

x = 2
  15 % 2 = 1
x = 3 
  15 % 3 = 2
x = 4
  17 % 4 = 1
x = 5
  因超過 for loop 限制，loop 結束
  return true;
```

實際上我們只會花 `O(√n)` 處理。

###### Ex.11
```java
int factorial(int n) {
  if (n < 0) {
    return -1;
  } else if (n == 0) { 
    return 1;
  } else {
    return n * factorial(n - 1);
  }
}
```

![](/images/DataStructure/3-9.png)

後一個的值等於是前面的已知值相加，按照此推法，想要知道 `f(3)` 就要先知道 `f(1)` 和 `f(2)` 是多少，同理想要知道 `f(n)` 是多少，就要先跑 `n-1` 次來獲得 `f(n-1)` 的值。

所以其運行時間為 `O(n)`。

###### Ex.12

###### Ex.13
Nth Fibonacci number ( 費式數列 )。
```java
int fib(int n) {
  if (n <= 0) {
    return 0;
  } else if (n == 1) {
    return 1; 
  }

  return fib(n - 1) + fib(n - 2);
}
```

要知道 `fib(n)` 需要先知道 `fib(n - 1)` 和 `fib(n - 2)`。而 `fib(n - 1)` 和 `fib(n - 2)` 也各自需要 `fib(n - 2) + fib(n - 3)` 和 `fib(n - 3) + fib(n - 4)`，等於說想知道某一個階層的值需要花費兩次的成本呼叫函式。

![](/images/DataStructure/3-9.png)

所以其整體成本為 `O(2^n)`。

可參考[淺談演算法複雜度與費波那契數列](https://tw.coderbridge.com/series/cfe509b1adfd4b02ac1c0705ff28c28c/posts/d1b8cecacb774b3e90307f8e8813ab33)

###### Ex.15
費波那契數列演算法的優化，使用 cache。

```java
void allFib(int n) {
  int[] memo = new int[n + 1];
  for (int i = 0; i < n; i++) {
    System.out.println(i + "： " + fib(i, memo));
  }
}

int fib(int n, int[] memo) {
  if (n <= 0) return 0;
  else if (n == 1) return 1;
  else if (memo[n] > 0) return memo[n];

  memo[n]= fib(n - 1, memo) + fib(n - 2, memo);
  return memo[n];
}
```
因只需要遍歷一次即可從 cache 中拿到想要的值，因此為 `O(n)`。

###### Ex.16
```java
int powers0f2(int n) {
  if (n < 1) {
    return 0;
  } else if (n == 1) {
    System.out.println(1);
    return 1;
  } else {
    int prev = powers0f2(n / 2); 
    int curr = prev * 2; 
    System.out.println(curr); 
    return curr;
  } 
}
```
```
powers0f2(50)
	-> powers0f2(25)
 		-> powers0f2(12)
			-> powers0f2(6)
				-> powers0f2(3)
					-> powersOf2(1)
						-> print & return 1 
					print & return 2
				print & return 4 
			print & return 8
		print & return 16 
	print & return 32
```

說明大概就像是下面這樣，所以是 `O(log n)`。

![](/images/DataStructure/3-10.png)

## 重點整理
* Big O notation 通常是用來描述 **最壞 ( worst-case )** 狀況下所需的成本。

---

## Logarithm 對數 (補充)
* 在一般數學而言，對數的定義是 ：
**log<sub>b</sub>(x) = y** if and only if **b<sup>y</sup> = x**
<br/>

* 在計算機科學中，Log 是以 2 為以底數，而非 10。也就是以以下定義為主：
**log(n) = y** if and only if **2<sup>y</sup> = n**
<br/>

* 簡單來說，當某個演算法具有對數時間複雜度 ( logarithmic time complexity )  **(O (log(n))**，其中 **n** 為輸入的變數 )，**n** 變成兩倍，對其而言所需的操作僅僅只是加上了一次。
  
  $2^4 = 16$ &rArr; $log(16) = 4$
  將 $16 * 2$ 後得到 32，取對數 $log(32) = 2^4 * 2$ 的結果是 5，僅僅只多加了一次

  ![](images/3-2.png)
<br/>

* 反之，若演算法具有線性時間複雜度，**n** 同樣變為兩倍，所需的時間很有可能是 **n**。
<br/>

* 具有對數時間複雜度，其效率會比線性時間複雜度高。
