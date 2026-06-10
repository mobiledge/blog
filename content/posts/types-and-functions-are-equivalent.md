---
title: "Types & Functions Are Equivalent"
date: 2026-06-10
categories: ["Coding"]
tags: ["Swift", "Functional Programming"]
summary: "How a type and a function can be equivalent in Swift — declaring the same thing as a struct or as a function returning closures."
---

It just occurred to me that types and functions are equivalent in the sense that one can declare a type in the form of a function. I'd never thought of it this way.

```swift
struct Circle {
    let radius: Double

    func area() -> Double {
        .pi * radius * radius
    }

    func perimeter() -> Double {
        2 * .pi * radius
    }
}

let circle = Circle(radius: 5)
circle.radius       // 5.0
circle.area()       // 78.54
circle.perimeter()  // 31.42
```

```swift
func makeCircle(radius: Double) -> (
    radius: () -> Double,
    area: () -> Double,
    perimeter: () -> Double
) {
    func getRadius() -> Double { radius }
    func area() -> Double { .pi * radius * radius }
    func perimeter() -> Double { 2 * .pi * radius }

    return (getRadius, area, perimeter)
}

let circle = makeCircle(radius: 5)
circle.radius()     // 5.0
circle.area()       // 78.54
circle.perimeter()  // 31.42
```
