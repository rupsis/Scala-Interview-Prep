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
