---
title: 設定ストアからサービス情報の取得 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 7028d440-d16d-4b08-9b94-eb8cc93b25fc
caps.latest.revision: 5
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cfe754203ae9b4e951de5beef8cd829f9d7716bb
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60116655"
---
# <a name="getting-service-information-from-the-settings-store"></a>設定ストアからのサービス情報の取得
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

設定ストアを使用するには、すべての利用可能なサービスを検索するかを特定のサービスがインストールされているかどうかを判断します。 サービス クラスの型が必要です。  
  
### <a name="to-list-the-available-services"></a>利用可能なサービスを一覧表示するには  
  
1. FindServicesExtension をという名前の VSIX プロジェクトを作成し、FindServicesCommand をという名前のカスタム コマンドを追加します。 カスタム コマンドを作成する方法の詳細については、次を参照してください[メニュー コマンドを使用して拡張機能の作成。](../extensibility/creating-an-extension-with-a-menu-command.md)  
  
2. FindServicesCommand.cs で、次のコードを追加ステートメントを使用します。  
  
    ```vb  
    using System.Collections.Generic;  
    using Microsoft.VisualStudio.Settings;  
    using Microsoft.VisualStudio.Shell.Settings;  
    using System.Windows.Forms;  
    ```  
  
3. 構成設定ストアを取得し、名前付きサービス、サブコレクションを検索します。 このコレクションには、利用可能なすべてのサービスが含まれています。 MenuItemCommand メソッドで、既存のコードを削除し、次のように置き換えます。  
  
    ```  
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
  
5. 実験用インスタンスでは、上、**ツール** メニューのをクリックして**呼び出す FindServicesCommand**します。  
  
     すべてのサービスを一覧表示するメッセージ ボックスが表示されます。  
  
     これらの設定を確認するには、レジストリ エディターを使用することができます。  
  
## <a name="finding-a-specific-service"></a>特定のサービスの検索  
 使用することも、<xref:Microsoft.VisualStudio.Settings.SettingsStore.CollectionExists%2A>する特定のサービスがインストールされているかどうかを判断するメソッド。 サービス クラスの型が必要です。  
  
1. 前の手順で作成したプロジェクトの MenuItemCallback での構成設定ストアを検索、`Services`という名前のサービスの GUID でサブコレクションを含むコレクション。 この場合、ヘルプ サービスを見ていきます。  
  
    ```  
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
  
3. 実験用インスタンスでは、上、**ツール** メニューのをクリックして**呼び出す FindServicesCommand**します。  
  
     テキスト メッセージが表示する必要があります**使用できるサービスのヘルプ:** 続けて**True**または**False**します。 この設定を確認するには、前の手順で示すように、レジストリ エディターを使用できます。
