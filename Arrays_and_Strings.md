# Arrays_and_Strings
### Hash 

 「Hash」是一種「演算法的概念」，而「Hashtable」與「HashMap」則是一種與「Hash」相關的資料結構實作。
 

「Hash」就是一個將東西切碎後再重新拼湊的過程。
就資料結構的來說就是：將原資料經過散列處理後，再拼湊成新的資料。

### Hash Tables(雜湊表)
是透過<font color=#FF6600>`雜湊函式(Hash Function)`</font>來計算出一個<font color=#FF6600>`鍵(key)`</font>與<font color=#FF6600>`值(value)`</font>所對應的位置，進而建立雜湊表格，而後也能夠過雜湊函式來搜尋找出鍵值存放在表格的位置。由於動作都需要先經由雜湊函式來執行，若不被知道雜湊函式情況下，保密性就極高，因此很常被應用在<font color=#FF6600>`加密`</font>、<font color=#FF6600>`解密`</font>、<font color=#FF6600>`壓縮`</font>、<font color=#FF6600>`驗證`</font>等領域。

Hash Table 是儲存 (key, value) 這種 mapping 關係的一種資料結構
![](https://i.imgur.com/nM6XGeZ.png)


#### 雜湊表一些專有名詞
<font color=#0000FF>`桶(Bucket)`</font> : 雜湊表中儲存資料的位置，每一個位置對應唯一位址(Bucket Address)。
<font color=#0000FF>`槽(Slot)`</font> : 每一個桶中的資料欄位，例如：一筆資料有2個欄位，則代表桶中有2個槽。
<font color=#0000FF>`碰撞(Collision)` </font>: 若2筆資料經過雜湊函數運算後的雜湊值相同，也就是對應到相同位址時，稱為碰撞。
<font color=#0000FF>`溢位(Overflow)`</font> : 資料經過雜湊函數運算後，雜湊值所指向的桶位址已滿，無法再儲存，稱為溢位。

#### Hash Table 的核心概念
1.快速索引通常只需要 O(1)的時間就可以索引到
2.降低記憶體空間浪費

#### 時間複雜度低原因:
因為 hash function 的關係，如果先把 n 個數字儲存在 Hash Table 裡面，那如果要判斷這個數字 A 是不是已經被存在 Hash Table 裡面，只要先把這個數字丟進 hash function，就可以直接知道 A 對應到 Hash Table 中哪一格。

#### Hash Table的優勢
主要優點: 執行insert/search/delete/modify的時間複雜度皆為O(1)，也就是不管資料量多大都超級快。

或者，我們可以使用<font color=#0000FF>`二元搜尋(Binary Search)`</font>來實現 hash table。這種方法的查找時間為 O(log N)

 (但當Hash Collision(碰撞)發生時，上面的優點不成立，如果衝突的數量非常高，他會去遍歷找到有空位的地方，所以最壞的情况所需的時間是 O(N) )。
![](https://i.imgur.com/Nxqn7yL.png)



##### 題目練習
給一個陣列nums和一個目標數target，陣列中僅有一組數字兩兩相加會等於target，需要回傳這組數字的位置。

舉例：如果輸入 nums = [2,10,1, 7, 6,11] target = 9，會回傳[0,3]

解題的思維：用一層迴圈，從第一個數字開始，到hash table找找看有沒有和這個數字相加起來等於target的值？如果有，就回傳這兩個值的陣列位置。

[LeetCode 1.Two Sum](https://leetcode.com/problems/two-sum/)
``` java 
import java.util.Hashtable;
class Solution {
    public int[] twoSum(int[] nums, int target) {
       int[] res = new int[2];
    Hashtable<Integer,Integer> ht = new Hashtable<>();
    for(int i = 0; i < nums.length; i++){
        if(ht.containsKey(target-nums[i])){
            res[0] = i;
            res[1] = ht.get(target-nums[i]);
            return res;
        }
        ht.put(nums[i],i);
    }  
    return res;
    }
}
```
參考文件 : [[資料結構]-雜湊表Hash Table](https://ithelp.ithome.com.tw/articles/10268077?sc=iThelpR)

# ArrayList & 可擴容組數
### ArrayList
ArrayList的平攤插入運行時間是 O(1)



| 序號 | 1| 2 |3 | 4 | 5 |6 | 7 |8 | 9 | 10 |
| --- | --- | --- |--- | --- | --- |--- | --- |--- | --- | --- |
| 容量     | 1  | 2 |4  | 4  | 8  |8  | 8 |8  | 16  | 16  |
| 花費時間 |1+0| 1+1 |1+2 |1+0 |1+4|1+0 |1+0 |1+0|1+8| 1+0|

![](https://i.imgur.com/dn3nxUE.png)

插入N个元素的複製總數大致為 N/2 + N/4 + N/8 + ... + 2 + 1，剛好小於 N。
加上必須有的每次插入的時間複雜度：O ( n )
這是插入n個數據，那麼對於每一次插入數據，時間複雜度是O ( 1 )
```java 
1 	Arraylist<String> merge(String[] words, String[] more) {
2 		Arraylist<String> sentence = new Arraylist<String>();
3 		for (String w : words) sentence.add(w);
4 		for (String w : more) sentence.add(w);
5 		return sentence;
6 	}
```
(↓我自己要看的，我理解能力比較差><)
```java 
// 平攤時間
		List<String> list =new ArrayList<>();
		// 每次插入的時間都是為O(1)
		// array的空間預設為10 
		// _ _ _ _ _ _ _ _ _ _10　　(空間)
		list.add("1"); // O(1) (10*1/10)
		list.add("2"); // O(1)
		list.add("3"); // O(1)
		list.add("4"); // O(1)
		list.add("5"); // O(1)
		list.add("6"); // O(1)
		list.add("7"); // O(1)
		list.add("8"); // O(1)
		list.add("9"); // O(1)
		list.add("10"); // O(1)
		
		// 假設今天要加入第 11 個 list.add("11");
		// step 1 先複製前一個空間大小 
		// _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 20　　(空間)
		// 1 2 3 4 5 6 7 8 9 10 _ _ _ _ _ _ _ _ _ _
		// step 2 要先把前面的10個值寫到新的陣列裡面 準備時間會是 O(10) 

		list.add("11"); // O(1)
		// 所以加入11 準備時間就會是O(10)+O(1)
```



### StringBuilder
1.String 
在java中String是不可變的，也就是當你創建一個string後是不能修改的，如果你需要給他加內容，java會重新創一個新的實例。這樣的問題就是如果使用s+=a,這樣時間複雜度是O(n),在java中會重新複製一遍string再給你創建。


第一次迭代需要複製 x 個字。第二次迭代需要複製 2x 個字。第三次迭代需要 3x，以此類推。因此總時間是 O(x + 2x + … + nx)。可以簡化成 O(xn^2)。
|為什麼是 O(xn^2)？因為 1 + 2 + ... + n​ 等於 n(n+1)/2，或寫為 O(n^2)。

```java
1 	String joinWords(String[] words) {
2 		String sentence = "";
3 		for (String w : words) {
4 			sentence = sentence + w;
5		}
6 		return sentence;
7 	}
```

2.StringBuilder
StringBuilder 只是創建一個包含所有字串的可調整大小的陣列，只有在必要時才將它們複製回字串。

複雜度分析：

時間複雜度：遍歷使用 O(N) ，每輪添加（修改）字操作使用 O(1)；

空間複雜度 O(N) ：Java 新建的 StringBuilder 都使用了線性大小的額外空間。
```java
String joinWords(String[] words) {
		StringBuilder sentence = new StringBuilder();
 		for (String w : words) {
 			sentence.append(w);
		}
 		return sentence.toString();
 	}
```
![](https://i.imgur.com/hOCLREG.png)
![](https://i.imgur.com/Dhmpioq.png)
``` JAVA
Runoob..
Runoob..!
Runoob..Java!
RunooJava!
```

#### 題目練習
-------------------
1.1 是否唯一（Is Unique）：實現一個算法來確定一個字符串中所有字符是否是唯一的。如果不能使用其他數據結構怎麼辦？
```java
public int firstUniqChar(String s) {
        int result = s.length();
        for (char c = 'a'; c <= 'z'; c++) {
            int i = s.indexOf(c);
            if (i != -1 && i == s.lastIndexOf(c)) {
                result = Math.min(result, i);
            }
        }
        return result == s.length() ? -1 : result;
    }
```
**練習題型** : [LeetCode 387. First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/)

1.2 檢查全排列（Check Permutation）：給定兩個字符串，編寫一個方法來確定其中一個是否是另一個的全排列。
listen
silent
```JAVA
public boolean CheckPermutation(String s1, String s2) {
        char[] c1=s1.toCharArray();
        Arrays.sort(c1);
        char[] c2=s2.toCharArray();
        Arrays.sort(c2);
        return new String(c1).equals(new String(c2));
    }
```
**練習題型** :[面试题 01.02. 判定是否互为字符重排](https://leetcode.cn/problems/check-permutation-lcci/)
**練習題型** :[LeetCode 567. Permutation in String](https://leetcode.com/problems/permutation-in-string/)


1.3 URL化（URLify）：編寫一個方法，用 '%20' 替換字串中的所有空格。你可以假設字串在末尾有足夠的空間來容納額外的字串，並且給定了字串的“真實”長度。 （注意：如果用 Java 實現，請使用字串陣列，以便可以在原來的空間（in place）執行此操作。）

EXAMPLE

```
Input: "Mr John Smith    ", 13
Output: "Mr%20John%20Smith"
```
使用StringBuilder解決，逐漸遍歷字串中的字，如果不是空格就把當前字加入到StringBuilder中，如果是字就把"%20"加入到StringBuilder中
```java
    public String replaceSpaces(String S, int length) {
        StringBuilder stringBuilder = new StringBuilder();
        //逐渐遍历字符串
        for (int i = 0; i < length; i++) {
            //如果不是空格就加入到StringBuilder中，如果是空格
            //就把"%20"加入到StringBuilder中
            char ch = S.charAt(i);
            if (ch == ' ') {
                stringBuilder.append("%20");
            } else {
                stringBuilder.append(ch);
            }
        }
        return stringBuilder.toString();
    }

```
**練習題型** :[面试题 01.03. URL化](https://leetcode.cn/problems/string-to-url-lcci/)
**練習題型** :[LeetCode 1592. Rearrange Spaces Between Words](https://leetcode.com/problems/rearrange-spaces-between-words/)

- 用StringBuilder可以



1.4 回文全排列（Palindrome Permutation）：給定一個字符串，編寫一個函數來檢查它是否是回文全排列。回文是指一個前後相同的單詞或短語。全排列是字母的重新排列。回文不需要局限於字典中的單詞。

EXAMPLE

```Input: Tact Coa
Output: True (permutations: "taco cat", "atco eta", etc.)
```
```java
  public boolean canPermutePalindrome(String s) {
        HashMap<Character, Integer> dic = new HashMap<>();
        for (int i = 0; i < s.length(); i++) {
            dic.put(s.charAt(i), dic.getOrDefault(s.charAt(i), 0) + 1);
        }
        int odd = 0;
        for (int val : dic.values()) {
            if (val % 2 == 1) {
                if (++odd > 1)
                    return false;
            }
        }
        return true;
    }
```
**練習題型** :[面试题 01.04. 回文排列](https://leetcode.cn/problems/palindrome-permutation-lcci/solution/mian-shi-ti-0104-hui-wen-pai-lie-ha-xi-b-yiks/)
**練習題型** :[LeetCode 125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)


1.5 差一步（One Away）：可以對字符串執行三種類型的編輯：插入字符，刪除字符或替換字符。給定兩個字符串，編寫一個函數來檢查它們是否相距一步編輯（或零步編輯）。

EXAMPLE

```pale, ple -> true
pales, pale -> true
pale, bale -> true
pale, bake -> false
```
```java
public boolean areAlmostEqual(String s1, String s2) {
        List<Integer> l = new ArrayList<>();
        for (int i = 0; i < s1.length(); i++) {
            if (s1.charAt(i) != s2.charAt(i)) l.add(i);
			if (l.size() > 2) return false; // added this line to short circuit the loop
        }
        return l.size() == 0 || (l.size() == 2
                                 && s1.charAt(l.get(0)) == s2.charAt(l.get(1))
                                 && s1.charAt(l.get(1)) == s2.charAt(l.get(0)));
    }
```
**練習題型** : [LeetCode 1790. Check if One String Swap Can Make Strings Equal](https://leetcode.com/problems/check-if-one-string-swap-can-make-strings-equal/)

1.6 字符串壓縮（String Compression）：實現一種方法，使用重複字符的計數執行基本的字符串壓縮。例如，字符串 aabcccccaaa 將變為 a2blc5a3。如果“壓縮”後的字符串長度不會變得小於原始字符串的長度，那麼你的方法應該返回原始字符串。你可以假設該字符串僅包含大寫和小寫字母（a ~ z）。
**練習題型** :[LeetCode 443. String Compression](https://leetcode.com/problems/string-compression/)


1.7 旋轉矩陣（Rotate Matrix）：給定一個由 NxN 矩陣表示的圖像，其中圖像中的每個像素為 4 字節，請編寫一種將圖像旋轉 90 度的方法。你能做到嗎？
**練習題型** :[LeetCode 48. Rotate Image](https://leetcode.com/problems/rotate-image/)


1.8 零矩陣（Zero Matrix）：編寫這樣一個算法，如果MxN矩陣中的元素為 0，則使其整個行和列均設置為 0。
**練習題型** :[LeetCode 73. Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/)


1.9 字符串旋轉（String Rotation）：假設你有一個 isSubstring 方法，該方法是檢查一個單詞是否是另一個單詞的子字符串。給定兩個字符串 s1 和 s2，編寫代碼以僅調用一次 isSubstring 來檢查 s2 是否是 s1 的旋轉（例如，“waterbottle” 是 “erbottlewat” 的旋轉）。

```java
public boolean rotateString(String A, String B) {
    return A.length() == B.length() && (A + A).contains(B);
}
```
**練習題型** :[LeetCode 796. Rotate String](https://leetcode.com/problems/rotate-string/)


