# SwiftyAppearance

[![Pod Version](https://img.shields.io/cocoapods/v/SwiftyAppearance.svg?style=flat)](http://cocoapods.org/pods/SwiftyAppearance)
[![Carthage: compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)
[![License: MIT](https://img.shields.io/badge/license-MIT-3b3b3b.svg?style=flat)](https://github.com/victor-pavlychko/SwiftyAppearance/blob/master/LICENSE)
[![Swift: 3.0](https://img.shields.io/badge/swift-3.0-orange.svg?style=flat)](https://github.com/victor-pavlychko/SwiftyAppearance)
[![Platform: iOS](https://img.shields.io/badge/platform-ios-lightgrey.svg?style=flat)](https://github.com/victor-pavlychko/SwiftyAppearance)

## Why UIAppearance

UIAppearance allows to set up global application look and feed in a single centralized location instead of
spreading bits of design across different classes, xibs and storyboards.

SwiftyAppearance adds a little bit of style to this approach.

## Example

To run the example project, clone the repo, and run `SwiftAppearanceDemo` app:

![Screenshot](https://raw.githubusercontent.com/victor-pavlychko/SwiftyAppearance/master/Screenshots/first.png)
![Screenshot](https://raw.githubusercontent.com/victor-pavlychko/SwiftyAppearance/master/Screenshots/second.png)

## Brief Walkthrough

To achieve best results with UIAppearance, avoid inheriting from UIKit base classes directly and insert custom
base classes instead. Consider class hierarchy like this: `UIViewController` → `AppViewController` → `UserListViewController`.
Doing so allows you to apply appearance to all view controllers across the app while leaving third-party screens
like SMS or Mail composers intact.

Also it is useful to create custom `BackgroundView` class to be used instead of `UIView` as a root view for most
view vontrollers. This allows to customize view controller backgrounds globally and does not affect other views. 

Demo application defines following root classes for global styling:
* AppViewController
* AppTabBarController
* AppNavigationController
* AppBackgroundView

```swift
appearance(inAny: [AppViewController.self, AppTabBarController.self, AppNavigationController.self]) {
    UITabBar.appearance {
        $0.barStyle = .black
        $0.barTintColor = UIColor(rgb: 0x2c3e50)
        $0.tintColor = UIColor(rgb: 0xecf0f1)
    }
}
```

Also we define two navigation controller subclasses for different screens:
* FirstNavigationController
* SecondNavigationController

```swift
FirstNavigationController.appearance {
    UINavigationBar.appearance {
        $0.barStyle = .black
        $0.barTintColor = UIColor(rgb: 0x2980b9)
        $0.tintColor = UIColor(rgb: 0xecf0f1)
    }
}
```

```swift
SecondNavigationController.appearance {
    UINavigationBar.appearance {
        $0.barStyle = .`default`
        $0.barTintColor = UIColor(rgb: 0xf39c12)
        $0.titleTextAttributes = [NSForegroundColorAttributeName: UIColor(rgb: 0xc0392b)]
    }
}
```

And finslly we customize our view controllers

```swift
FirstViewController.appearance {
    AppBackgroundView.appearance {
        $0.backgroundColor = UIColor(rgb: 0xecf0f1)
        $0.tintColor = UIColor(rgb: 0x34495e)
    }
    UILabel.appearance {
        $0.textColor = UIColor(rgb: 0x2c3e50)
    }
}
```

```swift
SecondViewController.appearance {
    AppBackgroundView.appearance {
        $0.backgroundColor = UIColor(rgb: 0xf1c40f)
    }
    UILabel.appearance {
        $0.textColor = UIColor(rgb: 0xe67e22)
    }
}
```

## Installation 

### CocoaPods

To integrate SwiftyAppearance into your Xcode project using [CocoaPods](http://cocoapods.org), add the following line to your Podfile:

```ruby
pod "SwiftyAppearance"
```

### Carthage

To integrate SwiftyAppearance into your Xcode project using Carthage, specify it in your `Cartfile`:

```ogdl
github "victor-pavlychko/SwiftyAppearance"
```

### Just Copy Files

SwiftyAppearance consists of two files and has no external dependencies.
You can just copy files into your project.

## Author

Victor Pavlychko, victor.pavlychko@gmail.com

## License

SwiftyAppearance is available under the MIT license. See the LICENSE file for more info.
