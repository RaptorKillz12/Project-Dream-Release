# Project Dream
Project Dream converts the macOS version of Dream Team into a game that runs on Windows and Android.

## Using Project Dream Installer

1. Get the macOS version of Sonic Dream Team (`SonicDreamTeam.app`) only tested on 1.10.1 version.
2. Run `Project Dream.exe`.
3. Browse to `SonicDreamTeam.app` and select `Contents` folder.
4. Select your platform either Windows or Android.
5. Click **Install** and wait for it to finish building.

**Android:** the APK and OBB are saved in `Project Dream Android` besides `ProjectDream.exe`.
1. Install `SonicDreamTeam.apk` on your device.
2. Create the `com.sonicdreamteam.android` folder inside `Android\obb\com.sonicdreamteam.android`
3. Copy `main.1.com.sonicdreamteam.android.obb` to `Android/obb/com.sonicdreamteam.android/` on the device.
The first Android build downloads the Android SDK, NDK, JDK and Unity Android player into an `AndroidTools` make sure you have atleast 3GB of free space.

## Known Issues
After running the game on Windows if there's no extra Game Options or Graphics options try running it as administrator for Melon Loader to work.
If it fails to build check Windows Defender or any 3rd party Anti virus you use because its a false positive.

## Mod support
Melon Loader is installed on Windows and works just the same as modding any other IL2CPP Unity Windows game so you can make anything.
A Dummy dump of the IL2CPP C# Mono dlls is provided inside the Melon Loader folder to get you started.
You can use DNSPY or ILSPY to check function names or script names to create Prefix or Postfix Melon Loader patches.
You can look up Melon Loader tutorials for how to create dll C# patches.

## How it works
The Mac version is built with Unity's IL2CPP backend. This means all of its game code is in a single library, `GameAssembly.dylib`.
Project Dream runs the original Mac game code natively without recompiling it. On Windows it uses the x86-64 copy:

- **Loader:** a replacement `GameAssembly.dll` loads the macOS `GameAssembly.dylib` into memory, the same way macOS would.
- **macOS functions:** every macOS system function the game calls, such as files, threads, Objective-C, Foundation and C++ exceptions, is handled by a Windows implementation.
- **Unity player:** the game code is presented to Unity's standard Windows player, which runs it like any other Windows Unity game.
- **Shaders:** the game's Metal shaders are converted to DirectX 11 and Vulkan for Windows, and OpenGL ES and Vulkan for Android.
- **Game patches:** MelonLoader loads GamePatches, which adds the Windows graphics, display and gameplay options to the game's menus.
