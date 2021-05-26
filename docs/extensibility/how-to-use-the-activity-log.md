---
title: '方法: アクティビティ ログを使用する | Microsoft Docs'
description: VSPackage では、アクティビティ ログにメッセージを書き込むことができます。 リテール環境で VSPackage をデバッグするためにアクティビティ ログを使用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- VSPackages, debugging
- VSPackages, troubleshooting
ms.assetid: bb3d3322-0e5e-4dd5-b93a-24d5fbcd2ffd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f02a8dd1497680239db9363a2e0682082f0c68d8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057339"
---
# <a name="how-to-use-the-activity-log"></a>方法: アクティビティ ログを使用する
VSPackage では、アクティビティ ログにメッセージを書き込むことができます。 この機能は、リテール環境で VSPackage をデバッグする場合に特に便利です。

> [!TIP]
> アクティビティ ログは常にオンになっています。 Visual Studio では、一般的な構成情報を持つ最後の 100 のエントリと最初の 10 のエントリのローリング バッファーが保持されます。

## <a name="to-write-an-entry-to-the-activity-log"></a>アクティビティ ログにエントリを書き込む方法

1. 次のように、このコードを VSPackage コンストラクターを除く、<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> メソッドまたは他の任意のメソッドに挿入します。

    ```csharp
    IVsActivityLog log = GetService(typeof(SVsActivityLog)) as IVsActivityLog;
    if (log == null) return;

    int hr = log.LogEntry((UInt32)__ACTIVITYLOG_ENTRYTYPE.ALE_INFORMATION,
        this.ToString(),
        string.Format(CultureInfo.CurrentCulture,
        "Called for: {0}", this.ToString()));
    ```

     このコードにより、<xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog> サービスが取得され、それが <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> インターフェイスにキャストされます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog.LogEntry%2A> により、現在のカルチャ コンテキストを使用して、情報エントリがアクティビティ ログに書き込まれます。

2. VSPackage が読み込まれると (通常はコマンドが呼び出されたとき、またはウィンドウが開かれたときに)、テキストがアクティビティ ログに書き込まれます。

## <a name="to-examine-the-activity-log"></a>アクティビティ ログを調べる方法

1. [/Log](../ide/reference/log-devenv-exe.md) コマンド ライン スイッチを使用して Visual Studio を実行し、セッション中にディスクに ActivityLog.xml を書き込みます。

2. Visual Studio を終了した後、Visual Studio データの次のサブフォルダーでアクティビティ ログを見つけます。

   <em> *%AppData%</em>\Microsoft\VisualStudio\\\<version>\ActivityLog.xml*.

3. 任意のテキスト エディターを使用して、アクティビティ ログを開きます。 典型的なエントリを次に示します。

   ```
   Called for: Company.MyApp.MyAppPackage ...
   ```

## <a name="robust-programming"></a>信頼性の高いプログラミング

アクティビティ ログはサービスであるため、アクティビティ ログは VSPackage コンストラクターでは使用できません。

書き込みの直前にアクティビティ ログを取得する必要があります。 将来使用するために、アクティビティ ログをキャッシュまたは保存しないでください。

## <a name="see-also"></a>関連項目

- [/Log (devenv.exe)](../ide/reference/log-devenv-exe.md)
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>
- <xref:Microsoft.VisualStudio.Shell.Interop.__ACTIVITYLOG_ENTRYTYPE>
- [VSPackage のトラブルシューティング](../extensibility/troubleshooting-vspackages.md)
- [VSPackages](../extensibility/internals/vspackages.md)
