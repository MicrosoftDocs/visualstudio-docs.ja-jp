---
title: Visual Studio におけるワークスペース ビルド | Microsoft Docs
description: フォルダーを開くシナリオをサポートするために、ワークスペースのインデックス付きおよびファイル コンテキスト データを提供するエクステンダーについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: e44c2398b873bbca95c971ae1b44ac3de831b2ae
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877105"
---
# <a name="workspace-build"></a>ワークスペース ビルド

[フォルダーを開く](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)シナリオでのビルド サポートには、実行するビルド アクションだけでなく、[ワークスペース](workspaces.md)の[インデックス付き](workspace-indexing.md)および[ファイル コンテキスト](workspace-file-contexts.md)データを提供するエクステンダーが必要です。

拡張機能に必要なものの概要を次に示します。

## <a name="build-file-context"></a>ビルド ファイル コンテキスト

- プロバイダー ファクトリ
  - `BuildContextTypes` のすべての適用可能な `string` 定数として `supportedContextTypeGuids` がある `ExportFileContextProviderAttribute` 属性
  - `IWorkspaceProviderFactory<IFileContextProvider>` を実装します
  - ファイル コンテキスト プロバイダー
    - サポートされるビルド操作と構成ごとに `FileContext` を返します
      - <xref:Microsoft.VisualStudio.Workspace.Build.BuildContextTypes> からの `contextType`
      - `context` は、`Configuration` プロパティをビルド構成として <xref:Microsoft.VisualStudio.Workspace.Build.IBuildConfigurationContext> を実装します (`"Debug|x86"`、`"ret"`、または該当しない場合は `null` など)。 または、単純に <xref:Microsoft.VisualStudio.Workspace.Build.BuildConfigurationContext> のインスタンス自体を使用します。 構成値は、インデックス付きのファイル データ値の構成と一致している **必要があります**。

## <a name="indexed-build-file-data-value"></a>インデックス付きビルド ファイルのデータ値

- プロバイダー ファクトリ
  - `IReadOnlyCollection<FileDataValue>` をサポートする型としての `ExportFileScannerAttribute` 属性
  - `IWorkspaceProviderFactory<IFileScanner>` を実装します
- `ScanContentAsync<T>` のファイル スキャナー
  - `FileScannerTypeConstants.FileDataValuesType` が型引数の場合にデータを返します
  - 次のように構築された各構成のファイル データ値を返します。
    - `type` as `BuildConfigurationContext.ContextTypeGuid`
    - ビルド構成としての `context` (`"Debug|x86"`、`"ret"`、または該当しない場合は `null` など)。 この値は、ファイル コンテキストの構成と一致している **必要があります**。

## <a name="build-file-context-action"></a>ビルド ファイル コンテキスト アクション

- プロバイダー ファクトリ
  - `BuildContextTypes` のすべての適用可能な `string` 定数として `supportedContextTypeGuids` がある `ExportFileContextActionProvider` 属性
  - `IWorkspaceProviderFactory<IFileContextActionProvider>` を実装します
- `IFileContextActionProvider.GetActionsAsync` のアクション プロバイダー
  - 指定された `FileContext.ContextType` 値と一致する `IFileContextAction` を返す
- ファイル コンテキスト アクション
  - `IFileContextAction` と <xref:Microsoft.VisualStudio.Workspace.Extensions.VS.IVsCommandItem> を実装します
  - `CommandGroup` プロパティは `16537f6e-cb14-44da-b087-d1387ce3bf57` を返します
  - `CommandId` は、ビルド用に `0x1000`、リビルド用に `0x1010`、またはクリーン用に `0x1020`

>[!NOTE]
>`FileDataValue` にはインデックスを作成する必要があるため、ワークスペースを開いてから、ファイルがスキャンされて完全なビルド機能が利用できるようになるまでには、一定の時間がかかります。 フォルダーを最初に開いたときは、以前にキャッシュされたインデックスが存在しないため、遅延が発生します。

## <a name="reporting-messages-from-a-build"></a>ビルドからのメッセージの報告

ビルドでは、次の 2 つの方法のいずれかで、情報、警告、およびエラー メッセージをユーザーに通知できます。 単純な方法は、<xref:Microsoft.VisualStudio.Workspace.Build.IBuildMessageService> を使用し、次のように <xref:Microsoft.VisualStudio.Workspace.Build.BuildMessage> を提供することです。

```csharp
using Microsoft.VisualStudio.Workspace;
using Microsoft.VisualStudio.Workspace.Build;

private static void OutputBuildMessage(IWorkspace workspace)
{
    IBuildMessageService buildMessageService = workspace.GetBuildMessageService();

    if (buildMessageService != null)
    {
      // Example error build message. See the documentation for BuildMessage for more information.
      var message = new BuildMessage()
      {
          Type = BuildMessage.TaskType.Error,
          Code = "MY1001",
          TaskText = "This is a sample error",
          ProjectFile = "buildfile.bld",
          File = "sourcefile.src"
          LogMessage = $"This is sample text that will only go to the Build output window pane.\n"

          // And any other properties to set
      };

      buildMessageService.ReportBuildMessages(new BuildMessage[] { message });
    }
}
```

`BuildMessage.Type` および `BuildMessage.LogMessage` は、ユーザーに情報が表示される場所の動作を制御します。 `None` 以外の `BuildMessage.TaskType` 値を指定すると、指定した詳細を含む **[エラー一覧]** エントリが生成されます。 `LogMessage` は常に **[出力]** ツール ウィンドウの **[ビルド]** ペインに出力されます。

または、拡張機能は、 **[エラー一覧]** または **[ビルド]** ペインと直接対話できます。 Visual Studio 2017 バージョン 15.7 より前のバージョンにはバグが存在し、<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane2.OutputTaskItemStringEx2*> の `pszProjectUniqueName` 引数が無視されます。

>[!WARNING]
>`IFileContextAction.ExecuteAsync` の呼び出し元は、`IProgress<IFileContextActionProgressUpdate>` 引数の基になる任意の実装を提供できます。 `IProgress<IFileContextActionProgressUpdate>.Report(IFileContextActionProgressUpdate)` を直接呼び出すことはできません。 現在、この引数を使用するための一般的なガイドラインはありませんが、これらのガイドラインは変更される可能性があります。

## <a name="build-related-apis"></a>ビルド関連の API

- <xref:Microsoft.VisualStudio.Workspace.Build.IBuildConfigurationContext> は、ビルド構成の詳細を提供します。
- <xref:Microsoft.VisualStudio.Workspace.Build.IBuildMessageService> は、ユーザーに <xref:Microsoft.VisualStudio.Workspace.Build.BuildMessage> を表示します。

## <a name="tasksvsjson-and-launchvsjson"></a>tasks.vs.json および launch.vs.json

tasks.vs.js ファイルまたは launch.vs.js ファイルを作成する方法については、[ビルド タスクとデバッグ タスクのカスタマイズ](../ide/customize-build-and-debug-tasks-in-visual-studio.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

* [言語サーバー プロトコル](language-server-protocol.md) -言語サーバーを Visual Studio に統合する方法について説明します。