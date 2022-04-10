# Expo project to show how to use Notifee with Expo

## What was done to create this:

- initiate a blank expo typescript project `npx expo-cli init`
- install Notifee `expo install @notifee/react-native`
- copy the plugin from my PR: `svn export https://github.com/abumalick/notifee/trunk/packages/react-native/plugin`
- install `expo-module-scripts`: `yarn add -D expo-module-scripts`
- modify plugin tsconfig.json extend to `"extends": "expo-module-scripts/tsconfig.plugin",` (It does not generate files here when extending default expo tsconfig file)
- build plugin `yr tsc -p plugin/tsconfig.json` (I get 224 errors but it compiles)
- install expo dev client `expo install expo-dev-client`
- add plugin to configuration: `"plugins": ["./plugin/build"]`
- `yarn expo prebuild`
- Check build.gradle, the compileSdkVersion should be 31 `cat android/build.gradle | grep compileSdkVersion`
- `yarn expo run:android` (Didn't test that, I don't have JDK 11 setup properly on my computer)

## Steps to start building on EAS

- add `postinstall` strict in package.json: `"postinstall": "tsc -p plugin/tsconfig.json"`
- eas init
- `eas build -p android`
- add android.image to `eas.json` profiles `"image": "ubuntu-18.04-jdk-11-ndk-r19c"`
- `eas build -p android`

## Add Notifee example code

```bash
rm App.tsx
svn export https://github.com/abumalick/notifee/trunk/packages/react-native/example/App.tsx
svn export https://github.com/abumalick/notifee/trunk/packages/react-native/example/src
```

## Notes

Install svn in macOS

https://stackoverflow.com/a/64566557/1673761
https://stackoverflow.com/a/70659881/1673761
