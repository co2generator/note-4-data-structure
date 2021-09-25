# List

The common operations of List can be

+ initialize
+ getLength
+ find
+ insert
+ delete

The following shows two implementations.

### Implement via array

```c++
#include <iostream>
using namespace std;
#define MAXSIZE 1000

// definition
typedef struct LNode *List;
struct LNode {
    int Data[MAXSIZE];
    int Last;
};

// initilize
List makeEmpty() {
    List PtrL;
    PtrL = (List)malloc(sizeof(struct LNode));
    PtrL->Last = -1;
    return PtrL;
}

// find
int find(int X, List PtrL) {
    int i = 0;
    while (i <= PtrL->Last && PtrL->Data[i] != X) {
        ++i;
    }
    if (i > PtrL->Last) return -1;
    else return i;
}

// insertion
void insert(int X, int i, List PtrL) {
    if (PtrL->Last == MAXSIZE-1) {
        cout << "List is full, insertion failed.";
        return;
    }
    if (i < 1 || i > PtrL->Last+2) {
        cout << "Position is invalid.";
        return;
    }
    for (int j = PtrL->Last; j >= i-1; j--) {
        PtrL->Data[j+1] = PtrL->Data[j];
    }
    PtrL->Data[i-1] = X;
    PtrL->Last++;
    return;
}

// deletion
void deleteItem(int i, List PtrL) {
    if (i < 1 || i > PtrL->Last+1) {
        cout << "The" << i << "th element not exists.";
        return;
    }
    for (int j = i; j <= PtrL->Last; j++) {
        PtrL->Data[j-1] = PtrL->Data[j];
    }
    PtrL->Last--;
    return;
}
```



### Implement via linked list

```c++
#include<iostream>
using namespace std;

typedef struct LNode *List;
struct LNode {
    int Data;
    List Next;
};

// length
int getLength(List PtrL) {
    List p = PtrL;
    int len = 0;
    while (p != NULL) {
        p = p->Next;
        len++;
    }
    return len;
}

// find kth
List findKth(int K, List PtrL) {
    List p = PtrL;
    int i = 1;
    while (p != NULL && i < K) {
        p = p->Next;
        i++;
    }
    if (i == K) return p;
    else return NULL;
}

// insertion
List insert(int X, int i, List PtrL) {
    List p, s;
    if (i == 1) {
        s = (List)malloc(sizeof(struct LNode));
        s->Data = X;
        s->Next = PtrL;
        return s;
    }
    p = findKth(i - 1, PtrL);
    if (p == NULL) {
        cout << "i is wrong.";
        return PtrL;
    } else {
        s = (List)malloc(sizeof(struct LNode));
        s->Data = X;
        s->Next = p->Next;
        p->Next = s;
        return PtrL;
    }
}

// deletion, delete the ith item
List deleteItem(int i, List PtrL) {
    List p, s;
    if (i == 1) {
        s = PtrL;
        if (PtrL != NULL) PtrL = PtrL->Next;
        else return NULL;
        free(s);
        return PtrL;
    }
    p = findKth(i - 1, PtrL);
    if (p == NULL) {
        cout << i-1 << "th element is not exists.";
        return NULL;
    } else if (p->Next == NULL) {
        cout << i << "th element is not exists.";
        return NULL;
    } else {
        s = p->Next;
        p->Next = s->Next;
        free(s);
        return PtrL;
    }
}
```

