---
title: Setting up an Android emulator for pentesting
date: 2023-08-01 13:37:00
categories: [Guides,Android]
tags: [android,emulator]     # TAG names should always be lowercase
---
First and foremost, to pentest Android apps, we'll need to create the Android emulator. Lots of options are available online such as [Noxplayer](https://www.bignox.com/), [Genymotion](https://www.genymotion.com/), or my personal favorite, [Android Studio](https://developer.android.com/studio). 
1. Open up "Android Studio", hit "More Actions" and go to "Virtual Device Manager".
![Opening the VDM in Android Studio](/assets/images/Opening%20the%20VDM%20in%20Android%20Studio.png)
2. Hit "Create device", select whichever phone size you want and press "Next".
![Create emulator part 1](/assets/images/Create%20emulator%20part%201.png)
3. Now when selecting a system image, go to the "x86 Images" tab and select an x86_64 version with Google APIs (NOT Google Play). I usually go for the Android 9.0 (Pie).
	1. Note that on first emulator creation, you will need to first download the system image from below.
![Create emulator part 2](/assets/images/Create%20emulator%20part%202.png)
4. Give it an appropriate name, and hit "Show Advanced Settings". If you can spare, it is recommended to add 1-2GBs more to the RAM and definitely add a few more GBs of storage.
![Create emulator part 3](/assets/images/Create%20emulator%20part%203.png)
 5. Android Studio can now be closed, and we'll open a terminal window with administrative privileges. 
	 1. Navigate to the Android SDK installation folder (the default for windows is `C:\Users\<USERNAME>\AppData\Local\Android\Sdk`) to confirm it's existence. 
	 2. For an easier life down the road, add the emulator and platform-tools folders to the PATH environment variable.
6. You can use `emulator.exe -list-avds` to check all available emulators without opening Android Studio again.
![Listing AVDs with emulator.exe](/assets/images/Listing%20AVDs%20with%20emulator.exe.png)
7. Now let's open it up `emulator.exe -avd AVD_NAME -writable-system -qemu`
	1. Side note for `failed to open /qemu.conf, err: 2` error: you will need to create a qemu.conf file at the root base of current working drive. For this, you can use `echo # > C:\qemu.conf` inside a CMD shell, or just do it with notepad.
	2. Side note for `Unable to connect to adb daemon on port: 5037` error: close the emulator, then run any `adb` command to start it's daemon, for example: `adb.exe root`![Start ADB daemon](/assets/images/Start%20ADB%20daemon.png)
![Opening newly created emulator](/assets/images/Opening%20newly%20created%20emulator.png)
8. Last thing to do is to issue a few commands with adb to have root access on the emulator. Note that these commands might need to be re-run when restarting the AVD.
- `adb root`
- `adb remount`
- `adb shell whoami`

![Gain root access on device](/assets/images/Gain%20root%20access%20on%20device.png)