# Grouping Subviews for Accessible Collection View Cells

By default, the subviews of a **custom** `UICollectionViewCell` are treated as separate accessibility elements by VoiceOver. This can be problematic if the cell contains multiple subviews, such as a title label, subtitle label, and an image, which can be challenging to navigate for some users.

To address this issue, we can use the technique of treating the cell as a single element by setting the `isAccessibilityElement` property of the cell to true, disabling the accessibility elements of its subviews, and setting the `accessibilityLabel` property to a combination of the titleLabel and subtitleLabel text.

```swift
class MyCollectionViewCell: UICollectionViewCell {
    @IBOutlet weak var titleLabel: UILabel!
    @IBOutlet weak var subtitleLabel: UILabel!

    func configureAccessibility() {
        titleLabel.isAccessibilityElement = false
        subtitleLabel.isAccessibilityElement = false
        isAccessibilityElement = true
        accessibilityLabel = "\(titleLabel.text ?? ""), \(subtitleLabel.text ?? "")"
    }

    // Other methods and properties
}
```

| Not Grouped | Grouped |
| ----------- | ----------- |
| <video src='https://user-images.githubusercontent.com/6307250/231303003-9bbb4516-ae35-471f-a816-6a85068cc888.mov'> | <video src='https://user-images.githubusercontent.com/6307250/231303012-a3468b8a-839b-47c8-afe3-f8534028acb9.MP4'> |


