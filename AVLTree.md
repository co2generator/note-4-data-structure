### AVL Tree

An **AVL tree** (named after inventors **A**delson-**V**elsky and **L**andis) is a self-balancing binary search tree. It was the first such data structure to be invented. In an AVL tree, the heights of the two child subtrees of any node differ by at most one; if at any time they differ by more than one, rebalancing is done to restore this property. Lookup, insertion, and deletion all take $O(logn)$ time in both the average and worst cases, where $n$ is the number of nodes in the tree prior to the operation. Insertions and deletions may require the tree to be rebalanced by one or more tree rotations.

<img src="/Users/co2maker/Desktop/note-4-data-structure/figure/AVL.png" style="zoom:50%" />

In this above diagram, (a) is a binary search tree, (b) is an AVL tree, (c) shows the worst case. In general, the set of operations is similar to binary search tree. The following shows a simple C++ implementation of building AVL Tree.

```c++
#include <iostream>
using namespace std;

typedef struct AVLNode *Position;
typedef Position AVLTree;
struct AVLNode {
    int Data;
    AVLTree Left;
    AVLTree Right;
    int Height;
};

int getHeight(AVLTree root);
AVLTree insert(AVLTree root, int data);
AVLTree rightRightRotation(AVLTree root);
AVLTree leftLeftRotation(AVLTree root);
AVLTree rightLeftRotation(AVLTree root);
AVLTree leftRightRotation(AVLTree root);

int getHeight(AVLTree root) {
    if (!root) return -1;
    return root->Height;
}

AVLTree insert(AVLTree root, int data) {
    if (!root) {
        root = new AVLNode();
        root->Data = data;
        root->Left = NULL;
        root->Right = NULL;
        root->Height = 0;
    } else if (root->Data > data) {
        root->Left = insert(root->Left, data);
        if (getHeight(root->Left) - getHeight(root->Right) == 2) {
            if (data < root->Left->Data) root = leftLeftRotation(root);
            else root = leftRightRotation(root);
        }
    } else if (root->Data < data) {
        root->Right = insert(root->Right, data);
        if (getHeight(root->Left) - getHeight(root->Right) == -2) {
            if (data < root->Right->Data) root = rightRightRotation(root);
            else root = rightLeftRotation(root);
        }
    }
    root->Height = max(getHeight(root->Left), getHeight(root->Right)) + 1;
    return root;
}

AVLTree rightRightRotation(AVLTree root) {
    AVLTree tmp = root->Right;
    root->Right = tmp->Left;
    tmp->Left = root;
    root->Height = max(getHeight(root->Left), getHeight(root->Right)) + 1;
    tmp->Height = max(getHeight(tmp->Left), getHeight(tmp->Right)) + 1;
    return tmp;
}

AVLTree leftLeftRotation(AVLTree root) {
    AVLTree tmp = root->Left;
    root->Left = tmp->Right;
    tmp->Right = root;
    root->Height = max(getHeight(root->Left), getHeight(root->Right)) + 1;
    tmp->Height = max(getHeight(tmp->Left), getHeight(tmp->Right)) + 1;
    return tmp;
}

AVLTree rightLeftRotation(AVLTree root) {
    AVLTree tmp = root->Right;
    root->Right = rightRightRotation(tmp);
    return leftLeftRotation(root);
}

AVLTree leftRightRotation(AVLTree root) {
    AVLTree tmp = root->Left;
    root->Left = leftLeftRotation(tmp);
    return rightRightRotation(root);
}
```

