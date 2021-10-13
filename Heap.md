# Heap

In computer science, a heap is a specialized tree-based data structure which is essentially an almost complete tree that satisfies the heap property: in a *max heap*, for any given node C, if P is a parent node of C, then the *key* (the *value*) of P is greater than or equal to the key of C. In a *min heap*, the key of P is less than or equal to the key of C. The node at the "top" of the heap (with no parents) is called the *root* node.

The heap is one maximally efficient implementation of an abstract data type called a priority queue, and in fact, priority queues are often referred to as "heaps", regardless of how they may be implemented. In a heap, the highest (or lowest) priority element is always stored at the root. However, a heap is not a sorted structure; it can be regarded as being partially ordered. A heap is a useful data structure when it is necessary to repeatedly remove the object with the highest (or lowest) priority.



The set of operations can be:

+ MaxHeap create(int maxSize);
+ boolean isFull(MaxHeap H);
+ void insert(MaxHeap H, int item);
+ boolean isEmpty(MaxHeap H);
+ int deleteMax(MaxHeap H); 



```c++
#include <iostream>
using namespace std;
#define MaxData 1000

typedef int ElementType;
typedef struct HeapStruct *MaxHeap;
struct HeapStruct {
    ElementType* data;     // 存储堆元素的数组
    int size;              // 堆的当前元素个数
    int capacity;          // 堆的最大容量
};

MaxHeap create(int maxSize);
bool isEmpty(MaxHeap H);
bool isFull(MaxHeap H);
void insert(MaxHeap H, ElementType item);
ElementType deleteMax(MaxHeap H);

int main() {

    return 0;
}

MaxHeap create(int maxSize) {
    MaxHeap H = (MaxHeap)malloc(sizeof(struct HeapStruct));
    H->data = (ElementType*)malloc((maxSize+1) * sizeof(ElementType));
    H->size = 0;
    H->capacity = maxSize;
    H->data[0] = MaxData;
    return H;
}

bool isFull(MaxHeap H) {
    return H->size == H->capacity;
}

bool isEmpty(MaxHeap H) {
    return H->size == 0;
}

void insert(MaxHeap H, ElementType item) {
    int i;
    if (isFull(H)) {
        cout << "最大堆已满." << endl;
        return;
    }
    i = ++H->size;
    for ( ; H->data[i / 2] < item; i /= 2) {
        H->data[i] = H->data[i / 2];
    }
    H->data[i] = item;
}

ElementType deleteMax(MaxHeap H) {
    int parent, child;
    ElementType maxItem, temp;
    if (isEmpty(H)) {
        cout << "最大堆已为空" << endl;
        return;
    }
    maxItem = H->data[1];   // 取出根结点
    temp = H->data[H->size--];
    for (parent = 1; parent*2 <= H->size; parent=child) {
        child = parent * 2;
        if ((child != H->size) && H->data[child] < H->data[child+1]) {
            child++;
        }
        if (temp >= H->data[child]) {
            break;
        } else {
            H->data[parent] = H->data[child];
        }
    }
    H->data[parent] = temp;
    return maxItem;
}



```

