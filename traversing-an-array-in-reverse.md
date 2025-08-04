# Traversing an Array in Reverse

Working on [this](https://leetcode.com/problems/product-of-array-except-self/description/) problem today, I needed to iterate through an array in reverse.

My first instinct was to use a range-based loop, since that's what I normally prefer. I found myself wondering if I could just do something simple like:

```swift
for i in (0..<nums.count).reversed() {
    print(nums[i]) 
}
```

But then, I was worried that creating a whole range and *then* reversing it might add unnecessary overhead. I thought maybe using `stride` was the more performant way to handle this. 

```swift
for i in stride(from: nums.count - 1, through: 0, by: -1) {
    print(nums[i])
}
```

After digging into it for a bit, it turns out that using `.reversed()` on a range is totally fine. The reason is that Swift handles this lazily. Creating the initial range is an $O(1)$ operation, and calling `.reversed()` on it is *also* an $O(1)$ operation. It doesn't actually build a new, reversed collection in memory; it just creates a lightweight view that knows how to iterate backwards over the original range.

That was really good to know, because I definitely prefer dealing with ranges over using `stride`. I just feel it's more readable and less cluttered than manually setting up the start, end, and step values. 


#### A Quick Note: `stride(through:)` vs. `stride(to:)`
- `stride(to: ...)` is exclusive. It will **not** include the end value.
- `stride(through: ...)` is inclusive. It will include the end value.
