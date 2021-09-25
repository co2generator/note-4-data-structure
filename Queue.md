# Queue

The common operations of Stack can be:

+ addQueue
+ deleteQueue

The following shows two implementations:

### Implement via Array

```c++
#include <iostream>
using namespace std;
#define MAXSIZE 1000

// definition
struct QNode {
    int Data[MAXSIZE];
    int rear;
    int front;
};
typedef struct QNode *Queue;

// add queue
void addQueue(Queue ptrQ, int item) {
    if ((ptrQ->rear+1)%MAXSIZE == ptrQ->front) {
        cout << "The queue is full." << endl;
        return;
    }
    ptrQ->rear = (ptrQ->rear+1)%MAXSIZE;
    ptrQ->Data[ptrQ->rear] = item;
}

// delete queue
int deleteQueue(Queue ptrQ) {
    if (ptrQ->front == ptrQ->rear) {
        cout << "The queue is null. Delete failed." << endl;
        return NULL;
    } else {
        ptrQ->front = (ptrQ->front+1)%MAXSIZE;
        return ptrQ->Data[ptrQ->front];
    }
}
```

### Implement via LinkedList

```c++
#include <iostream>
using namespace std;

// definition
struct Node {
    int Data;
    struct Node *Next;
};
struct QNode {
    struct Node *front;
    struct Node *rear;
};
typedef struct QNode *Queue;

// add queue
void addQueue(Queue ptrQ, int item) {
    Node *tmp = (Node*)malloc(sizeof(struct Node));
    tmp->Data = item;
    ptrQ->rear->Next = tmp;
    ptrQ->rear = ptrQ->rear->Next;
}


// delete queue
int deleteQueue(Queue ptrQ) {
    if (ptrQ->front == NULL) {
        cout << "The queue is null." << endl;
        return NULL; 
    }
    struct Node *frontItem = ptrQ->front;
    if (ptrQ->front == ptrQ->rear) {
        ptrQ->front = ptrQ->rear = NULL;
    } else {
        ptrQ->front = ptrQ->front->Next;
    }
    int frontValue = frontItem->Data;
    free(frontItem);
    return frontValue;
}
```

