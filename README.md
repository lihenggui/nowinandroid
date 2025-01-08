![Now in Android](docs/images/nia-splash.jpg "Now in Android")

<a href="https://play.google.com/store/apps/details?id=com.google.samples.apps.nowinandroid"><img src="https://play.google.com/intl/en_us/badges/static/images/badges/en_badge_web_generic.png" height="70"></a>

Now in Android App - Kotlin Multiplatform Edition
==================
Welcome to the Kotlin Multiplatform edition of Now in Android, a community-driven initiative to bring the best of Android development content to developers across platforms. This repository is a branch of the original Now in Android project, reimagined and re-engineered using Kotlin Multiplatform technology to make the project truly cross-platform.

**Learn how this app was designed and built in the [design case study](https://goo.gle/nia-figma), [architecture learning journey](docs/ArchitectureLearningJourney.md) and [modularization learning journey](docs/ModularizationLearningJourney.md).**

This is the repository for the [Now in Android](https://developer.android.com/series/now-in-android)
app.

**Now in Android** is a fully functional Android app built entirely with Kotlin and Jetpack Compose. It
follows Android design and development best practices and is intended to be a useful reference
for developers. As a running app, it's intended to help developers keep up-to-date with the world
of Android development by providing regular news updates.

The app is currently in development. The `prodRelease` variant is [available on the Play Store](https://play.google.com/store/apps/details?id=com.google.samples.apps.nowinandroid).

# Project Status

This project is a **work in progress** 🚧. Please note that the CI may not function normally at this time.

# Changes to Convention Plugins

Numerous changes have been made on top of the original Now in Android app. We've replaced several third-party libraries with ones that support Kotlin Multiplatform. Here are some conventions I've documented:

- [KmpLibraryConventionPlugin](build-logic/convention/src/main/kotlin/KmpLibraryConventionPlugin.kt): Convention for Kotlin Multiplatform Libraries
- [KotlinInjectConventionPlugin](build-logic/convention/src/main/kotlin/KotlinInjectConventionPlugin.kt): Convention for using [kotlin-inject](https://github.com/evant/kotlin-inject) as a replacement for [Hilt](https://dagger.dev/hilt/)
- [SqlDelightConventionPlugin](build-logic/convention/src/main/kotlin/SqlDelightConventionPlugin.kt): Convention for using [SQLDelight](https://github.com/cashapp/sqldelight) for storing local data, replacing [Android Room](https://developer.android.com/jetpack/androidx/releases/room).

## Changes to Modules

To transform the main app into a Compose Multiplatform app capable of running on multiple platforms, all modules need to be converted to Kotlin Multiplatform libraries. The project structure of these modules should be adjusted to align with [Kotlin Multiplatform source sets](https://kotlinlang.org/docs/multiplatform-discover-project.html#source-sets). 

As Firebase Analytics does not yet support Kotlin Multiplatform, the implementation in `:core:analytics` has been removed, leaving an empty implementation in its place.


## Status for modules

| Module                    | Progress    | Desktop supported | Android supported | iOS supported | Web supported |
|---------------------------|-------------|-------------------|-------------------|---------------|---------------|
| app                       | In progress | ✅                | ✅                | ✅            | ❌            |
| app-nia-catalog           | Done        | ✅                | ✅                | ✅            | ✅            |
| :core:analytics           | Done        | ✅                 | ✅️                 | ✅             | ❌            |
| :core:common              | Done        | ✅                 | ✅                 | ✅             | ❌            |
| :core:data                | Done        | ✅                 | ✅️                 | ✅             | ❌            |
| :core:data-test           | Done        | ✅                | ✅️                | ✅            | ❌            |
| :core:database            | Done        | ✅                 | ✅️                 | ✅             | ❌            |
| :core:datastore           | Done        | ✅                 | ✅️                 | ✅             | ❌            |
| :core:datastore-proto     | Done        | ✅                 | ✅️                 | ✅             | ❌            |
| :core:datastore-test      | Removed     | ❌                | ❌                | ❌            | ❌            |
| :core:designsystem        | Done        | ✅                | ✅                | ✅            | ✅            |
| :core:domain              | Done        | ✅                 | ✅️                 | ✅             | ❌            |
| :core:model               | Done        | ✅                 | ✅️                 | ✅             | ❌            |
| :core:network             | Done        | ✅                 | ✅️                 | ✅             | ❌            |
| :core:notification        | Done        | No implmentaion   | ✅️                 |No implmentaion| ❌           |
| :core:screenshot-testing  | Not started | ❌                | ❌                | ❌            | ❌            |
| :core:testing             | Done        | ✅                 | ✅️                 | ✅             | ❌            |
| :core:ui                  | Done        | ✅                 | ✅️                 | ✅             | ❌            |
| :feature:bookmarks        | Done        | ✅                | ✅️                | ✅            | ❌            |
| :feature:foryou           | Done        | ✅                | ✅️                | ✅            | ❌            |
| :feature:interests        | Done        | ✅                | ✅️                | ✅            | ❌            |
| :feature:search           | Done        | ✅                | ✅️                | ✅            | ❌            |
| :feature:settings         | Done        | ✅                | ✅️                | ✅            | ❌            |
| :feature:topic            | Done        | ✅                | ✅️                | ✅            | ❌            |
| lint                      | Not started | ❌                | ❌                | ❌            | ❌            |
| :sync:sync-test           | Done        | ✅                | ✅                | ✅            | ❌            |
| :sync:work                | Not started | No implmentaion   | ✅️                | No implmentaion| ❌            |
| ui-test-manifest          | Removed     | ❌                | ❌                | ❌            | ❌            |



✅: Functioning properly  
❔: Not yet tested, but expected to work  
✔️: Successfully compiled  
❌: Not functioning, requires further attention  
🚧: Work in progress  

# Running the Project

This project currently supports running the `app-nia-catalog` module in Compose Multiplatform. The `app` module is still working in progress.

## Running on Android

1. Create an Android Virtual Device (AVD).
2. Select `app-nia-catalog` from the list of run configurations.
3. Choose your AVD and click "Run".

## Running on Desktop

To run the desktop application, follow these steps:

1. Navigate to `Run | Edit Configurations`.
2. Click the plus button and select "Gradle" from the dropdown menu.
3. In the "Tasks and arguments" field, paste the following command: 
   ```
   desktopRun -DmainClass=MainKt --quiet
   ```
4. Choose the Gradle project: `nowinandroid:app-nia-catalog`.
5. Click "OK" to save the configuration.

## Running on iOS

For instructions on running the application on iOS, please refer to [this guide](https://www.jetbrains.com/help/kotlin-multiplatform-dev/compose-multiplatform-create-first-app.html#run-your-application-on-ios).


# Features

**Now in Android** displays content from the
[Now in Android](https://developer.android.com/series/now-in-android) series. Users can browse for
links to recent videos, articles and other content. Users can also follow topics they are interested
in, and be notified when new content is published which matches interests they are following.

## Screenshots

![Screenshot showing For You screen, Interests screen and Topic detail screen](docs/images/screenshots.png "Screenshot showing For You screen, Interests screen and Topic detail screen")

# Development Environment

**Now in Android** uses the Gradle build system and can be imported directly into Android Studio (make sure you are using the latest stable version available [here](https://developer.android.com/studio)). 

Change the run configuration to `app`.

![image](https://user-images.githubusercontent.com/873212/210559920-ef4a40c5-c8e0-478b-bb00-4879a8cf184a.png)

The `demoDebug` and `demoRelease` build variants can be built and run (the `prod` variants use a backend server which is not currently publicly available).

![image](https://user-images.githubusercontent.com/873212/210560507-44045dc5-b6d5-41ca-9746-f0f7acf22f8e.png)

Once you're up and running, you can refer to the learning journeys below to get a better
understanding of which libraries and tools are being used, the reasoning behind the approaches to
UI, testing, architecture and more, and how all of these different pieces of the project fit
together to create a complete app.

# Architecture

The **Now in Android** app follows the
[official architecture guidance](https://developer.android.com/topic/architecture) 
and is described in detail in the
[architecture learning journey](docs/ArchitectureLearningJourney.md).

# Modularization

The **Now in Android** app has been fully modularized and you can find the detailed guidance and
description of the modularization strategy used in
[modularization learning journey](docs/ModularizationLearningJourney.md).

# Build

The app contains the usual `debug` and `release` build variants. 

In addition, the `benchmark` variant of `app` is used to test startup performance and generate a
baseline profile (see below for more information).

`app-nia-catalog` is a standalone app that displays the list of components that are stylized for
**Now in Android**.

The app also uses
[product flavors](https://developer.android.com/studio/build/build-variants#product-flavors) to
control where content for the app should be loaded from.

The `demo` flavor uses static local data to allow immediate building and exploring of the UI.

The `prod` flavor makes real network calls to a backend server, providing up-to-date content. At 
this time, there is not a public backend available.

For normal development use the `demoDebug` variant. For UI performance testing use the
`demoRelease` variant. 

# Testing

To facilitate testing of components, **Now in Android** uses dependency injection with
[Hilt](https://developer.android.com/training/dependency-injection/hilt-android).

Most data layer components are defined as interfaces.
Then, concrete implementations (with various dependencies) are bound to provide those interfaces to
other components in the app.
In tests, **Now in Android** notably does _not_ use any mocking libraries.
Instead, the production implementations can be replaced with test doubles using Hilt's testing APIs
(or via manual constructor injection for `ViewModel` tests).

These test doubles implement the same interface as the production implementations and generally
provide a simplified (but still realistic) implementation with additional testing hooks.
This results in less brittle tests that may exercise more production code, instead of just verifying
specific calls against mocks.

Examples:
- In instrumentation tests, a temporary folder is used to store the user's preferences, which is
  wiped after each test.
  This allows using the real `DataStore` and exercising all related code, instead of mocking the 
  flow of data updates.

- There are `Test` implementations of each repository, which implement the normal, full repository
  interface and also provide test-only hooks.
  `ViewModel` tests use these `Test` repositories, and thus can use the test-only hooks to
  manipulate the state of the `Test` repository and verify the resulting behavior, instead of
  checking that specific repository methods were called.

To run the tests execute the following gradle tasks: 

- `testDemoDebug` run all local tests against the `demoDebug` variant. Screenshot tests will fail
(see below for explanation). To avoid this, run `recordRoborazziDemoDebug` prior to running unit tests.
- `connectedDemoDebugAndroidTest` run all instrumented tests against the `demoDebug` variant. 

> [!NOTE]
> You should not run `./gradlew test` or `./gradlew connectedAndroidTest` as this will execute 
tests against _all_ build variants which is both unnecessary and will result in failures as only the
`demoDebug` variant is supported. No other variants have any tests (although this might change in future). 

## Screenshot tests
A screenshot test takes a screenshot of a screen or a UI component within the app, and compares it 
with a previously recorded screenshot which is known to be rendered correctly. 

For example, Now in Android has [screenshot tests](https://github.com/android/nowinandroid/blob/main/app/src/testDemo/kotlin/com/google/samples/apps/nowinandroid/ui/NiaAppScreenSizesScreenshotTests.kt)
to verify that the navigation is displayed correctly on different screen sizes 
([known correct screenshots](https://github.com/android/nowinandroid/tree/main/app/src/testDemo/screenshots)). 

Now In Android uses [Roborazzi](https://github.com/takahirom/roborazzi) to run screenshot tests
of certain screens and UI components. When working with screenshot tests the following gradle tasks are useful:

- `verifyRoborazziDemoDebug` run all screenshot tests, verifying the screenshots against the known
correct screenshots.
- `recordRoborazziDemoDebug` record new "known correct" screenshots. Use this command when you have
made changes to the UI and manually verified that they are rendered correctly. Screenshots will be
stored in `modulename/src/test/screenshots`.
- `compareRoborazziDemoDebug` create comparison images between failed tests and the known correct
images. These can also be found in `modulename/src/test/screenshots`. 

> [!NOTE]
> **Note on failing screenshot tests**   
> The known correct screenshots stored in this repository are recorded on CI using Linux. Other
platforms may (and probably will) generate slightly different images, making the screenshot tests fail. 
When working on a non-Linux platform, a workaround to this is to run `recordRoborazziDemoDebug` on the
`main` branch before starting work. After making changes, `verifyRoborazziDemoDebug` will identify only
legitimate changes. 

For more information about screenshot testing 
[check out this talk](https://www.droidcon.com/2023/11/15/easy-screenshot-testing-with-compose/).

# UI
The app was designed using [Material 3 guidelines](https://m3.material.io/). Learn more about the design process and 
obtain the design files in the [Now in Android Material 3 Case Study](https://goo.gle/nia-figma) (design assets [also available as a PDF](docs/Now-In-Android-Design-File.pdf)).

The Screens and UI elements are built entirely using [Jetpack Compose](https://developer.android.com/jetpack/compose). 

The app has two themes: 

- Dynamic color - uses colors based on the [user's current color theme](https://material.io/blog/announcing-material-you) (if supported)
- Default theme - uses predefined colors when dynamic color is not supported

Each theme also supports dark mode. 

The app uses adaptive layouts to
[support different screen sizes](https://developer.android.com/guide/topics/large-screens/support-different-screen-sizes).

Find out more about the [UI architecture here](docs/ArchitectureLearningJourney.md#ui-layer).

# Performance

## Benchmarks

Find all tests written using [`Macrobenchmark`](https://developer.android.com/topic/performance/benchmarking/macrobenchmark-overview)
in the `benchmarks` module. This module also contains the test to generate the Baseline profile.

## Baseline profiles

The baseline profile for this app is located at [`app/src/main/baseline-prof.txt`](app/src/main/baseline-prof.txt).
It contains rules that enable AOT compilation of the critical user path taken during app launch.
For more information on baseline profiles, read [this document](https://developer.android.com/studio/profile/baselineprofiles).

> [!NOTE]
> The baseline profile needs to be re-generated for release builds that touch code which changes app startup.

To generate the baseline profile, select the `benchmark` build variant and run the
`BaselineProfileGenerator` benchmark test on an AOSP Android Emulator.
Then copy the resulting baseline profile from the emulator to [`app/src/main/baseline-prof.txt`](app/src/main/baseline-prof.txt).

## Compose compiler metrics

Run the following command to get and analyse compose compiler metrics:

```bash
./gradlew assembleRelease -PenableComposeCompilerMetrics=true -PenableComposeCompilerReports=true
```

The reports files will be added to [build/compose-reports](build/compose-reports). The metrics files will also be 
added to [build/compose-metrics](build/compose-metrics).

For more information on Compose compiler metrics, see [this blog post](https://medium.com/androiddevelopers/jetpack-compose-stability-explained-79c10db270c8).

# License

**Now in Android** is distributed under the terms of the Apache License (Version 2.0). See the
[license](LICENSE) for more information.
