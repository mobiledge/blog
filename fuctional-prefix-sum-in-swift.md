# Fuctional Prefix Sum in Swift

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

Other languages provice slightly better ergonomics of doing this. For example, in Kotlin using the `runningReduce()` function that takes no initial value.

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
-- scanr :: (a -> b -> b) -> b -> [a] -> [b]
suffixSum = scanr (+) 0 [3, 1, 4, 1, 5]
-- Result: [14, 11, 10, 6, 5, 0]
```

The `scanl` function accumulates values from left to right, while `scanr` accumulates from right to left. Both include the initial value in their results.

## Implementing `scanL` in Swift as an Array Extension

We can add this functional capability to Swift by implementing a `scanl` extension on Array:

```swift
extension Array {
    func scanl<Result>(_ initial: Result, _ combine: (Result, Element) -> Result) -> [Result] {
        var result = [initial]
        var accumulated = initial
        
        for element in self {
            accumulated = combine(accumulated, element)
            result.append(accumulated)
        }
        
        return result
    }
}
```

With this extension, calculating prefix sums becomes elegantly simple:

```swift
let numbers = [3, 1, 4, 1, 5]
let prefixSum = numbers.scanl(0, +)
// Result: [0, 3, 4, 8, 9, 14]
```
