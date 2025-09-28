---
title: Setting up Google Admob in SwiftUI
description: This article goes through the steps for setting an account in Google's AdMob and then displaying ads in your SwiftUI app.
---

# Setting up Google Admob in SwitUI

Table of Contents
- [Google AdMob Setup](google-admob-setup)


## Overview

While there are other Ad networks you can incorporate into your app, Google's AdMob is the most widely used and is a good starting point for your app. 

## Google Admob Setup

1. Create an AdMob account
  - Go to [Google AdMob](https://admob.google.com/home/) and sign in with your Google account.
  - Accept terms and set up your payment profile.
2. Register your app
  - In the AdMob dashboard, click Apps → Add App.
  - Choose whether your app is already published on the App Store or not.
  - Enter your app’s name and select iOS.
3. Get the App ID
  - After adding the app, you’ll receive an App ID (looks like: `ca-app-pub-xxxxxxxx~yyyyyyyyy`).
  - You'll need this in your app’s **Info.plist**.
4. Create Ad Units
  - In your app’s AdMob dashboard, click **Ad Units → Add Ad Unit**.
  - Choose the type of ad (Banner, Interstitial, Rewarded, or App Open).
  - Each ad unit has its own Ad Unit ID (looks like: `ca-app-pub-xxxxxxxx/zzzzzzzz`).


## Xcode Project Setup (with Swift Package Manager)

### Add the SDK with SPM
- In Xcode, open your project.
- Go to **File → Add Packages...**.
- Enter the Google Mobile Ads SDK repo URL:
```
https://github.com/googleads/swift-package-manager-google-mobile-ads
```
- Pick the latest version (Google recommends “Up to Next Major”).
- Add the package to your app target.

### Add App ID to Info.plist
Inside your app’s Info.plist, add:
```
<key>GADApplicationIdentifier</key>
<string>ca-app-pub-xxxxxxxx~yyyyyyyyy</string>
```
(Replace with your actual App ID from AdMob.)

### Initialize Google Mobile Ads SDK
In your AppDelegate.swift:

```
import UIKit
import GoogleMobileAds

@main
class AppDelegate: UIResponder, UIApplicationDelegate {
    func application(_ application: UIApplication,
                     didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        GADMobileAds.sharedInstance().start(completionHandler: nil)
        return true
    }
}
```

If you’re only using SwiftUI (@main struct MyApp: App), you can initialize inside init:
```
import SwiftUI
import GoogleMobileAds

@main
struct MyApp: App {
    init() {
        GADMobileAds.sharedInstance().start(completionHandler: nil)
    }

    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```

## Using Ads in SwiftUI

### Banner Ad (SPM version)

```
import SwiftUI
import GoogleMobileAds

struct BannerAdView: UIViewRepresentable {
    let adUnitID: String

    func makeUIView(context: Context) -> GADBannerView {
        let banner = GADBannerView(adSize: GADAdSizeBanner)
        banner.adUnitID = adUnitID
        banner.rootViewController = UIApplication.shared.windows.first?.rootViewController
        banner.load(GADRequest())
        return banner
    }

    func updateUIView(_ uiView: GADBannerView, context: Context) {}
}
```

Usage in SwiftUI:
```
struct ContentView: View {
    var body: some View {
        VStack {
            Text("Hello, AdMob!")
                .font(.largeTitle)
            Spacer()
            BannerAdView(adUnitID: "ca-app-pub-3940256099942544/2934735716") // Test ID
        }
    }
}
```


### Interstitial Ad (SPM version)

```
import GoogleMobileAds

class InterstitialAd: NSObject, GADFullScreenContentDelegate {
    private var interstitial: GADInterstitialAd?

    func loadAd() {
        GADInterstitialAd.load(
            withAdUnitID: "ca-app-pub-3940256099942544/4411468910",
            request: GADRequest()
        ) { ad, error in
            if let error = error {
                print("Failed to load interstitial: \(error)")
                return
            }
            self.interstitial = ad
            self.interstitial?.fullScreenContentDelegate = self
        }
    }

    func showAd(from root: UIViewController) {
        if let ad = interstitial {
            ad.present(fromRootViewController: root)
        } else {
            print("Ad not ready")
        }
    }
}
```

Usage in SwiftUI:
```
struct ContentView: View {
    @State private var interstitial = InterstitialAd()

    var body: some View {
        Button("Show Interstitial Ad") {
            interstitial.loadAd()
            DispatchQueue.main.asyncAfter(deadline: .now() + 2) {
                if let root = UIApplication.shared.windows.first?.rootViewController {
                    interstitial.showAd(from: root)
                }
            }
        }
    }
}
```

## Testing & Deployment
- Always test with Google’s test IDs before switching to real Ad Unit IDs.
- Replace with your own IDs only before App Store release.
- Ensure you comply with [AdMob policies](https://support.google.com/admob/answer/6128543).




