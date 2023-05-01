樹與圖
==========
搜尋一個樹比一個線性組織的數據結構(如陣列、集合)中搜索要複雜得多，時間複雜度可能會有很大的差異。

多數人較熟悉樹，也比圖簡單，而實際樹也是一種圖

## 樹的類型
理解樹的方法試用遞迴來解釋，樹是由節點(Node)組成數據結構。
* 每棵樹都有一個根節點(非必要，但程式上使用通常是這樣)
* 根結點具有多個子節點
* 每個子節點都有0個或多個子節點

## 樹 vs 二叉樹
二叉樹(binary tree) 是指每個節點最多有兩個子節點的樹

![binarytree](https://user-images.githubusercontent.com/89962742/235472327-133f6389-6b4e-407b-9427-29cbf22f26e1.jpg)

## 二叉樹 vs 二叉搜尋樹
二叉搜尋樹（binary search tree）是一種二叉樹，每個節點須符合特性:`所有左子節點<=n<所有右子節點`

![OIP](https://user-images.githubusercontent.com/89962742/235472522-9588372e-7445-4765-9972-77c44311efe6.gif)


## 平衡 vs 不平衡
平衡是指"不是非常不平衡"。其程度足以確保inser及find的時間複雜度為O(log n)

常見的平衡樹為紅黑樹、和AVL樹

## 完全二叉樹
完全二叉樹（complete binary tree）除了最後一層外，每一層都被完全填充。最後一層滿足從左到右填充

![1867105-20201222230710401-1727662184](https://user-images.githubusercontent.com/89962742/235473283-372a3eb8-2758-44ce-939a-dee7261de50b.png)

## 滿二叉樹
滿二叉樹（full binary tree）是一種二叉樹，其中每個節點都有0個或2個子節點。也就是說，不存在某個節點只有一個子節點

![full](https://user-images.githubusercontent.com/89962742/235473747-cccfa487-1ea2-4df6-9900-460a6afed204.png)

## 完美二叉樹
完美二叉樹（perfect binary tree）滿足完全二叉樹又滿足滿二叉樹特徵

![perfect](https://user-images.githubusercontent.com/89962742/235474082-ea53f939-0f30-43a7-9b1d-a0555c1ae42b.png)

完美二叉樹面試跟實際都很少見，不要假設二叉樹是完美的。

## 二叉樹遍歷
面試前應能輕鬆實現中序遍歷、前序遍歷及後續遍歷。其中最常見的是中序遍歷。

### 中序遍歷
``` java
1	void inOrderTraversal(TreeNode node) {
2		if (node != null) {
3			inOrderTraversal(node.left);
4 			visit(node);
5 			inOrderTraversal(node.right);
6		}
7 	}
```

### 前序遍歷
``` java
1	void preOrderTraversal(TreeNode node) {
2 		if (node != null) {
3 			visit(node);
4 			preOrderTraversal(node.left);
5 			preOrderTraversal(node.right);
6 		}
7	}
```


### 後序遍歷
``` java
1	void postOrderTraversal(TreeNode node) {
2 		if (node != null) {
3 			postOrderTraversal(node.left);
4 			postOrderTraversal(node.right);
5 			visit(node);
6		}
7 	}
```
# 遍歷有2種
## DFS left 左深度優先

遍歷 Traversal
### pre-order
遇到一個節點 馬上印出來



### in-order
左邊回來後印



### post-order
右邊回來後印



## DFS right 右深度優先

遍歷 Traversal
### pre-order
遇到一個節點 馬上印出來



### in-order
`右`邊回來後印



### post-order
`左`邊回來後印



## Binary Tree Traversal
BST 用DFS left or DFS right?
依照需求，一般習慣用left

### BST定義
左邊的節點數字小，右邊大


### 實作遍歷

1. 建立class


2. buildtree()


3. 測試方法


4. DFS left

* pre-order


* in-order


* post-order


* 執行結果


5. DFS right
left跟right對換即可

## 陣列實作二元數


## leetcode 0100
https://leetcode.com/problems/same-tree/

解法
```java
public class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) return true;
        if (p != null && q == null) return false;
        if (p == null && q != null) return false;

        boolean result = true;

        if (p.val != q.val) {
            result = false;
        }else {
            boolean result_left = isSameTree(p.left, q.left);
            if (result_left == false) result = false;
            boolean result_right = isSameTree(p.right, q.right);
            if (result_right == false) result = false;
        }


        return result;
    }
}

```

預設兩者節點相同 result=true
當下比較節點值不同result = false，如果相同繼續往下走，更新結果=>回傳
