---
title: ユーザー設定ストアへの書き込み | Microsoft Docs
description: このチュートリアルを使用して、ユーザー設定ストアの読み取りと書き込みによって Visual Studio にメモ帳を外部ツールとして追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 05/23/2019
ms.topic: how-to
ms.assetid: efd27f00-7fe5-45f8-9b97-371af732be97
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8ff3fa6f061f894abce17d2e6c58bfb791740a90
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061772"
---
# <a name="writing-to-the-user-settings-store"></a>ユーザー設定ストアへの書き込み
ユーザー設定は、 **[ツール] > [オプション]** ダイアログ、[プロパティ] ウィンドウ、その他特定のダイアログ ボックスのように書き込み可能な設定です。 Visual Studio 拡張機能では、これらを使用して少量のデータを保存できます。 このチュートリアルでは、ユーザー設定ストアの読み取りと書き込みによって Visual Studio にメモ帳を外部ツールとして追加する方法について説明します。

## <a name="writing-to-the-user-settings-store"></a>ユーザー設定ストアへの書き込み

1. UserSettingsStoreExtension という名前の VSIX プロジェクトを作成してから、UserSettingsStoreCommand という名前のカスタム コマンドを追加します。 カスタム コマンドを作成する方法の詳細については、「[メニュー コマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

2. UserSettingsStoreCommand.cs で、次の using ディレクティブを追加します。

    ```csharp
    using System.Collections.Generic;
    using Microsoft.VisualStudio.Settings;
    using Microsoft.VisualStudio.Shell.Settings;
    ```

3. MenuItemCallback で、メソッドの本文を削除し、次のようにユーザー設定ストアを取得します。

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        WritableSettingsStore userSettingsStore = settingsManager.GetWritableSettingsStore(SettingsScope.UserSettings);
    }
    ```

4. メモ帳が外部ツールとして既に設定されているかどうかを確認します。 次のように、すべての外部ツールを反復処理して、ToolCmd の設定が "Notepad" であるかどうかを確認する必要があります。

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        WritableSettingsStore userSettingsStore = settingsManager.GetWritableSettingsStore(SettingsScope.UserSettings);

        // Find out whether Notepad is already an External Tool.
        int toolCount = userSettingsStore.GetInt32("External Tools", "ToolNumKeys");
        bool hasNotepad = false;
        CompareInfo Compare = CultureInfo.InvariantCulture.CompareInfo;
        for (int i = 0; i < toolCount; i++)
        {
            if (Compare.IndexOf(userSettingsStore.GetString("External Tools", "ToolCmd" + i), "Notepad", CompareOptions.IgnoreCase) >= 0)
            {
                hasNotepad = true;
                break;
            }
        }
    }

    ```

5. メモ帳が外部ツールとして設定されていない場合は、次のように設定します。

    ```vb
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        WritableSettingsStore userSettingsStore = settingsManager.GetWritableSettingsStore(SettingsScope.UserSettings);

        // Find out whether Notepad is already installed.
        int toolCount = userSettingsStore.GetInt32("External Tools", "ToolNumKeys");
        bool hasNotepad = false;
        CompareInfo Compare = CultureInfo.InvariantCulture.CompareInfo;
        for (int i = 0; i < toolCount; i++)
        {
            if (Compare.IndexOf(userSettingsStore.GetString("External Tools", "ToolCmd" + i), "Notepad", CompareOptions.IgnoreCase) >= 0)
            {
                hasNotepad = true;
                break;
            }
        }

        string message = (hasNotepad) ? "Notepad already installed" : "Installing Notepad";
         if (!hasNotepad)
        {
            userSettingsStore.SetString("External Tools", "ToolTitle" + toolCount, "&Notepad");
            userSettingsStore.SetString("External Tools", "ToolCmd" + toolCount, "C:\\Windows\\notepad.exe");
            userSettingsStore.SetString("External Tools", "ToolArg" + toolCount, "");
            userSettingsStore.SetString("External Tools", "ToolDir" + toolCount, "$(ProjectDir)");
            userSettingsStore.SetString("External Tools", "ToolSourceKey" + toolCount, "");
            userSettingsStore.SetUInt32("External Tools", "ToolOpt" + toolCount, 0x00000011);

            userSettingsStore.SetInt32("External Tools", "ToolNumKeys", toolCount + 1);
        }
    }
    ```

6. コードをテストします。 メモ帳が外部ツールとして追加されるので、2 回目に実行する前にレジストリをロールバックする必要があることにご注意ください。

7. コードをビルドし、デバッグを開始します。

8. **[ツール]** メニューの **[UserSettingsStoreCommand の呼び出し]** をクリックします。 これで、 **[ツール]** メニューにメモ帳が追加されます。

9. [ツール] > [オプション] メニューに [メモ帳] が表示され、 **[メモ帳]** をクリックするとメモ帳のインスタンスが表示されます。
