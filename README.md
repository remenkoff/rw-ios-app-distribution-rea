# rw-ios-app-distribution-rea

Sinopsis and practical part of the "iOS App Distribution" book.

## TOC
- [Chapter 1. The App Store](#chapter-1-the-app-store)
  * [App Development Lifecycle](#app-development-lifecycle)
- [Chapter 2. First App in the App Store](#chapter-2-first-app-in-the-app-store)
  * [Creating a developer account](#creating-a-developer-account)
  * [Enrolling in the Apple Developer Program](#enrolling-in-the-apple-developer-program)
  * [Installing Xcode](#installing-xcode)
  * [Installing the app on a device](#installing-the-app-on-a-device)
  * [Creating a distribution certificate](#creating-a-distribution-certificate)
  * [Uploading an app with Xcode](#uploading-an-app-with-xcode)

----

## Chapter 1. The App Store

### App Development Lifecycle
- `Development` (making the app)
- `Upload` (packaging and uploading for further downloading by others)
- `Testing`
- `Product Page` (marketing and App Store product page decoration inclides setting the app’s price, adding screenshots, writing compelling descriptions, etc.)
- `App Review` (real Apple employees look at your app submission to make sure it meets the App Store Review Guidelines)
- `App Store` (approved version becomes available in the App Store)
- `Analytics` (analytics, app reviews and crash reports)

Notes:
- Versions of the app:
  - `Development`
  - `Alpha`
  - (`Beta`)
  - `Production`
- `CI` — continuous integration
- `CD` — continuous delivery

## Chapter 2. First App in the App Store

### Creating a developer account
1. Create an Apple ID and enable two-factor authentication.
1. Enroll in the Apple Developer Program.
1. Download and install Xcode.
1. Configure your app in the App Store’s backend system.

Notes:
- `Apple ID` identifies a user in Apple’s ecosystem
- How to create a new Apple ID: https://apple.co/2S18AzU
- `Two-factor authentication` for Apple ID: https://apple.co/3kIy1CA

### Enrolling in the Apple Developer Program
[Apple Developer Program](https://apple.co/303Kt8j) (need to pay $99 once per team) gives:
1. Software development kits (SDKs) for all Apple platforms.
1. Beta versions of the SDKs and developer tools when available.
1. Advanced app capabilities like In-App Purchases, push notifications and CloudKit.
1. Developer relations and editorial support. Entire teams at Apple support developers and feature the best apps on the App Store.
1. Code-level support. You can ask two detailed code-level questions per year.
1. Special programs and events like the option to attend WWDC.
1. App Store distribution.

Types of Enrollments:
- `Individuals/sole proprietorship` (if you decided to use your personal Apple ID)
- `Organization` (if you’re publishing an app for your employer, but you need to sign up for a [D-U-N-S](https://apple.co/308Ikbq) number through Dun & Bradstreet before you can complete your enrollment)

List of Roles:
- Account Holder (that’s you!)
- Admin
- App Manager
- Developer
- Finance
- Marketing
- Sales

Notes:
- When you complete the enrollment, you automatically become your team’s `Account Holder`
- The Account Holder role used to be called «Team Agent»
- Identify the app’s publisher and use **The app publisher's Apple developer account** whenever you start a new project
- Use **your client's Apple developer account** if you are a contractor or consultant

### Installing Xcode
Versions of Xcode:
1. **The current version** (macOS App Store)
1. **The gold master (GM) version** (version of Xcode to upload apps that rely on pre-released SDK features)
1. **Beta versions** (beta versions are used for testing and development, you can't upload and distribute apps to the App Store with them)

Notes:
- Download `Xcode` IDE
- Enable `Developer Mode`
- Install `additional components` to support running and debugging
- `Organization Name`
- `Organization Identifier` (its may be reverse DNS notation of the app publisher’s website, e.g. «com.publisher»)
- `Bundle ID`:
  - its *organization identifier* followed by *product name*
  - it uniquely identifies an app throughout Apple’s systems
  - you can’t change your app’s *bundle identifier* later on
- Select `Project File` → Select `Target` → Select `Signing and Capabilities`:
  - Check `Automatically manage signing` (requires to sign in Xcode with the Apple ID)
  - Set `Team` in `Signing` section
- Xcode → Preferences → Accounts:
  - Add Account (+) → Apple ID → Continue (sings Xcode in with Apple ID)
  - Manage Certificates → Add Certificate (+) → Apple Development (creates a `development certificate`)

### Installing the app on a device
Notes:
- `Trust` macOS when iPhone ask for it so iOS could give it required access
- To change target to install your app from simulator to the connected iPhone, in Xcode select `Toolbar` → `Scheme` → (*pop-up*) → `iOS Device` → *Connected iPhone Name*
- To build and install application, click `Toolbar` → `Run` (CMD+R)
- To register device with your developer account, click `Register Device` (***codesign*** adds a cryptographic signature to your app so Apple can make sure no one has tampered with it once a device wants to install it)

### Creating a distribution certificate
Notes:
- To make Xcode able to submit app to the App Store, `distribution certificate` must be created
- To create distribution certificate, go to Xcode → Preferences → Accounts, select `Manage Certificates` → Add certificate (`+` button) → Apple Distribution

### Uploading an app with Xcode
Notes:
- When you submit an app to the App Store, you're submitting an `archive` (a.k.a.`build` with additional debugging information) of the app
- `build` is an executable program that contains everything your app needs to run on a device: the compiled source code, embedded artwork, even the app icon
- `Any iOS Device (arm 64)` (special configuration that tells Xcode you just want to create a build for a special hardware configuration for further *archiving*)
- To create an archive, click Xcode Menu → `Product` → `Archive`
- `Organizer` (Xcode tool that manages archived builds of the different apps that you work on)
- To begin uploading build, open `Organizer` (CMD + Option + Shift + O) then select app and its archive (build) and click `Distribute App`
- `App Store Connect` (App Store’s admin interface for developers)
- **Methods of distribution**:
  - `App Store Connect` (to distribute on TestFlight and the App Store)
  - `Ad Hoc` (to install on designated devices)
  - `Enterprise` (to internal distribute to organization)
  - `Development` (to distribute to members of *team*)
- **Destinations of distribution**:
  - `Upload` (send app to App Store Connect)
  - `Export` (sign and export without uploading)
- **App Store Connect distribution options**:
  - `Include bitcode in iOS content` (allows the App Store to build your app to take advantage of hardware, software or compiler changes; improves the performance of the app)
  - `Upload your app's symbols to ceceive symbolicated reports from Apple` (crash logs and other diagnostic information from your customers will be symbolicated and viewable within Xcode)
- **Signing options during distribution**:
  - `Automatically manage signing` (Xcode will create and update profiles, app IDs, and certificates)
  - `Manually manage signing` (Select certificates and profiles from your *team*)  
> *codesign* might prompt you for a password in Keychain Access so it could sign the build
- **Reviewing content of distribution stage**:
  - Verify all your selections on the review screen
    - If everything checks out, click `Upload`
    - Otherwise, click `Previous` and fix what you need
- **Errors that may occur during upload process**:
  - `«No suitable application records were found»` (most likely you didn’t configure *application record* in App Store Connect)
  - etc.
- Ways to upload a build to App Store:
  - `Distribute App` within `Xcode`'s `Organizer`
  - Using `xcodebuild` CLI utility
  - `Transporter` (macOS application)
