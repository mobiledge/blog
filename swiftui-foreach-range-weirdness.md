# Weirdness of SwiftUI's `ForEach` Constructor with Ranges

In SwiftUI, when using a `Range` of integers with `ForEach`, a constant range can be used as an argument without an `id`, but a non-constant range requires an `id` parameter. This is because the compiler considers the range non-constant at runtime even if it's declared using let. Example:

```swift
// No warning:
ForEach(0..<10) { number in
    Text("\(number)")
}

// Warning: Non-constant range
let numbers = 0..<10
ForEach(numbers) { number in
    Text("\(number)")
}

// No warning with `id` parameter
let numbers = 0..<10
ForEach(numbers, id: \.self) { number in
    Text("\(number)")
}
```
