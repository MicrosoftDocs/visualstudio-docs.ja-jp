---
title: '方法: アクティビティ ログの使用 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, debugging
- VSPackages, troubleshooting
ms.assetid: bb3d3322-0e5e-4dd5-b93a-24d5fbcd2ffd
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 53888f85a41fdd5bef3985c4da986609a032e377
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66309351"
---
# <a name="how-to-use-the-activity-log"></a>方法: アクティビティ ログを使用します。
Vspackage は、メッセージをアクティビティ ログに書き込むことができます。 この機能は、小売環境で Vspackage をデバッグするために特に便利です。

> [!TIP]
> アクティビティ ログは常にオンにします。 Visual Studio では、一般的な構成情報がある、最初の 10 個のエントリと同様に、最新の 100 個のエントリのローリング バッファーを保持します。

## <a name="to-write-an-entry-to-the-activity-log"></a>アクティビティ ログにエントリを書き込む

1. このコードを挿入、<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>メソッドまたはコンス トラクターは、VSPackage を除くその他の方法で。

    ```csharp
    IVsActivityLog log = GetService(typeof(SVsActivityLog)) as IVsActivityLog;
    if (log == null) return;

    int hr = log.LogEntry((UInt32)__ACTIVITYLOG_ENTRYTYPE.ALE_INFORMATION,
        this.ToString(),
        string.Format(CultureInfo.CurrentCulture,
        "Called for: {0}", this.ToString()));
    ```

     このコードを取得、<xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog>サービスおよびにキャスト、<xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>インターフェイス。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog.LogEntry%2A> 現在のカルチャのコンテキストを使用してアクティビティ ログに情報のエントリを書き込みます。

2. (通常は、コマンドが呼び出されたまたはウィンドウを開いた) ときに VSPackage が読み込まれるときに、テキストは、アクティビティ ログに書き込まれます。

## <a name="to-examine-the-activity-log"></a>アクティビティ ログを確認するには

1. Visual Studio での実行、 [/log](../ide/reference/log-devenv-exe.md) ActivityLog.xml をディスクに書き込むセッション中にコマンド ライン スイッチ。

2. Visual Studio を閉じた後に、Visual Studio のデータのサブフォルダーでアクティビティ ログを検索します。

   <em> *%AppData%</em>\Microsoft\VisualStudio\\\<version>\ActivityLog.xml*.

3. 任意のテキスト エディターでは、アクティビティ ログを開きます。 一般的なエントリを次に示します。

   ```
   Called for: Company.MyApp.MyAppPackage ...
   ```

## <a name="robust-programming"></a>信頼性の高いプログラミング

アクティビティ ログは、サービスであるためには、アクティビティ ログは、VSPackage のコンス トラクターで使用できません。

記述する前に、アクティビティ ログを取得する必要があります。 キャッシュしたり、将来使用するためのアクティビティ ログを保存しないでください。

## <a name="see-also"></a>関連項目

- [/Log (devenv.exe)](../ide/reference/log-devenv-exe.md)
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>
- <xref:Microsoft.VisualStudio.Shell.Interop.__ACTIVITYLOG_ENTRYTYPE>
- [VSPackage のトラブルシューティング](../extensibility/troubleshooting-vspackages.md)
- [VSPackage](../extensibility/internals/vspackages.md)
