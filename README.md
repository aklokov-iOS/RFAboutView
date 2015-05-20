# RFAboutView

[![Version](https://img.shields.io/cocoapods/v/RFAboutView.svg?style=flat)](http://cocoapods.org/pods/RFAboutView)
[![License](https://img.shields.io/cocoapods/l/RFAboutView.svg?style=flat)](http://cocoapods.org/pods/RFAboutView)
[![Platform](https://img.shields.io/cocoapods/p/RFAboutView.svg?style=flat)](http://cocoapods.org/pods/RFAboutView)

**RFAboutView** is an easy, drop-in solution to display copyright, support, privacy and other information while also automatically crediting the developers of third-party Cocoapods. RFAboutView uses AutoLayout and can be used both for iPhone and iPad apps.

It's main features are:

* Displays app name and copyright information.
* Displays an optional link to a website, opening in Safari.
* Displays an optional link to an Email address.
* If the user clicks on the Email link, a `MFMailComposeViewController` opens, (optionally) prefilled with diagnostic information useful for support: App name and version, current device, current iOS version, preferred device language.
* Displays additional buttons with further information (for example your TOS or Privacy Policy) that you can specify.
* Displays acknowledgements for all Cocoapods used in the project. The acknowledgements file automatically created by Cocoapods is used for this, requiring almost no work on your part. See the "Automatic acknowledgements" below for more information.
* Clean and modern design with lots of customization options.

## Screenshots

![https://fouquet.me/RFAboutView/screenshot1.png](Screenshot 1)
![https://fouquet.me/RFAboutView/screenshot2.png](Screenshot 1)
![https://fouquet.me/RFAboutView/screenshot3.png](Screenshot 1)

## Usage

To use RFAboutView, import the header:
```objective-c
#import "RFAboutViewController.h"`
```

After that, initialise a RFAboutViewController and add it to a UINavigationController. The RFAboutViewController must always be used in navigation stack. Here is a complete example:

```objective-c
// First create a UINavigationController (or use your existing one).
// The RFAboutView needs to be wrapped in a UINavigationController.
    
UINavigationController *aboutNavigation = [UINavigationController new];

// Initialise the RFAboutView:
    
RFAboutViewController *aboutView = [[RFAboutViewController alloc] initWithAppName:nil appVersion:nil appBuild:nil copyrightHolderName:@"ExampleApp, Inc." contactEmail:@"mail@example.com" titleForEmail:@"Contact us" websiteURL:[NSURL URLWithString:@"http://example.com"] titleForWebsiteURL:@"Our Website" andPublicationYear:nil];
    
// Set some additional options:
aboutView.headerBackgroundColor = [UIColor blackColor];
aboutView.headerTextColor = [UIColor whiteColor];
aboutView.blurStyle = UIBlurEffectStyleDark;
aboutView.headerBackgroundImage = [UIImage imageNamed:@"about_header_bg.jpg"];

// Add an additional button:
[aboutView addAdditionalButtonWithTitle:@"Privacy Policy" andContent:@"Here's the privacy policy"];

// Add the aboutView to the NavigationController:
[aboutNavigation setViewControllers:@[aboutView]];
    
// Present the navigation controller:
[self presentViewController:aboutNavigation animated:YES completion:nil];
```

## Automatic acknowledgements

Every time you run `pod update` or `pod install`, Cocoapods automatically generates a file containing copyright and license information for all Cocoapods used in the project. RFAboutView uses this file to display the acknowledgements. To use it, copy the file `Pods-<Target Name>-acknowledgements.plist` found in the `<Project Root>/Pods/Target Support Files/Pods-<Target Name>` directory to your project and call it `Acknowledgements.plist`. You can also use a different name if you would like – if you do, set the `acknowledgementsFilename` property of `RFAboutViewController` to the new name.

To automate this, you can add the following snippet to your `Podfile`:

```ruby
post_install do |installer|
  require 'fileutils'
  FileUtils.cp_r('Pods/Target Support Files/Pods-<Target Name>/Pods-<Target Name>-acknowledgements.plist', '<Project Dir>/Acknowledgements.plist', :remove_destination => true)
end
```
Note that the directory names can differ based on whether or not you are using different targets or not. Check with your local project directory and change the snippet accordingly. Also don't forget to add the `Acknowledgements.plist` file to your Xcode project.

## Example Project

To run the example project, clone the repo, and run `pod install` from the Example directory first.

## Requirements

RFAboutView requires iOS 8.0.

## Installation

RFAboutView is available through [CocoaPods](http://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
pod "RFAboutView", '~> 1.0.0'
```

## Author

René Fouquet, mail@fouquet.me

Check out my blog: [fouquet.me](http://fouquet.me)

Follow me on Twitter at @renefouquet

## License

RFAboutView is available under the MIT license. See the LICENSE file for more info.