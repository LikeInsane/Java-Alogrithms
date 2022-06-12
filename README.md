# 数组，链表，栈，队列
## 第一题：加一 https://leetcode.cn/problems/plus-one/
```java
class Solution {
    public int[] plusOne(int[] digits) {
        int n = digits.length;
        /**
        1.当最高位!=9的时候
        2.逆序遍历找到!=9的第一个数字加1
        3.将其后续全置为0
         */
        for (int i = n - 1; i >= 0; --i) {
            if (digits[i] != 9) {
                ++digits[i];
                for (int j = i + 1; j < n; ++j) {
                    digits[j] = 0;
                }
                return digits;
            }
        }

        /**
        1.当digits 中所有的元素均为9时
        2.创建新数组，长度为digits+1
        3.直接最高为置1
         */
        int[] ans = new int[n + 1];
        ans[0] = 1;
        return ans;
    }
}
```

## 第二题：合并两个有序链表 https://leetcode.cn/problems/merge-two-sorted-lists/
```java
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        /**
        1.当l1或l2为空，直接返回
        2.否则，比较l1和l2值，小的指向大的
        3.当一方遍历为空后，递归结束
         */
         if(list1 == null){
             return list2;
         }else if(list2 == null){
             return list1;
         }else if(list1.val <= list2.val){
             list1.next = mergeTwoLists(list1.next, list2);
             return list1;
         }else{
             list2.next = mergeTwoLists(list1, list2.next);
             return list2;
         }

    }
}
```

## 第三题：设计循环队列 https://leetcode.cn/problems/design-circular-queue/
```java
class MyCircularQueue {
    private int[] deque;
    private int front;
    private int rear;
    private int capacity;

    public MyCircularQueue(int k) {
        capacity = k + 1;
        deque = new int[capacity];
        front = 0;
        rear = 0;

    }
    
    public boolean enQueue(int value) {
        if (isFull()) {
            return false;
        }
        deque[rear] = value;
        rear = (rear + 1) % capacity;
        return true;
    }
    
    public boolean deQueue() {
        if (isEmpty()) {
            return false;
        }
        front = (front + 1) % capacity;
        return true;
    }
    
    public int Front() {
        if (isEmpty()) {
            return -1;
        }

        return deque[front];
    }
    
    public int Rear() {
        if (isEmpty()) {
            return -1;
        }

        return deque[(rear - 1 + capacity) % capacity];
    }
    
    public boolean isEmpty() {
        return front == rear;
    }
    
    public boolean isFull() {
        return (rear + 1) % capacity == front;
    }
}

/**
 * Your MyCircularQueue object will be instantiated and called as such:
 * MyCircularQueue obj = new MyCircularQueue(k);
 * boolean param_1 = obj.enQueue(value);
 * boolean param_2 = obj.deQueue();
 * int param_3 = obj.Front();
 * int param_4 = obj.Rear();
 * boolean param_5 = obj.isEmpty();
 * boolean param_6 = obj.isFull();
 */
 
```

## 第四题：设计循环双端队列 https://leetcode.cn/problems/design-circular-deque/
```java
class MyCircularDeque {
        /**
         * 1.构造一个长度为k+1的数组，避免判断队列为空和为满冲突
         * 2.front指针指向队列头元素，rear指向下一个要插入的队尾元素位置
         * 3.rear + 1 = front
         */
        private int[] deque;
        private int front;
        private int rear;
        private int capacity;

        public MyCircularDeque(int k) {
            capacity = k + 1;
            deque = new int[capacity];
            front = 0;
            rear = 0;
        }

        public boolean insertFront(int value) {
            /**
             * 先判断是否满了
             * 从头插入，指针向前移动，减一
             * 注意front=0越界
             */
            if (isFull()) {
                return false;
            }
            front = (front - 1 + capacity) % capacity;
            deque[front] = value;
            return true;
        }

        public boolean insertLast(int value) {
            /**
             * 先判断是否满了
             * 从尾插入，指针向后移动，+1
             * 注意越界
             */
            if (isFull()) {
                return false;
            }
            deque[rear] = value;
            rear = (rear + 1) % capacity;
            return true;
        }

        public boolean deleteFront() {
            if (isEmpty()) {
                return false;
            }
            front = (front + 1) % capacity;
            return true;

        }

        public boolean deleteLast() {
            if (isEmpty()) {
                return false;
            }
            rear = (rear - 1 + capacity) % capacity;
            return true;
        }

        public int getFront() {
            if (isEmpty()) {
                return -1;
            }

            return deque[front];
        }

        public int getRear() {
            if (isEmpty()) {
                return -1;
            }

            return deque[(rear - 1 + capacity) % capacity];

        }

        public boolean isEmpty() {
            return front == rear;
        }

        public boolean isFull() {
            return (rear + 1) % capacity == front;
        }
    }

/**
 * Your MyCircularDeque object will be instantiated and called as such:
 * MyCircularDeque obj = new MyCircularDeque(k);
 * boolean param_1 = obj.insertFront(value);
 * boolean param_2 = obj.insertLast(value);
 * boolean param_3 = obj.deleteFront();
 * boolean param_4 = obj.deleteLast();
 * int param_5 = obj.getFront();
 * int param_6 = obj.getRear();
 * boolean param_7 = obj.isEmpty();
 * boolean param_8 = obj.isFull();
 */
```

## TODO: 将后续题刷完
