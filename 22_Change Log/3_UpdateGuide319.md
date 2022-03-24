# Migrating to 3.19.0

Wiser SDK has supported AndroidX since 3.19.0.

Google's supprot library will no longer be updated after 28.0.0. It is recommended that developers upgrade to AndroidX.

## Migrating to Android X

AndroidX replaces the original support library APIs with packages in the `androidx` namespace. Only the package and Maven artifact names changed; class, method, and field names did not change.

**Note:** We recommend working in a separate branch when migrating. Also try to avoid refactoring your code while performing the migration.

## Prerequisites

Before you migrate, bring your app up to date. We recommend updating your project to use the final version of the support library: [version 28.0.0](https://developer.android.google.cn/topic/libraries/support-library/revisions#28-0-0). This is because AndroidX artifacts with version 1.0.0 are binary equivalent to the Support Library 28.0.0 artifacts.

## Migrate an existing project using Android Studio

With Android Studio 3.2 and higher, you can migrate an existing project to AndroidX by selecting **Refactor > Migrate to AndroidX** from the menu bar.

The refactor command makes use of two flags. By default, both of them are set to `true` in your [`gradle.properties`](https://developer.android.google.cn/studio/build#properties-files) file:

- `android.useAndroidX=true`

  The Android plugin uses the appropriate AndroidX library instead of a Support Library.

- `android.enableJetifier=true`

  The Android plugin automatically migrates existing third-party libraries to use AndroidX by rewriting their binaries.

**Note:** The built-in Android Studio migration might not handle everything. Depending on your build configuration you may need to update your build scripts and Proguard mappings manually. For example, if you maintain your dependency configuration in a separate build file, use the mapping files mentioned below to review and update your dependencies to the corresponding AndroidX packages.

## Mappings

If you run into issues with migration, refer to these tables to determine the proper mappings from the support library to the corresponding AndroidX artifacts and classes:

- [Maven artifact mappings](https://developer.android.google.cn/jetpack/androidx/migrate/artifact-mappings)
- [Class mappings](https://developer.android.google.cn/jetpack/androidx/migrate/class-mappings)

For the latest versions of the Jetpack libraries, see the [versions page](https://developer.android.google.cn/jetpack/androidx/versions).

## Additional resources

To learn more about migrating your code to AndroidX, see the following additional resources:

### Blog posts

- [Cross-stitching Plaid and AndroidX](https://medium.com/androiddevelopers/cross-stitching-plaid-and-androidx-7603a192348e)
- [Migrating to AndroidX: Tip, Tricks, and Guidance](https://medium.com/androiddevelopers/migrating-to-androidx-tip-tricks-and-guidance-88d5de238876)

### Videos

- [Migrating to AndroidX: the time is right](https://www.youtube.com/watch?v=Hyt7LR5mXLc)

## Reference

[https://developer.android.google.cn/jetpack/androidx/migrate?hl=en](https://developer.android.google.cn/jetpack/androidx/migrate?hl=en)