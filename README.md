# Data Structures & Algorithms — Assignment

| Field | Details |
|---|---|
| **Student Name** | Ayesha Javaid|
| **Student ID** | S2025376102 |

---

## Table of Contents

1. [Arrays and Memory Management](#question-1--arrays-and-memory-management)
2. [Sorting Algorithms](#question-2--sorting-algorithms)
3. [Searching Algorithms](#question-3--searching-algorithms)
4. [Algorithm Analysis](#question-4--algorithm-analysis)
5. [Linked Lists](#question-5--linked-lists)
6. [Complete Program](#complete-program)

---

## Question 1 — Arrays and Memory Management

### Q1.A.1 — Contiguous Memory

Contiguous memory means data is stored in one single block. Arrays use it so they can find elements quickly. Then we can access any index instantly.

### Q1.A.2 — Memory Leaks

A memory leak happens when we take memory from the system but don't give it back. Like when we use `new` for a dynamic array and forget to use `delete[]`.

### Q1.A.3 — Static vs. Dynamic Arrays

Static arrays have a fixed size when we write the code. Dynamic arrays can change size while the program is running. Fixed size matters because if we run out of space, we can't add more things.

### Q1.A.4 — O(1) Array Access

Array access is O(1) because the computer knows exactly where each element is. In a Linked List, we have to start from the head and follow pointers one by one.

### Implementation — Linear Search & Max/Min

```cpp
// Linear Search — O(n) time complexity
int linSrch(int arr[], int size, int key) {
    for (int i = 0; i < size; i++) {
        if (arr[i] == key) {
            return i;
        }
    }
    return -1;
}

// Find Max and Min in a single traversal — O(n) time complexity
void findMaxMin(int arr[], int size) {
    int maxVal = arr[0];
    int minVal = arr[0];
    for (int i = 1; i < size; i++) {
        if (arr[i] > maxVal) {
            maxVal = arr[i];
        }
        if (arr[i] < minVal) {
            minVal = arr[i];
        }
    }
    cout << "Maximum: " << maxVal << endl;
    cout << "Minimum: " << minVal << endl;
}
```

---

## Question 2 — Sorting Algorithms

### Q2.A.1 — Bubble Sort Mechanism

Bubble Sort compares two side-by-side numbers and swaps them if needed. In each pass, the largest number "bubbles up" to the end.

### Q2.A.2 — Bubble Sort Complexity

| Case | Time Complexity | Notes |
|---|---|---|
| Best Case | O(n) | Array already sorted; optimization flag stops after one pass |
| Average Case | O(n²) | Random input order |
| Worst Case | O(n²) | Array sorted in reverse order |

If the array is sorted and we use an optimization flag, it stops after one pass.

### Q2.A.3 — Bubble Sort vs. Selection Sort

Selection Sort is usually better because it does fewer swaps. Bubble Sort might be chosen if the array is already mostly sorted.

### Implementation — Optimized Bubble Sort

```cpp
// Bubble Sort with early termination optimization
// Returns the total number of swaps performed
int bubSrt(int arr[], int n) {
    int swaps = 0;
    for (int i = 0; i < n - 1; i++) {
        bool swapped = false;
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                swaps++;
                swapped = true;
            }
        }
        cout << "Pass " << i + 1 << ": ";
        for (int k = 0; k < n; k++) cout << arr[k] << " ";
        cout << endl;
        if (!swapped) break; // Array is sorted — early exit
    }
    return swaps;
}
```

---

## Question 3 — Searching Algorithms

### Q3.A.1 — Binary Search Prerequisite

The array must be sorted first for Binary Search to work.

### Q3.A.2 — Binary Search Walkthrough

**Target:** Key = 23 on array `{2, 5, 8, 12, 16, 23, 38, 45}`

| Step | low | high | mid | arr[mid] | Action |
|---|---|---|---|---|---|
| 1 | 0 | 7 | 3 | 12 | 12 < 23, so low = 4 |
| 2 | 4 | 7 | 5 | 23 | Found at index 5 |

### Q3.A.3 — Binary Search vs. Linear Search

Binary Search is O(log n) and Linear Search is O(n). Binary Search cuts the work in half every time, so it's much faster.

### Implementation — Binary Search with Iteration Tracking

```cpp
// Binary Search — O(log n) time complexity
// Tracks the number of iterations for performance analysis
int binSrch(int arr[], int size, int key, int &iterations) {
    int low = 0;
    int high = size - 1;
    iterations = 0;
    while (low <= high) {
        iterations++;
        int mid = low + (high - low) / 2; // Prevents integer overflow
        if (arr[mid] == key) {
            return mid;
        }
        if (arr[mid] < key) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    return -1; // Key not found
}
```

---

## Question 4 — Algorithm Analysis

### Q4.A.1 — Big O Notation

Big O describes how the time grows as input size (n) gets bigger. We don't use seconds because different computers have different speeds.

### Q4.A.2 — Asymptotic Notations

| Notation | Name | Description |
|---|---|---|
| O(f(n)) | Big O | Worst-case upper bound (longest time) |
| Ω(f(n)) | Big Omega | Best-case lower bound (shortest time) |
| Θ(f(n)) | Big Theta | Tight bound — average case when O and Ω coincide |

### Q4.A.3 — Growth Rate Hierarchy

```
O(1) < O(log n) < O(n) < O(n log n) < O(n²)
```

### Q4.A.4 — Space Complexity

Space complexity is how much extra memory we need. If we make an array of size n, it is O(n).

### Q4.A.5 — Asymptotic Dominance

No, because for very large n, O(n log n) will always be faster than O(n²) no matter how fast the computer is.

### Implementation — Complexity Examples

**O(n²) — Quadratic Time:**

```cpp
// Nested loops produce O(n²) time complexity
void nestedLoop(int n) {
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            // some work
        }
    }
}
```

**O(n) — Linear Time:**

```cpp
// Single loop produces O(n) time complexity
void singleLoop(int n) {
    for (int i = 0; i < n; i++) {
        // some work
    }
}
```

**O(n²) Search with Optimization Strategy:**

```cpp
// Naive O(n²) approach — checking each element of A in B
bool checkElements(int A[], int B[], int n) {
    for (int i = 0; i < n; i++) {
        bool found = false;
        for (int j = 0; j < n; j++) {
            if (A[i] == B[j]) {
                found = true;
                break;
            }
        }
        if (!found) return false;
    }
    return true;
}
```

> **Optimization:** Sort B first (O(n log n)), then use Binary Search for each element of A (O(log n) each). Total: **O(n log n)**.

---

## Question 5 — Linked Lists

### Q5.A.1 — Linked List vs. Array

A Linked List is a chain of nodes where each node points to the next one. Arrays are one big block, but Linked List nodes can be anywhere.

### Q5.A.2 — Linked List Operations

| Operation | Time Complexity | Notes |
|---|---|---|
| Insertion at head | O(1) | Direct pointer manipulation |
| Insertion at tail | O(n) | Must traverse to the end |
| Deletion by value | O(n) | Search required before deletion |

### Q5.A.3 — Memory Management in Linked Lists

If we don't use `delete`, we get a "Memory Leak". To avoid it, always use `delete` when removing a node.

### Implementation — Singly Linked List

```cpp
// Node structure for a singly linked list
struct Node {
    int data;
    Node* next;
};

// Linked List class with core operations
class LinkedList {
public:
    Node* head;

    LinkedList() {
        head = nullptr;
    }

    // Insert at beginning — O(1)
    void insertAtHead(int val) {
        Node* newNode = new Node();
        newNode->data = val;
        newNode->next = head;
        head = newNode;
    }

    // Insert at end — O(n)
    void insertAtTail(int val) {
        Node* newNode = new Node();
        newNode->data = val;
        newNode->next = nullptr;
        if (head == nullptr) {
            head = newNode;
            return;
        }
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }

    // Display the list — O(n)
    void display() {
        Node* temp = head;
        while (temp != nullptr) {
            cout << temp->data << " -> ";
            temp = temp->next;
        }
        cout << "NULL" << endl;
    }

    // Delete first node matching value — O(n)
    void delByVal(int val) {
        if (head == nullptr) return;
        if (head->data == val) {
            Node* temp = head;
            head = head->next;
            delete temp;
            return;
        }
        Node* curr = head;
        Node* prev = nullptr;
        while (curr != nullptr && curr->data != val) {
            prev = curr;
            curr = curr->next;
        }
        if (curr == nullptr) return;
        prev->next = curr->next;
        delete curr;
    }
};
```

---

## Complete Program

```cpp
#include <iostream>
using namespace std;

/*
Q1.A.1: Contiguous memory means data is stored in one single block.
        Arrays use it so they can find elements quickly.
        The advantage is that we can access any index instantly.
Q1.A.2: A memory leak happens when we take memory from the system but don't give it back.
        Like when we use 'new' for a dynamic array and forget to use 'delete[]'.
Q1.A.3: Static arrays have a fixed size when we write the code.
        Dynamic arrays can change size while the program is running.
        Fixed size matters because if we run out of space, we can't add more things.
Q1.A.4: Array access is O(1) because the computer knows exactly where each element is.
        In a Linked List, we have to start from the head and follow pointers one by one.
*/

// Linear Search function
int linSrch(int arr[], int size, int key) {
    for (int i = 0; i < size; i++) {
        if (arr[i] == key) {
            return i;
        }
    }
    return -1;
}

// Find Max and Min in one loop
void findMaxMin(int arr[], int size) {
    int maxVal = arr[0];
    int minVal = arr[0];
    for (int i = 1; i < size; i++) {
        if (arr[i] > maxVal) {
            maxVal = arr[i];
        }
        if (arr[i] < minVal) {
            minVal = arr[i];
        }
    }
    cout << "Maximum: " << maxVal << endl;
    cout << "Minimum: " << minVal << endl;
}

/*
Q2.A.1: Bubble Sort compares two side-by-side numbers and swaps them if needed.
        In each pass, the largest number "bubbles up" to the end.
Q2.A.2:
        Best case: O(n) (if already sorted and we use a flag).
        Average and Worst case: O(n^2).
        If the array is sorted and we use an optimization flag, it stops after one pass.
Q2.A.3: Selection Sort is usually better because it does fewer swaps.
        Bubble Sort might be chosen if the array is already mostly sorted.
*/

// Bubble Sort with optimization
int bubSrt(int arr[], int n) {
    int swaps = 0;
    for (int i = 0; i < n - 1; i++) {
        bool swapped = false;
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                swaps++;
                swapped = true;
            }
        }
        cout << "Pass " << i + 1 << ": ";
        for (int k = 0; k < n; k++) cout << arr[k] << " ";
        cout << endl;
        if (!swapped) break;
    }
    return swaps;
}

/*
Q3.A.1: The array must be sorted first for Binary Search to work.
Q3.A.2: Key = 23 on {2, 5, 8, 12, 16, 23, 38, 45}
        1. low=0, high=7, mid=3. arr[3]=12. 12 < 23, low = 4.
        2. low=4, high=7, mid=5. arr[5]=23. Found at index 5.
Q3.A.3: Binary Search is O(log n) and Linear Search is O(n).
        Binary Search cuts the work in half every time, so it's much faster.
*/

// Binary Search with iteration count
int binSrch(int arr[], int size, int key, int &iterations) {
    int low = 0;
    int high = size - 1;
    iterations = 0;
    while (low <= high) {
        iterations++;
        int mid = low + (high - low) / 2;
        if (arr[mid] == key) {
            return mid;
        }
        if (arr[mid] < key) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    return -1;
}

/*
Q4.A.1: Big O describes how the time grows as input size (n) gets bigger.
        We don't use seconds because different computers have different speeds.
Q4.A.2:
        Big O: Worst case (longest time).
        Big Omega: Best case (shortest time).
        Big Theta: Average case (tight bound).
Q4.A.3: O(1) < O(log n) < O(n) < O(n log n) < O(n^2)
Q4.A.4: Space complexity is how much extra memory we need.
        If we make an array of size n, it is O(n).
Q4.A.5: No, because for very large n, O(n log n) will always be faster than O(n^2)
        no matter how fast the computer is.
*/

// O(n^2) function
void nestedLoop(int n) {
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            // some work
        }
    }
}

// O(n) function
void singleLoop(int n) {
    for (int i = 0; i < n; i++) {
        // some work
    }
}

// O(n^2) search function
bool checkElements(int A[], int B[], int n) {
    for (int i = 0; i < n; i++) {
        bool found = false;
        for (int j = 0; j < n; j++) {
            if (A[i] == B[j]) {
                found = true;
                break;
            }
        }
        if (!found) return false;
    }
    return true;
}

// Better way: Sort B first (O(n log n)), then use Binary Search for each A (O(log n)).

/*
Q5.A.1: A Linked List is a chain of nodes where each node points to the next one.
        Arrays are one big block, but Linked List nodes can be anywhere.
Q5.A.2:
        - Insertion at head: O(1).
        - Insertion at tail: O(n).
        - Deletion by value: O(n).
Q5.A.3: If we don't use delete, we get a "Memory Leak".
        To avoid it, always use delete when removing a node.
*/

struct Node {
    int data;
    Node* next;
};

class LinkedList {
public:
    Node* head;

    LinkedList() {
        head = nullptr;
    }

    void insertAtHead(int val) {
        Node* newNode = new Node();
        newNode->data = val;
        newNode->next = head;
        head = newNode;
    }

    void insertAtTail(int val) {
        Node* newNode = new Node();
        newNode->data = val;
        newNode->next = nullptr;
        if (head == nullptr) {
            head = newNode;
            return;
        }
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }

    void display() {
        Node* temp = head;
        while (temp != nullptr) {
            cout << temp->data << " -> ";
            temp = temp->next;
        }
        cout << "NULL" << endl;
    }

    void delByVal(int val) {
        if (head == nullptr) return;
        if (head->data == val) {
            Node* temp = head;
            head = head->next;
            delete temp;
            return;
        }
        Node* curr = head;
        Node* prev = nullptr;
        while (curr != nullptr && curr->data != val) {
            prev = curr;
            curr = curr->next;
        }
        if (curr == nullptr) return;
        prev->next = curr->next;
        delete curr;
    }
};

int main() {
    // Q1
    int arr1[] = {4, 15, 7, 23, 1, 9, 42, 18, 6, 30};
    int index = linSrch(arr1, 10, 42);
    cout << "42 found at index: " << index << endl;
    findMaxMin(arr1, 10);

    // Q2
    int arr2[] = {64, 34, 25, 12, 22, 11, 90};
    int totalSwaps = bubSrt(arr2, 7);
    cout << "Total swaps: " << totalSwaps << endl;

    // Q3
    int arr3[] = {2, 5, 8, 12, 16, 23, 38, 45, 56, 72};
    int iterCount;
    int bIndex = binSrch(arr3, 10, 56, iterCount);
    cout << "Searching 56: Index " << bIndex << ", Iterations: " << iterCount << endl;
    bIndex = binSrch(arr3, 10, 100, iterCount);
    cout << "Searching 100: Index " << bIndex << ", Iterations: " << iterCount << endl;

    // Q5
    LinkedList list;
    list.insertAtHead(10);
    list.insertAtHead(20);
    list.insertAtTail(30);
    list.insertAtTail(40);
    list.insertAtTail(50);
    list.display();
    list.delByVal(30);
    list.delByVal(100);
    list.display();

    return 0;
}
```
