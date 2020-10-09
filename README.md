docsdk-swift
=======================

This is a lightweight wrapper for the [DocSDK](https://docSDK.com) API, written in Swift. It is compatible with iOS 9.0+ / Mac OS X 10.9+ and requires Xcode 9.0.

Feel free to use, improve or modify this wrapper! If you have questions contact us or open an issue on GitHub.




## Quickstart

```Swift
import DocSDK

DocSDK.apiKey = "your_api_key"

let inputURL = NSBundle.mainBundle().URLForResource("file",withExtension: "png")!
let outputURL = NSFileManager.defaultManager().URLsForDirectory(.DocumentDirectory, inDomains: .UserDomainMask)[0] as? NSURL

DocSDK.convert([
                    "inputformat": "png",
                    "outputformat" : "pdf",
                    "input" : "upload",
                    "file": inputURL,
                    "download": outputURL
                ],
                progressHandler: { (step, percent, message) -> Void in
                    print(step! + " " + percent!.description + "%: " + message!)
                },
                completionHandler: { (path, error) -> Void in
                    if(error != nil) {
                        print("failed: " + error!.description)
                    } else {
                        println("done! output file saved to: " + path!.description)
                    }   
            })
```

You can use the [DocSDK API Console](https://docsdk.com/apiconsole) to generate ready-to-use Swift code snippets using this wrapper.


## Installation


### CocoaPods

[CocoaPods](http://cocoapods.org) is a dependency manager for Cocoa projects.

CocoaPods 0.36 adds supports for Swift and embedded frameworks. You can install it with the following command:

```bash
gem install cocoapods
```

To integrate DocSDK into your Xcode project using CocoaPods, specify it in your `Podfile`:

```ruby
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '9.0'
use_frameworks!

pod 'DocSDK', '~> 1.0'
```

Then, run the following command:

```bash
pod install
```

### Manually
If you prefer not to use CocoaPods, you can integrate DocSDK into your project manually.
As DocSDK depends on [Alamofire](https://github.com/Alamofire/Alamofire), you need to add [Alamofire.swift](https://github.com/Alamofire/Alamofire/blob/master/Source/Alamofire.swift) to your Xcode Project first. Afterwards you can add the [DocSDK.swift](https://github.com/docSDK/docsdk-swift/blob/master/Source/docsdk.swift) Source file.

Note that any calling conventions described in this README with the DocSDK prefix would instead omit it (for example, ``DocSDK.convert`` becomes ``convert``), since this functionality is incorporated into the top-level namespace.


## Example Project

It is a good starting point to have a look at the DocSDK Example project in this repository. It shows how to find possible conversion types, start and monitor a conversions and how to cancel a conversion.

To open the project:

* Checkout (or download) this repository
* Execute ``pod install`` in the DocSDKExample folder
* Open DocSDKExample***.xcworkspace*** in the DocSDKExample folder with Xcode

## Resources

* [API Documentation](https://docsdk.com/apidoc)
* [Conversion Types](https://docsdk.com/formats)
* [DocSDK Blog](https://docsdk.com/blog)
