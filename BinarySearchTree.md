# Binary Search Tree

Binary Search Tree (BST) is also called **sorted binary tree**. It is a rooted binary tree data structure whose internal nodes each store a key greater than all the keys in the node’s left subtree and less than those in its right subtree.  A binary tree is a type of data structure for storing data such as numbers in an organized way. Binary search trees allow binary search for fast lookup, addition and removal of data items, and can be used to implement dynamic sets and lookup tables. The order of nodes in a BST means that each comparison skips about half of the remaining tree, so the whole lookup takes time proportional to the binary logarithm of the number of items stored in the tree. 

<img src="/Users/co2maker/Desktop/note-4-data-structure/figure/BST.png" style="zoom:50%" />

In the above diagram, (a) shows a binary tree and (b) shows a binary search tree. In general, for BST, time complexity are:

| Operation |  Average  | Worst  |
| :-------: | :-------: | :----: |
|   Space   |  $O(n)$   | $O(n)$ |
|  Search   | $O(logn)$ | $O(n)$ |
|  Insert   | $O(logn)$ | $O(n)$ |
|  Delete   | $O(logn)$ | $O(n)$ |

For BST, the general operations set can be:

+ Find

+ Find Minimum

+ Find Maximum

+ Insert Node

+ Delete Node

  

Thus, a C++ implementation can be:

```c++
#include <iostream>
using namespace std;

typedef struct TreeNode *BinTree;
typedef BinTree Position;
struct TreeNode {
    int Data;
    BinTree Left;
    BinTree Right;
};

Position find(int x, BinTree BST);
Position findMin(BinTree BST);
Position findMax(BinTree BST);
BinTree insertNode(int x, BinTree BST);
BinTree deleteNode(int x, BinTree BST);

Position find(int x, BinTree BST) {
    if (!BST) return NULL;
    if (BST->Data > x) {
        return find(x, BST->Left);
    } else if (BST->Data < x) {
        return find(x, BST->Right);
    } else {
        return BST;
    }
}

Position findMin(BinTree BST) {
    if (!BST) {
        return NULL;
    } else if (!BST->Left) {
        return BST;
    } else {
        return findMin(BST->Left);
    }
}

Position findMax(BinTree BST) {
    if (BST) {
        while(BST->Right) BST = BST->Right;
    }
    return BST;
}

BinTree insertNode(int x, BinTree BST) {
    if (!BST) {
        BST = (BinTree)malloc(sizeof(TreeNode));
        BST->Data = x;
        BST->Left = NULL;
        BST->Right = NULL;
    } else {
        if (BST->Data < x) {
            insertNode(x, BST->Right);
        } else {
            insertNode(x, BST->Left);
        }
    }
    return BST;
}

BinTree deleteNode(int x, BinTree BST) {
    Position tmp;
    if (!BST) cout << "The node doesn't exists." << endl;
    else if (BST->Data < x) {
        BST->Right = deleteNode(x, BST->Right);
    } else if (BST->Data > x) {
        BST->Left = deleteNode(x, BST->Left);
    } else {
        if (BST->Left && BST->Right) {
            tmp = findMin(BST->Right);
            BST->Data = tmp->Data;
            BST->Right = deleteNode(BST->Data, BST->Right);
        } else {
            tmp = BST;
            if (!BST->Left) {
                BST = BST->Right;
            } else if (!BST->Right) {
                BST = BST->Left;
            }
            free(tmp);
        }
    }
}
```

