# Leetcode_Day100
# 622. Design Circular Queue

**Difficulty:** Medium  
**Topic:** Queue, Array, Design

## Problem Statement
Design a circular queue that follows the FIFO (First In, First Out) principle. The last position connects back to the first position, allowing us to reuse empty spaces.

Implement the following operations:
- `MyCircularQueue(k)` – Initialize a queue of size `k`.
- `Front()` – Return the front element, or `-1` if empty.
- `Rear()` – Return the last element, or `-1` if empty.
- `enQueue(value)` – Insert an element if the queue is not full.
- `deQueue()` – Remove the front element if the queue is not empty.
- `isEmpty()` – Check whether the queue is empty.
- `isFull()` – Check whether the queue is full.

## Approach: Array + Circular Indexing

1. Create an array of size `k` to store queue elements.
2. Maintain three variables:
   - `front` – Index of the front element.
   - `rear` – Index of the rear element.
   - `count` – Number of elements currently present.
3. Initially, set `front = 0`, `rear = -1`, and `count = 0`.
4. For insertion, update the rear using `(rear + 1) % capacity`.
5. For deletion, update the front using `(front + 1) % capacity`.
6. Use `count` to check whether the queue is empty or full.

## Java Solution

```java
class MyCircularQueue {

    int[] queue;
    int front;
    int rear;
    int count;
    int capacity;

    public MyCircularQueue(int k) {
        queue = new int[k];
        capacity = k;
        front = 0;
        rear = -1;
        count = 0;
    }

    public boolean enQueue(int value) {
        if (isFull()) {
            return false;
        }

        rear = (rear + 1) % capacity;
        queue[rear] = value;
        count++;

        return true;
    }

    public boolean deQueue() {
        if (isEmpty()) {
            return false;
        }

        front = (front + 1) % capacity;
        count--;

        return true;
    }

    public int Front() {
        if (isEmpty()) {
            return -1;
        }

        return queue[front];
    }

    public int Rear() {
        if (isEmpty()) {
            return -1;
        }

        return queue[rear];
    }

    public boolean isEmpty() {
        return count == 0;
    }

    public boolean isFull() {
        return count == capacity;
    }
}
```

## Complexity Analysis

| Operation | Time Complexity |
|---|---|
| Constructor | O(k) |
| enQueue() | O(1) |
| deQueue() | O(1) |
| Front() | O(1) |
| Rear() | O(1) |
| isEmpty() | O(1) |
| isFull() | O(1) |

**Space Complexity:** O(k), for the array of size `k`.

## What I Learned

- How circular queues work using arrays.
- How the modulo (`%`) operator helps wrap indices around.
- How to manage front and rear pointers efficiently.
- How to reuse empty spaces without shifting elements.

## Key Takeaway

A circular queue makes memory usage more efficient by reusing previously occupied positions. Using modulo arithmetic allows insertion and deletion in O(1) time without using a built-in queue.
