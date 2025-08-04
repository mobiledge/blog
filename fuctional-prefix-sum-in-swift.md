# Functional Prefix Sum in Swift

A prefix sum of an array is a new array where each element is the sum of all previous elements plus the current element in the original array. For example, given the array `[3, 1, 4, 1, 5]`, its prefix sum would be: `[3, 4, 8, 9, 14]`. Prefix sums show up in various algorithms and data structure problems and are useful for quickly calculating the sum of any subarray.

The most straightforward way to calculate a prefix sum in Swift is with a simple loop:
```swift
var result = Array(repeating: 0, count: nums.count)
result[0] = nums[0]    
for i in 1..<nums.count {
    result[i] = result[i-1] + nums[i]
}
```

An alternative implementation using `reduce(into:)` might look like this:
```swift
let prefixSum = nums.reduce(into: []) { sums, num in
    sums.append((sums.last ?? 0) + num)
}
```

## Prefix Sums in Kotlin
Other languages provide slightly better ergonomics for doing this. For example, in Kotlin using the `runningReduce()` function that takes no initial value:
```kotlin
val numbers = listOf(3, 1, 4, 1, 5)
val prefixSum1 = numbers.runningReduce { acc, num -> acc + num }
println(prefixSum1)  // [3, 4, 8, 9, 14]
```

## Prefix Sums in Haskell
Haskell offers `scanl` and `scanr` functions:
```haskell
-- Left-to-right prefix sum with scanl
prefixSum = scanl (+) 0 [3, 1, 4, 1, 5]
-- Result: [0, 3, 4, 8, 9, 14]

-- Right-to-left suffix sum with scanr
suffixSum = scanr (+) 0 [3, 1, 4, 1, 5]
-- Result: [14, 11, 10, 6, 5, 0]
```

The `scanl` function accumulates values from left to right, while `scanr` accumulates from right to left. Both include the initial value in their results.

> TODO: Try and attempt to do something similar in Swift as an Array Extension such that calculating prefix sums becomes more elegant. I'll explore this implementation in the near future.

## Variants
In certain problems (like [this](https://leetcode.com/problems/product-of-array-except-self/) one), it is more convinient to construct the prefix array as the sum of all previous elements NOT INCLUDING the current element.

```swift
var prefix2 = Array(repeating: 0, count: nums.count)
for i in 1..<nums.count {
    prefix2[i] = prefix2[i-1] + nums[i-1]
}
print(prefix2) /// [0, 3, 4, 8, 9]
```

Similarly, constructing a postfix array NOT INCLUDING the current element:

```swift
var postfix = Array(repeating: 0, count: nums.count)
postfix[nums.count - 1] = 0
for i in stride(from: nums.count - 2, through: 0, by: -1) {
    postfix[i] = postfix[i+1] + nums[i+1]
}
print(postfix) /// [11, 10, 6, 5, 0]
```
