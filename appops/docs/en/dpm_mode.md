# Delegated Device Admin mode

## Background

Delegated Device Admin mode is a new working mode that App Ops has added since v2.9.0. Starting with Android 9, Device admin apps can modify appops settings, but the system limits the ability to set only one app as a Device admin on a device. Therefore, the App Ops app chooses to use APIs provided by other Device admin apps.

From v2.9.0, App Ops supports Device admin apps using [Delegated Scopes Manager](https://github.com/heruoxin/Delegated-Scopes-Manager).

From v2.9.8, App Ops supports [another API provided by Island app](https://island.oasisfeng.com/api).

## Disclaimer

* The Device admin app you need to install is not developed by us.
* Device admin have somewhat problems with Samsung devices and many devices from mainland China. Please be sure to read the help provided by the Device admin app. If you can't accept possible problems, please don't use them.
* Samsung devices may cause irreparable results after using the Device admin (see [Document from IceBox](https://iceboxdoc.catchingnow.com/Device%20Owner%20%E4%B8%89%E6%98%9F%E7%89%B9%E5%88%AB%E8%AF%B4%E6%98%8E)), **please be cautious**.

## How to use

The setup process requires a computer to be use adb, but only needs to be set once.

### 1. Install and set up the Device admin app

#### IceBox
  
1. Download from [Google Play](https://play.google.com/store/apps/details?id=com.catchingnow.icebox) or [Coolapk](https://www.coolapk.com/apk/com.catchingnow.icebox)
2. See [Help](https://iceboxdoc.catchingnow.com/Device%20Owner%20(Non%20Root)%20Setup) to set up Device admin mode for it

#### 小黑屋 (Simplified Chinese only)
  
1. Download from [Google Play](https://play.google.com/store/apps/details?id=web1n.stopapp) or [Coolapk](https://www.coolapk.com/apk/web1n.stopapp )
2. See [Help](https://github.com/web1n/Stopapp-Docs/blob/master/Device%20Owner%20%EF%BC%88%E5%85%8D%20root%EF%BC%89%E6%A8%A1%E5%BC%8F%E8%AE%BE%E7%BD%AE.md) (Simplified Chinese only) to set up Device admin mode for it

#### Island

1. Download from [Google Play](https://play.google.com/store/apps/details?id=https://island.oasisfeng.com/setup) or [Coolapk](https://www.coolapk.com/apk/https://island.oasisfeng.com/setup)
2. See [Help](https://island.oasisfeng.com/setup) to set up Device admin mode for it (Island call it "God mode")

### 2. Granting permissions

In the "Settings" - "Working Mode" of App Ops, select "Delegated Device Admin mode" and return to the app list. The authorization dialog from the Device admin app should pop up. Please check "change app ops" and confirm.

Next, you'll also need to grant App Ops the "get app ops" permission using adb. Use the following command:

```
adb shell pm grant --user 0 rikka.appops android.permission.GET_APP_OPS_STATS
```

Note that if you install the App Ops app in other users, you need to replace the `0` of `--user 0` with the id of the other user (use `adb shell pm list users` you will see results like `UserInfo{0:Owner:13} running`, `0` from it is the user id).