Problem:
```
Design your implementation of the circular queue. The circular queue is a linear data structure in which the operations are performed based on FIFO (First In First Out) principle and the last position is connected back to the first position to make a circle. It is also called "Ring Buffer".

One of the benefits of the circular queue is that we can make use of the spaces in front of the queue. In a normal queue, once the queue becomes full, we cannot insert the next element even if there is a space in front of the queue. But using the circular queue, we can use the space to store new values.

Implementation the MyCircularQueue class:

MyCircularQueue(k) Initializes the object with the size of the queue to be k.
int Front() Gets the front item from the queue. If the queue is empty, return -1.
int Rear() Gets the last item from the queue. If the queue is empty, return -1.
boolean enQueue(int value) Inserts an element into the circular queue. Return true if the operation is successful.
boolean deQueue() Deletes an element from the circular queue. Return true if the operation is successful.
boolean isEmpty() Checks whether the circular queue is empty or not.
boolean isFull() Checks whether the circular queue is full or not.
You must solve the problem without using the built-in queue data structure in your programming language. 
```

```scala
Input
["MyCircularQueue", "enQueue", "enQueue", "enQueue", "enQueue", "Rear", "isFull", "deQueue", "enQueue", "Rear"]
[[3], [1], [2], [3], [4], [], [], [], [4], []]
Output
[null, true, true, true, false, 3, true, true, true, 4]

Explanation
MyCircularQueue myCircularQueue = new MyCircularQueue(3);
myCircularQueue.enQueue(1); // return True
myCircularQueue.enQueue(2); // return True
myCircularQueue.enQueue(3); // return True
myCircularQueue.enQueue(4); // return False
myCircularQueue.Rear();     // return 3
myCircularQueue.isFull();   // return True
myCircularQueue.deQueue();  // return True
myCircularQueue.enQueue(4); // return True
myCircularQueue.Rear();     // return 4
```

<details><summary>Pre-order</summary>

```scala
class MyCircularQueue(_k: Int) {
  val listLength = _k
  var currentLength = 0

  var queue: List[Int] = List()

  def enQueue(value: Int): Boolean = {
      if(currentLength + 1 <= listLength){
        currentLength = currentLength + 1
        queue = queue ++ List(value)
        true
      } else {
        false
      }
  }

  def deQueue(): Boolean = {
    println(currentLength)
    if(!this.isEmpty()){
      currentLength = currentLength - 1
      queue = queue.tail
      true
    } else {
      false
    }
  }

  def Front(): Int = {
    if(this.isEmpty()){
      -1
    } else {
      queue.head
    }
  }

  def Rear(): Int = {
    if(this.isEmpty()){
      -1
    } else {
      queue.last
    }
  }

  def isEmpty(): Boolean = {
    currentLength == 0
  }

  def isFull(): Boolean = {
    currentLength == listLength
  }

}

/**
 * Your MyCircularQueue object will be instantiated and called as such:
 * var obj = new MyCircularQueue(k)
 * var param_1 = obj.enQueue(value)
 * var param_2 = obj.deQueue()
 * var param_3 = obj.Front()
 * var param_4 = obj.Rear()
 * var param_5 = obj.isEmpty()
 * var param_6 = obj.isFull()
 */
```

Runtime: `O(N)` 

</details>


Problem:
```
Given a stream of integers and a window size, calculate the moving average of all integers in the sliding window.

Implement the MovingAverage class:

MovingAverage(int size) Initializes the object with the size of the window size.
double next(int val) Returns the moving average of the last size values of the stream.
```

```scala
Input
["MovingAverage", "next", "next", "next", "next"]
[[3], [1], [10], [3], [5]]
Output
[null, 1.0, 5.5, 4.66667, 6.0]

Explanation
MovingAverage movingAverage = new MovingAverage(3);
movingAverage.next(1); // return 1.0 = 1 / 1
movingAverage.next(10); // return 5.5 = (1 + 10) / 2
movingAverage.next(3); // return 4.66667 = (1 + 10 + 3) / 3
movingAverage.next(5); // return 6.0 = (10 + 3 + 5) / 3
```

<details><summary>Pre-order</summary>

```scala
import scala.collection.mutable

class MovingAverage(_size: Int) {
  val maxSize = _size
  var currentSize = 0
  val queue = mutable.Queue[Int]()
  
  def next(`val`: Int): Double = {
    if(currentSize == maxSize){
      queue.dequeue()
      currentSize = currentSize - 1
    }
    
    queue.enqueue(`val`)
    currentSize = currentSize + 1

    queue.reduce(_ + _) / currentSize.toDouble
  }

}

/**
 * Your MovingAverage object will be instantiated and called as such:
 * var obj = new MovingAverage(size)
 * var param_1 = obj.next(`val`)
 */
```

Runtime: `O(N)` 

</details>

Problem:
```
You are given an m x n grid rooms initialized with these three possible values.

-1 A wall or an obstacle.
0 A gate.
INF Infinity means an empty room. We use the value 231 - 1 = 2147483647 to represent INF as you may assume that the distance to a gate is less than 2147483647.
Fill each empty room with the distance to its nearest gate. If it is impossible to reach a gate, it should be filled with INF.
```

```scala
Input: rooms = [[2147483647,-1,0,2147483647],[2147483647,2147483647,2147483647,-1],[2147483647,-1,2147483647,-1],[0,-1,2147483647,2147483647]]
Output: [[3,-1,0,1],[2,2,1,-1],[1,-1,2,-1],[0,-1,3,4]]
```

<details><summary>Pre-order</summary>

```scala
import scala.collection.mutable

object Solution {
  def wallsAndGates(rooms: Array[Array[Int]]): Unit = {
    val rows = rooms.length -1
    val cols = rooms(0).length -1
    val visited = mutable.Set[(Int, Int)]()
    val queue = mutable.Queue[(Int, Int)]()

    def addRoom(r: Int, c:Int): Unit = {
      if(r > rows || r < 0){ return }
      if(c > cols || c < 0) { return }
      if(visited.contains((r,c))){ return }
      if(rooms(r)(c) == -1) { return }

      visited.add((r,c))
      queue.enqueue((r,c))
    }

    for(r <- 0 to rows){
      for(c <- 0 to cols){
        if(rooms(r)(c) == 0){
          queue.enqueue((r,c))
          visited.add((r,c))
        }
      }
    }

    var dist = 0
    while (!queue.isEmpty){
      for(i <- 0 to queue.length - 1 ){
        var (r, c) = queue.dequeue()
        rooms(r)(c) = dist

        addRoom(r + 1, c)
        addRoom(r - 1, c)
        addRoom(r, c - 1)
        addRoom(r, c + 1)
      }

      dist = dist + 1
      
    }
  }
}
```

Runtime: `O(N*M)` 

</details>