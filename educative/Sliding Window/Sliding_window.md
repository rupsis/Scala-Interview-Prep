## Sliding Window 

Problem:
```
Given an array, find the average of all subarrays of ‘K’ contiguous elements in it.
```

```scala
Array: [1, 3, 2, 6, -1, 4, 1, 8, 2], K=5
```

<details><summary>Solution</summary>

```scala
Seq(1, 3, 2, 6, -1, 4, 1, 8, 2).sliding(5, 1).map{ window =>
  window.sum / window.size.toFloat
}.foreach(println(_)) // 2.2, 2.8, 2.4, etc
```
</details>

---

Problem:
```
Given an array, find the average of all subarrays of ‘K’ contiguous elements in it.
```

```scala
Array: [1, 3, 2, 6, -1, 4, 1, 8, 2], K=5
```

<details><summary>Solution</summary>

```scala
Seq(1, 3, 2, 6, -1, 4, 1, 8, 2).sliding(5, 1).map{ window =>
  window.sum / window.size.toFloat
}.foreach(println(_)) // 2.2, 2.8, 2.4, etc
```
</details>

---
