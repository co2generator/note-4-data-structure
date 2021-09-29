# Tree



For binary tree, we can use a linked list to store. 

```c++
typedef struct TreeNode *BinTree;
typedef BinTree Position;
struct TreeNode {
    int Data;
    BinTree Left;
    BinTree Right;
};
```



### Recursive Traversal

+ Pre Order Traversal

```c++
void preOrderTraversal(BinTree BT) {
    if (BT) {
        cout << BT->Data << endl;
        preOrderTraversal(BT->Left);
        preOrderTraversal(BT->Right);
    } else {
        cout << "Tree is null." << endl;
    }
}
```



+ In Order Traversal

```c++
void inOrderTraversal(BinTree BT) {
    if (BT) {
        inOrderTraversal(BT->Left);
        cout << BT->Data << endl;
        inOrderTraversal(BT->Right);
    } else {
        cout << "Tree is null." << endl;
    }
}
```



+ Post Order Traversal

```c++
void postOrderTraversal(BinTree BT) {
    if (BT) {
        postOrderTraversal(BT->Left);
        postOrderTraversal(BT->Right);
        cout << BT->Data << endl;
    } else {
        cout << "Tree is null." << endl;
    }
}
```



### Non-recursive Traversal

+ Pre Order Traversal

```c++
void preOrderTraversal(BinTree BT) {
    BinTree T = BT;
    stack<BinTree> s;
    while (T || !s.empty()) {
        while (T) {
            cout << T->Data << endl;
            s.push(T);
            T = T->Left;
        }
        if (!s.empty()) {
            T = s.top();
            s.pop();
            T = T->Right;
        }
    }
}
```



+ In Order Traversal

```c++
void inOrderTraversal(BinTree BT) {
    BinTree T = BT;
    stack<BinTree> s;
    while (T || !s.empty()) {
        while (T) {
            s.push(T);
            T = T->Left;
        }
        if (!s.empty()) {
            T = s.top();
            s.pop();
            cout << T->Data << endl;
            T = T->Right;
        }
    }
}
```



+ Post Order Traversal

 ```c++
 void preOrderTraversal(BinTree BT) {
     BinTree T = BT;
     stack<BinTree> s;
     stack<BinTree> s2;
     while (T || !s.empty()) {
         while (T) {
             s2.push(T);
             s.push(T);
             T = T->Right;
         }
         if (!s.empty()) {
             T = s.top();
             s.pop();
             T = T->Left;
         }
     }
     while (!s2.empty()) {
         T = s2.top();
         cout << T->Data << endl;
         s2.pop();
     }
 }
 ```



### Level Order Traversal

```c++
void levelOrderTraversal(BinTree BT) {
    queue<BinTree> q;
    BinTree T;
    if (!BT) return;
    q.push(BT);
    while (!q.empty()) {
        T = q.front();
        q.pop();
        cout << T->Data << endl;
        if (T->Left) q.push(T->Left);
        if (T->Right) q.push(T->Right);
    } 
}
```

