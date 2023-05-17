# Software Implementation Documentation

## Dependancies

```
name: VIITxSmartband
description: A new Flutter project.

# The following line prevents the package from being accidentally published to
# pub.dev using `flutter pub publish`. This is preferred for private packages.
publish_to: 'none' # Remove this line if you wish to publish to pub.dev

# The following defines the version and build number for your application.
# A version number is three numbers separated by dots, like 1.2.43
# followed by an optional build number separated by a +.
# Both the version and the builder number may be overridden in flutter
# build by specifying --build-name and --build-number, respectively.
# In Android, build-name is used as versionName while build-number used as versionCode.
# Read more about Android versioning at https://developer.android.com/studio/publish/versioning
# In iOS, build-name is used as CFBundleShortVersionString while build-number used as CFBundleVersion.
# Read more about iOS versioning at
# https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/CoreFoundationKeys.html
version: 1.0.0+1

environment:
  sdk: ">=2.17.6 <3.0.0"

# Dependencies specify other packages that your package needs in order to work.
# To automatically upgrade your package dependencies to the latest versions
# consider running `flutter pub upgrade --major-versions`. Alternatively,
# dependencies can be manually updated by changing the version numbers below to
# the latest version available on pub.dev. To see which dependencies have newer
# versions available, run `flutter pub outdated`.
dependencies:
  flutter:
    sdk: flutter


  # The following adds the Cupertino Icons font to your application.
  # Use with the CupertinoIcons class for iOS style icons.
  cupertino_icons: ^1.0.2
  bottom_navy_bar: ^6.0.0
  firebase_core: ^2.8.0
  firebase_auth: ^4.3.0
  firebase_database: ^10.0.16
  cloud_firestore: ^4.4.5
  google_fonts: ^4.0.3
  google_sign_in: ^5.4.4
  get: ^4.6.5
  carousel_slider: ^4.2.1
  carousel_indicator: ^1.0.6
  flutter_svg: ^1.1.6
  circular_chart_flutter: ^0.0.2
  syncfusion_flutter_core: 20.1.48
  syncfusion_flutter_charts: 20.1.48

dev_dependencies:
  flutter_test:
    sdk: flutter

  # The "flutter_lints" package below contains a set of recommended lints to
  # encourage good coding practices. The lint set provided by the package is
  # activated in the `analysis_options.yaml` file located at the root of your
  # package. See that file for information about deactivating specific lint
  # rules and activating additional ones.
  flutter_lints: ^2.0.0

# For information on the generic Dart part of this file, see the
# following page: https://dart.dev/tools/pub/pubspec

# The following section is specific to Flutter packages.
flutter:

  # The following line ensures that the Material Icons font is
  # included with your application, so that you can use the icons in
  # the material Icons class.
  uses-material-design: true

  # To add assets to your application, add an assets section, like this:
  assets:
     - lib/assets/LandingPageIllustrations/
     - lib/assets/Icons/
  #   - images/a_dot_ham.jpeg

  # An image asset can refer to one or more resolution-specific "variants", see
  # https://flutter.dev/assets-and-images/#resolution-aware

  # For details regarding adding assets from package dependencies, see
  # https://flutter.dev/assets-and-images/#from-packages

  # To add custom fonts to your application, add a fonts section here,
  # in this "flutter" section. Each entry in this list should have a
  # "family" key with the font family name, and a "fonts" key with a
  # list giving the asset and other descriptors for the font. For
  # example:
  # fonts:
  #   - family: Schyler
  #     fonts:
  #       - asset: fonts/Schyler-Regular.ttf
  #       - asset: fonts/Schyler-Italic.ttf
  #         style: italic
  #   - family: Trajan Pro
  #     fonts:
  #       - asset: fonts/TrajanPro.ttf
  #       - asset: fonts/TrajanPro_Bold.ttf
  #         weight: 700
  #
  # For details regarding fonts from package dependencies,
  # see https://flutter.dev/custom-fonts/#from-packages

```

## Models

### User Model
1. This model is used to represent the user, user is generated via Google SSO, which provides with User's Email, Display Name, Profile Pic URL etc.
2. Additional information such as height (cm) & weight (kg) is taken later
3. Date of Birth is stored as DateTime & Age is calculated everytime
```
User {
    "date_of_birth" : DateTime,
    "devices" : List<Devices>,
    "height_cm" : number,
    "is_profile_complete" : bool,
    "weight_kg" : number
}
```

### Device Model
1. This is the midel for the hardware device used
2. It stores the basic metadata of the hardware device
3. Provides a communication channel via use of access key, where once a command is putted we can get a response.
4. Tunning parameters can be changed based on user.

```
Device {
    "id" : str,
    "date_of_manufacturing" : DateTime,
    "device_name" : str,
    "device_description" : str,
    "featurs" : List<str>,
    "last_active" : DateTime,
    "wifi_cred" : {
        "ssid" : str,
        "psw_hash" : str
    },
    "tuning_param" : {
        "user_weight" : number,
        "delay" : {
          "jump" : number,
          "step" :number,
          "kick" : number
        },
        "jump" : {
          "x" : number,
          "y" : number,
          "z" : number
        },
        "step" : {
          "x" : number,
          "y" : number,
          "z" : number
        },
        "kick" : {
          "x" : number,
          "y" : number,
          "z" : number
        }
    },
    "monitoring_param" : {
        "jump" : number,
        "step" : number,
        "kick" : number
    },
    "access" : {
        "status" : str (values [start, stop]),
        "upload_delay" : number,
        "command" : str,
        "response" : str
    }
}
```


## Flutter Project Structure
```
lib
├── assets
│   ├── Icons
│   │   └── google.svg
│   └── LandingPageIllustrations
│       ├── undraw_fitness_tracker_3033.svg
│       ├── undraw_internet_on_the_go_re_vben.svg
│       └── undraw_personal_training_0dqn.svg
├── controllers
│   ├── AuthenticationController.dart
│   └── DeviceViewController.dart
├── firebase_options.dart
├── generated_plugin_registrant.dart
├── main.dart
├── models
│   ├── DeviceModel.dart
│   ├── UserModel.dart
│   └── UserStats.dart
├── services
│   ├── AuthenticationService.dart
│   ├── DatabaseService.dart
│   └── FirebaseImplementations
│       ├── FirebaseAuthenticationImpl.dart
│       └── FirebaseDatabaseImpl.dart
├── utilities
│   ├── Theme.dart
│   ├── formatters.dart
│   ├── helpers.dart
│   └── size_util.dart
└── views
    ├── Components
    │   ├── BottomSheetDesignLanguage.dart
    │   ├── ButtonDesignLanguage.dart
    │   ├── DeviceStatisticalView.dart
    │   ├── PageHeader.dart
    │   ├── device_details_view.dart
    │   └── information_box.dart
    ├── DeviceConfigurationFlow
    │   └── FlowStart.dart
    ├── HomePage.dart
    ├── HomePageSubViews
    │   ├── Dashboard.dart
    │   ├── Devices.dart
    │   └── Profile.dart
    ├── LandingPage.dart
    ├── ProfileUpdatation
    │   ├── ShowUserProfile.dart
    │   └── add_device.dart
    └── deviceConfigurationPage.dart

```

The project structure is created according to GetX & MVC requirements, all the views, components are located in <strong>views</strong> folder, while the controllers are present in <strong>controllers</strong>, the theme of project is defined globally for both dark and light mode.

### Realtiem Database Device Object
```
device_id: {
  upload: int (default=20000),
  status: str (values [start, stop]),
}
```