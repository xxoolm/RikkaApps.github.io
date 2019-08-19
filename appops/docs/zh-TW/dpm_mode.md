# 託管裝置管理員模式

## 背景

託管裝置管理員模式是 App Ops 從 v2.9.0 開始加入的新的工作模式。從 Android 9 開始，裝置管理員開始可以修改 appops 設定，但系統限制一臺裝置上僅能設定一個程式為裝置管理員。因此 App Ops 使用由其他裝置管理員程式提供的 API。

從 v2.9.0 起支援使用 [Delegated Scopes Manager](https://github.com/heruoxin/Delegated-Scopes-Manager) 的裝置管理員程式。

從 v2.9.8 起支援另一種[由 Island 提供的 API](https://island.oasisfeng.com/api)。

## 免責聲明

* 你需要安裝的裝置管理員程式都不是由我們開發。
* 裝置管理員在 Samsung 裝置及很多來自中國大陸地區廠商的裝置上或多或少存在一些問題，請務必仔細閱讀來自裝置管理員程式提供的幫助，如果你無法接受可能的問題，請不要使用。
* Samsung 裝置在使用裝置管理員後可能造成無法挽回的結果（參閱 [來自 冰箱 IceBox 的文件](https://iceboxdoc.catchingnow.com/Device%20Owner%20%E4%B8%89%E6%98%9F%E7%89%B9%E5%88%AB%E8%AF%B4%E6%98%8E)），請務必謹慎。

## 如何使用

設定過程需要連線電腦使用 adb，但只需要進行一次設定。

### 1. 安裝及設定裝置管理員程式

#### 冰箱 IceBox
  
1. 下載 [Google Play](https://play.google.com/store/apps/details?id=com.catchingnow.icebox) 或 [Coolapk](https://www.coolapk.com/apk/com.catchingnow.icebox)
2. 參閱 [幫助](https://iceboxdoc.catchingnow.com/Device%20Owner%20%EF%BC%88%E5%85%8D%20root%EF%BC%89%E6%A8%A1%E5%BC%8F%E8%AE%BE%E7%BD%AE) 為其設定裝置管理員模式

#### 小黑屋
  
1. 下載 [Google Play](https://play.google.com/store/apps/details?id=web1n.stopapp) 或 [Coolapk](https://www.coolapk.com/apk/web1n.stopapp)
2. 參閱 [幫助](https://github.com/web1n/Stopapp-Docs/blob/master/Device%20Owner%20%EF%BC%88%E5%85%8D%20root%EF%BC%89%E6%A8%A1%E5%BC%8F%E8%AE%BE%E7%BD%AE.md)（僅提供簡體中文） 為其設定裝置管理員模式

#### Island

1. 下載 [Google Play](https://play.google.com/store/apps/details?id=https://island.oasisfeng.com/setup) 或 [Coolapk](https://www.coolapk.com/apk/https://island.oasisfeng.com/setup)
2. 參閱 [幫助](https://island.oasisfeng.com/setup) 為其設定裝置管理員模式（Island 稱其為「上帝模式」）

### 2. 授予權限

在 App Ops「設定」-「工作模式」中選擇「託管裝置管理員模式」後返回程式列表應該會彈出來自裝置管理員程式的授權對話方塊，請在勾選「修改 app ops」後確認。

接著，你還需要使用使用 adb 授予 App Ops 「獲取 app ops」 權限。使用以下的指令：

```
adb shell pm grant --user 0 rikka.appops android.permission.GET_APP_OPS_STATS
```

注意，如果你將 App Ops 程式安裝到其他使用者，需要將其中 `--user 0` 的 `0` 替換為其他使用者的 id（使用 `adb shell pm list users` 獲得的 `UserInfo{0:Owner:13} running` 的結果中的 `0` 即為使用者 id）。