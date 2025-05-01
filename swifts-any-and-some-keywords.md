#  Swift's 'any' and 'some' keywords

When using `any`, under the hood, Swift implements a wrapper structure with closures that mirror the protocol methods.

```swift
// When you write:
protocol Drawable {
    func draw()
}

// It's conceptually similar to:
struct AnyDrawable {
    private let _value: Any
    private let _drawMethod: () -> Void
    
    init<T: Drawable>(_ value: T) {
        self._value = value
        self._drawMethod = { value.draw() }
    }
    
    func draw() {
        _drawMethod()
    }
}
```

Similarly, here's what `some` can be thought of as:

```swift
// When you write:
func createDrawable() -> some Drawable {
    return Circle()
}

// It's conceptually similar to:
func createDrawable<T: Drawable>() -> T where T == Circle {
    return Circle()
}
```
