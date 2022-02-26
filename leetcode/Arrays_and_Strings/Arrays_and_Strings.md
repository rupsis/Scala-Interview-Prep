Problem:
```
Given a string s, find the length of the longest substring without repeating characters.
```

```scala
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

<details><summary>Solution</summary>

```scala
def lengthOfLongestSubstring(s: String): Int = {
      val indices = mutable.Map[Char, Int]()
      var left = 0
      var longest = 0
      println(s.zipWithIndex)
      for ((char, right) <- s.zipWithIndex) {
        indices.get(char).foreach{ i =>
          left = left max (i + 1)
        }
        longest = longest max (right - left + 1)
        indices.put(char, right)
      }
      longest
    }
```
</details>

---

Problem:
```
Given a binary array nums, return the maximum number of consecutive 1's in the array.
```

```scala
Input: nums = [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s. The maximum number of consecutive 1s is 3.
```

<details><summary>Solution</summary>

```scala
object Solution {
    def findMaxConsecutiveOnes(nums: Array[Int]): Int = {
      var counter = 0
      var maxNum = 0
      nums.zipWithIndex.foreach{ n =>
         if(n._1 == 1) {
           counter = counter + 1
         } else {
           maxNum = maxNum max counter
           counter = 0
         }

        if(n._2 == nums.length - 1){
          maxNum = maxNum max counter
        }
      }

      maxNum
    }
}
```
</details>

---

Problem:
```
Given an array nums of integers, return how many of them contain an even number of digits.
```

```scala
Input: nums = [12,345,2,6,7896]
Output: 2
Explanation: 
12 contains 2 digits (even number of digits). 
345 contains 3 digits (odd number of digits). 
2 contains 1 digit (odd number of digits). 
6 contains 1 digit (odd number of digits). 
7896 contains 4 digits (even number of digits). 
Therefore only 12 and 7896 contain an even number of digits.
```

<details><summary>Solution</summary>

```scala
object Solution {
    def findNumbers(nums: Array[Int]): Int = {
      nums.filter(_.toString.length % 2 == 0).length
    }
}
```
</details>

---

Problem:
```
Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.
```

```scala
Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].
```

<details><summary>Solution</summary>

```scala
object Solution {
    def sortedSquares(nums: Array[Int]): Array[Int] = {
      nums.map(x => x * x).sorted
    }
}
```
</details>

---

Problem:
```
Given a fixed-length integer array arr, duplicate each occurrence of zero, shifting the remaining elements to the right.

Note that elements beyond the length of the original array are not written. Do the above modifications to the input array in place and do not return anything.
```

```scala
Input: arr = [1,0,2,3,0,4,5,0]
Output: [1,0,0,2,3,0,0,4]
Explanation: After calling your function, the input array is modified to: [1,0,0,2,3,0,0,4]
```

<details><summary>Solution</summary>

```scala
object Solution {
    def duplicateZeros(arr: Array[Int]): Unit = {
      var arr_2: Seq[Int] = Seq()
      arr.foreach{a =>
        if( arr_2.length < arr.length){
          if(a == 0){
            arr_2 = arr_2 ++ Seq(0,0)
          } else {
            arr_2 = arr_2 ++ Seq(a)
          }
        }
      }

      for(i <- 0 to arr.length - 1){
        arr(i) = arr_2(i)
      }
    }
}
```

Runtime: `O(N)`

</details>

---