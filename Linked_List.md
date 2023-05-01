# Linked_Lists
- 各節點的資料型態不必一定相同
- 每個點放在不同記憶體位置，不會按線性的順序儲存資料
- 記憶體非連續，不需事先知道整體資料大小
- 每一個節點裡存有到下一個節點記憶體位置的 pointer
- 可以有單向或是雙向的 linked list
- 能夠被直接存取的節點只有最前面的第一個節點

### LinkedList 的種類
- 單向鏈結串列 (Single Link List)
![](https://i.imgur.com/pZETH13.png)


單向鏈結串列是鏈結串列家族中最簡單的版本，特色是每兩個節點間只有一個單向的鏈結。

###### 簡單的單向鏈表
```java
1 	class Node {
2 		Node next= null;
3 		int data; 
4
5 		public Node(int d) {
6 			data= d;
7 		}
8
9 		void appendToTail(int d) {
10 			Node end= new Node(d);
11 			Node n = this;
12 			while (n.next != null) {
13 				n = n.next;
14 			}
15 			n.next = end;
16 		}
17 	}
```
###### 從單鏈表中刪除節點
給定一個節點 n，我們找到其前一節點 `prev` 並令 `prev.next = n.next`
如果是雙向鏈表，我們還必須更新 `n.next`，令 `n.next.prev = n.prev`。
要記住的重要事項是
（1）檢查空指針
（2）根據需要更新頭或尾指針。
![](https://i.imgur.com/AXrD4OT.png)

```java
1 	Node deleteNode(Node head, int d) {
2 		Node n = head;
3
4 		if (n.data == d) {
5 			return head.next; /* moved head */
6 		}
7
8 		while (n.next != null) {
9 			if (n.next.data == d) {
10 				n.next = n.next.next;
11 				return head; /* head didn't change */
12 			}
13 			n = n.next;
14 		}
15 		return head;
16 	}
```
	


-----
- 雙向鏈結串列 (Double Link List)
![](https://i.imgur.com/7VGmcoJ.png)
和單向操作類似，差別在於每個節點都有紀錄前、後位置的`pointer`
而第一個節點的`prev`和最後一個節點`next`,皆指向為`null`


------
- 環狀鏈結串列 (Circular Link List)
![](https://i.imgur.com/7Wp5XmS.jpg)


### Linked List效能

|Operation|Complexity|
|  ----  | ----  |
|get|O(n)|
|insert|節點已知：O(1) ；節點未知：O(n−i)|
|remove|節點已知：O(1) ；節點未知：O(n−i)|
|append|O(n)|
|insert/remove first|O(1)|
|insert/remove last |O(n)|
|space|	O(n) + 各節點額外一個指標 n 個

`n：資料筆數。
i：相對於整個容器的索引位置。`

----
## ArrayList 與 Linked List比較
//TODO



-----------
## Runner技術

例如，假設你有一個鏈表
a1 -> a2 -> ... -> an -> b1 -> b2 -> ... -> bn，並且你想把它重新排列成
a1 -> b1 -> a2 -> b2 -> ... -> an -> bn。
你不知道鏈表的長度（但是你知道長度是偶數）。你可以使用一個指針 p1​（快指針），在 ​p2​ 每移動一個元素時 ​p1​ 移動兩個元素。當 ​p1 到達鏈表的末尾時，p2 將位於中點。然後，將 p1 移回到鏈表頭並開始“織入（weaving）”元素(?)。在每次迭代中，p2 選擇一個元素並將其插入 p1​ 之後。

```java
public static void findMidElOfLinkedList(FindMidElementOfLinkedList findMidElementOfLinkedList) {
    Node node = findMidElementOfLinkedList.head;
    Node slow = node;
    Node fast = node;

    while (fast != null && fast.next != null) {
        fast = fast.next.next; // increase 2
        slow = slow.next; // increate 1
    }
    System.out.println(slow.data);
    /*
    * Slow runner goes at a pace of 1 element per move, fast runner goes 2 elements per move.
    When the fast runner reaches the end of the linked list, then slow runner is sitting at the middle. Testing this out for one/two middle cases work.
    Time O(N), faster than the previous brute force method, Space: O(1).
    * */
}
```

-------------
## Interview Questions

2.1 刪除重複項（Remove Dups）：編寫代碼從未排序的鏈錶中刪除重複項。

FOLLOW UP

如果不允許使用臨時緩衝區，如何解決這個問題?

**題目練習** : [02.01. 移除重複節點](https://leetcode.cn/problems/remove-duplicate-node-lcci/)

2.2 返回第 K 到最後（Return Kth to Last）：實現一個算法，以找到單鏈表的第 K 個到最後一個元素。

**題目練習** : [02.02 返回倒數第 k 個節點](https://leetcode.cn/problems/kth-node-from-end-of-list-lcci/)

2.3 刪除中間節點（Delete Middle Node）：實現一個算法，以刪除單鏈表的中間節點（即，除了第一個和最後一個節點以外的任何節點，不一定是確切的中間節點），要求僅允許訪問該節點。

EXAMPLE

Input: the node c from the linked list a->b->c->d->e->f
Result: nothing is returned, but the new linked list looks like a->b->d->e->f

**題目練習** : [02.03. 刪除中間節點](https://leetcode.cn/problems/delete-middle-node-lcci/)

2.4 分區（Partition）：編寫代碼以圍繞值 x 對鏈表進行分區，使所有小於 x 的節點排在所有大於或等於 x 的節點之前。如果 x 包含在列表中，則 x 的值僅需在小於 x 的元素之後（請參見下文）。分區元素 x 可以出現在“右分區”中的任何位置； 不需要將它放在左右分區之間。

EXAMPLE

Input: 3 -> 5 -> 8 -> 5 -> 10 -> 2 -> 1 [partition= 5]
Output: 3 -> 1 -> 2 -> 10 -> 5 -> 5 -> 8
**題目練習** : [02.04 分割鏈表](https://leetcode.cn/problems/partition-list-lcci/)

2.5 總和列表（Sum Lists）：你有兩個由鏈表表示的數字，其中每個節點都包含一個數字。這些數字以相反的順序存儲，即第一位的數字就位於列表的開頭。編寫一個函數，將兩個數字相加，然後將和以鏈表的形式返回。

EXAMPLE

Input: (7-> 1 -> 6) + (5 -> 9 -> 2). That is, 617 + 295.
Output: 2 -> 1 -> 9. That is, 912.
FOLLOW UP

假設數字以正序存儲。重複上述問題。

EXAMPLE

Input: (6 -> 1 -> 7) + (2 -> 9 -> 5). That is, 617 + 295.
Output: 9 -> 1 -> 2. That is, 912.
**題目練習** : [02.05 鏈表求和](https://leetcode.cn/problems/sum-lists-lcci/)

2.6 回文（Palindrome）：實現一個函數來檢查一個鏈表是否是一個回文。
**題目練習** : [02.06 回文鏈表](https://leetcode.cn/problems/palindrome-linked-list-lcci/)

2.7 相交（Intersection）：給定兩個（單）鏈表，判斷兩個鏈表是否相交。是的話返回相交節點。請注意，相交是基於引用而不是基於值定義的。也就是說，如果第一個鏈表的第 k 個節點與第二個鏈表的第 j 個節點完全相同（引用層面上），那麼它們相交。

**題目練習** : [02.07 鏈表相交](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/)

2.8 循環檢測（Loop Detection）：給定一個循環鏈表，實現一個算法，返回循環開始處的節點。

DEFINITION

循環鏈表：一種（不純的）鏈表，其中一個節點的下一個指針指向較早的節點，從而在鏈表中形成一個循環。

EXAMPLE

Input: A -> B -> C -> D -> E -> C [the same C as earlier]
Output: C
**題目練習** : [LeetCode 141](https://leetcode.com/problems/linked-list-cycle/)
