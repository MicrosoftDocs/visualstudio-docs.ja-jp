---
title: 設定ストアの使用 | Microsoft Docs
description: 読み取り専用の Visual Studio と VSPackage の設定である構成設定ストアからデータを読み取る方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Settings Store, using
ms.assetid: 447ec08a-eca5-40b8-89b0-f98fdf3d39a4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0a84fa551a4a3ea10b212832c0891fb0d7d19b2f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060186"
---
# <a name="using-the-settings-store"></a>設定ストアの使用
設定ストアには次の 2 種類があります。

- 構成設定は、読み取り専用の Visual Studio と VSPackage の設定です。 Visual Studio では、すべての既知の .pkgdef ファイルの設定がこのストアにマージされます。

- ユーザー設定は、 **[オプション]** ダイアログ ボックス、プロパティ ページ、その他の特定のダイアログ ボックスのページに表示されるものなど、書き込み可能な設定です。 Visual Studio 拡張機能では、少量のデータのローカル ストレージにこれらを使用できます。

  このチュートリアルでは、構成設定ストアからデータを読み取る方法について説明します。 ユーザー設定ストアに書き込む方法の詳細については、「[ユーザー設定ストアへの書き込み](../extensibility/writing-to-the-user-settings-store.md)」を参照してください。

## <a name="creating-the-example-project"></a>プロジェクト例の作成
 このセクションでは、デモンストレーション用のメニュー コマンドを使用して単純な拡張機能プロジェクトを作成する方法について説明します。

1. すべての Visual Studio 拡張機能は、拡張機能アセットを格納する VSIX デプロイ プロジェクトから始まります。 `SettingsStoreExtension` という名前の [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、 **[新しいプロジェクト]** の **[Visual C# / 拡張機能]** の下にあります。

2. 次に、**SettingsStoreCommand** という名前のカスタム コマンド項目テンプレートを追加します。 **[新しい項目の追加]** ダイアログで、 **[Visual C#]、[拡張機能]** の順に移動し、 **[カスタム コマンド]** を選択します。 ウィンドウの下部にある **[名前]** フィールドで、コマンド ファイル名を **SettingsStoreCommand.cs** に変更します。 カスタム コマンドを作成する方法の詳細については、「[メニュー コマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

## <a name="using-the-configuration-settings-store"></a>構成設定ストアの使用
 このセクションでは、構成設定を検出して表示する方法について説明します。

1. SettingsStorageCommand.cs ファイルで、次の using ディレクティブを追加します。

   ```
   using System.Collections.Generic;
   using Microsoft.VisualStudio.Settings;
   using Microsoft.VisualStudio.Shell.Settings;
   using System.Windows.Forms;
   ```

2. `MenuItemCallback` で、メソッドの本文を削除し、次の行を追加して、構成設定ストアを取得します。

   ```
   SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
   SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
   ```

    <xref:Microsoft.VisualStudio.Shell.Settings.ShellSettingsManager> は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsManager> サービスを介したマネージド ヘルパー クラスです。

3. 次に、Windows Phone ツールがインストールされているかどうかを確認します。 コードは、次のようになります。

   ```
   private void MenuItemCallback(object sender, EventArgs e)
   {
       SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
       SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
       bool arePhoneToolsInstalled = configurationSettingsStore.CollectionExists(@"InstalledProducts\Microsoft Windows Phone Developer Tools");
       string message = "Microsoft Windows Phone Developer Tools: " + arePhoneToolsInstalled;
       MessageBox.Show(message);
   }
   ```

4. コードをテストします。 プロジェクトをビルドし、デバッグを開始します。

5. 実験用インスタンスで、 **[ツール]** メニューの **[SettingsStoreCommand の呼び出し]** をクリックします。

    「**Microsoft Windows Phone 開発者ツール**」、その後に **True** または **False** が続くメッセージ ボックスが表示されます。

   Visual Studio では、設定ストアはシステム レジストリに保持されます。

#### <a name="to-use-a-registry-editor-to-verify-configuration-settings"></a>レジストリ エディターを使用して構成設定を確認する方法

1. Regedit.exe を開きます。

2. HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0Exp_Config\InstalledProducts\\ に移動します。

    > [!NOTE]
    > \14.0_Config\\ ではなく \14.0Exp_Config\ を含むキーを見ていることを確認します。 Visual Studio の実験用インスタンスを実行すると、構成設定はレジストリ ハイブ "14.0Exp_Config" にあります。

3. \Installed Products\ ノードを展開します。 前の手順のメッセージが「**Microsoft Windows Phone 開発者ツールがインストール済み: True**」の場合は、\Installed Products\ に Microsoft Windows Phone 開発者ツール ノードが含まれているはずです。 メッセージが「**Microsoft Windows Phone 開発者ツールがインストール済み: False**」の場合は、\Installed Products\ に Microsoft Windows Phone 開発者ツール ノードが含まれていないはずです。
