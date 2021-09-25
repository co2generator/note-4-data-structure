#  Stack

The common operations of Stack can be:

+ createStack
+ push
+ pop

The following shows two implementations:

### Implement via Array

```c++
#include <iostream>
using namespace std;
#define MAXSIZE 1000

// definition
typedef struct SNode *Stack;
struct SNode {
    int Data[MAXSIZE];
    int Top;
};

// push
void push(Stack PtrS, int item) {
    if (PtrS->Top == MAXSIZE-1) {
        cout << "The stack is full." << endl;
    } else {
        PtrS->Data[++(PtrS->Top)] = item;
        return;
    }
}

// pop
int pop(Stack PtrS) {
    if (PtrS->Top == -1) {
        cout << "The stack is null." << endl;
    } else {
        return (PtrS->Data[(PtrS->Top)--]);
    }
}
```



### Implement via LinkedList

```c++
#include <iostream>
using namespace std;

typedef struct SNode *Stack;
struct SNode {
    int Data;
    struct SNode *Next;
};

// initialize 
Stack createStack() {
    Stack S = (Stack)malloc(sizeof(struct SNode));
    S->Next = NULL;
    return S;
}

// is empty stack
int isEmpty(Stack S) {
    return S->Next == NULL;
} 

// push
void push(int item, Stack S) {
    struct SNode *tmp;
    tmp = (struct SNode *)malloc(sizeof(struct SNode));
    tmp->Data = item;
    tmp->Next = S->Next;
    S->Next = tmp;
}

// pop
int pop(Stack S) {
    if (isEmpty(S)) {
        cout << "The stack is null." << endl;
    } else {
        struct SNode *firstItem;
        firstItem = S->Next;
        S->Next = firstItem->Next;
        int topData = firstItem->Data;
        free(firstItem);
        return topData;
    }
}
```

