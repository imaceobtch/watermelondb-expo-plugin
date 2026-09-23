# watermelon-db-plugin 🍉
Config plugin to auto configure `@nozbe/watermelondb`

> **This is a fork of [`@morrowdigital/watermelondb-expo-plugin`](https://github.com/morrowdigital/watermelondb-expo-plugin).**
> Upstream's `main` branch (2.4.0) already removes the `JSIModulePackage` registration that
> React Native's New-Architecture-only builds no longer expose, but that fix has never been cut
> as a stable npm release (npm's `latest` tag is still stuck on 2.3.3, which fails to compile
> against current RN). This fork exists solely to publish that already-written fix as a real,
> stable release. No behavior changes beyond what upstream's own `main` already contains.

## Install

> Tested against Expo SDK 54–57, RN 0.86.x (New Architecture)

```
npm install @imaceobtch/watermelondb-expo-plugin

```

After installing this npm package, add the [config plugin](https://docs.expo.io/guides/config-plugins/) to the [`plugins`](https://docs.expo.io/versions/latest/config/app/#plugins) array of your `app.json` or `app.config.js`. Then rebuild your app using a custom development client, as described in the ["Adding custom native code"](https://docs.expo.io/workflow/customizing/) guide.

## Example

In your app.json `plugins` array:

```json
{
  "plugins": [
        "@imaceobtch/watermelondb-expo-plugin"
  ]
}
```

## JSI support for Android

This plugin installs automatically JSI support for Android builds, as per [WatermelonDB for Android instructions](https://watermelondb.dev/docs/Installation#android-react-native).
If you wish to disable JSI support during build you may add the option in config plugin:
```json
  [
    "@imaceobtch/watermelondb-expo-plugin",
    { "disableJsi": true }
  ]
```

## Build errors with M1 architectures for simulators

There have been errors building with M1 architectures for simulators on iOS, with Error:
```
No such module 'ExpoModulesCore' 
```
See these discussions:
* [https://github.com/morrowdigital/watermelondb-expo-plugin/issues/20](https://github.com/morrowdigital/watermelondb-expo-plugin/issues/20)
* [https://github.com/morrowdigital/watermelondb-expo-plugin/issues/34](https://github.com/morrowdigital/watermelondb-expo-plugin/issues/34)
* [https://github.com/facebook/react-native/issues/32704#issuecomment-1174458011](https://github.com/facebook/react-native/issues/32704#issuecomment-1174458011)

This plugin will NOT add the `arm64` in  `Exlcuded_Archs`, in SDK 50+ builds:
```
'"EXCLUDED_ARCHS[sdk=iphonesimulator*]"'] = '"arm64"'
```

If you wish to add the above in configuration, you can add it with option:
```json
  [
    "@imaceobtch/watermelondb-expo-plugin",
    { "excludeSimArch": true }
  ]
```
