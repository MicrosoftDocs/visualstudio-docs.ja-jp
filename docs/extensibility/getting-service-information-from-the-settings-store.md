---
title: 設定ストアからのサービス情報の取得 | Microsoft Docs
description: 設定ストアを使用して、使用可能なすべてのサービスを検索する方法、または特定のサービスがインストールされているかどうかを確認する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 7028d440-d16d-4b08-9b94-eb8cc93b25fc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cb014803945ea88cd6c2c27eee8c120059014a18
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900643"
---
# <a name="get-service-information-from-the-settings-store"></a>設定ストアからのサービス情報の取得
設定ストアを使用して、使用可能なすべてのサービスを検索する方法、または特定のサービスがインストールされているかどうかを確認できます。 サービス クラスの型を把握している必要があります。

## <a name="to-list-the-available-services"></a>使用できるサービスを一覧表示する方法

1. `FindServicesExtension` という名前の VSIX プロジェクトを作成し、`FindServicesCommand` という名前のカスタム コマンドを追加します。 カスタム コマンドを作成する方法の詳細については、「[メニュー コマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

2. *FindServicesCommand.cs* で、次の using ディレクティブを追加します。

    ```csharp
    using System.Collections.Generic;
    using Microsoft.VisualStudio.Settings;
    using Microsoft.VisualStudio.Shell.Settings;
    using System.Windows.Forms;
    ```

3. 構成設定ストアを取得し、Services という名前のサブコレクションを見つけます。 このコレクションには、利用可能なすべてのサービスが含まれます。 `MenuItemCommand` メソッドで、既存のコードを削除し、次に置き換えます。

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
        string message = "Available services:\n";
        IEnumerable<string> collection = configurationSettingsStore.GetSubCollectionNames("Services");
        int n = 0;
        foreach (string service in collection)
        {
            message += configurationSettingsStore.GetString("Services\\" + service, "Name", "Unknown") + "\n";
        }

        MessageBox.Show(message);
    }
    ```

4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

5. 実験用インスタンスで、 **[ツール]** メニューの **[FindServicesCommand の呼び出し]** をクリックします。

     すべてのサービスを一覧表示するメッセージ ボックスが表示されます。

     これらの設定を確認するには、レジストリ エディターを使用します。

## <a name="find-a-specific-service"></a>特定のサービスを検索する
 また、<xref:Microsoft.VisualStudio.Settings.SettingsStore.CollectionExists%2A> メソッドを使用して、特定のサービスがインストールされているかどうかを確認することもできます。 サービス クラスの型を把握している必要があります。

1. 前の手順で作成したプロジェクトの MenuItemCallback の構成設定ストアで、サービスの GUID によって指定されたサブコレクションが含まれている `Services` コレクションを検索します。 この例では、ヘルプ サービスを検索します。

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
        string helpServiceGUID = typeof(SVsHelpService).GUID.ToString("B").ToUpper();
        bool hasHelpService = configurationSettingsStore.CollectionExists("Services\\" + helpServiceGUID);
        string message = "Help Service Available: " + hasHelpService;

        MessageBox.Show(message);
    }
    ```

2. プロジェクトをビルドし、デバッグを開始します。

3. 実験用インスタンスで、 **[ツール]** メニューの **[FindServicesCommand の呼び出し]** をクリックします。

     「**ヘルプ サービスが使用可能:** 」、その後に **True** または **False** が続くメッセージが表示されます。 この設定を確認するには、前の手順で示したように、レジストリ エディターを使用します。
