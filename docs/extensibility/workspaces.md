---
title: Visual Studio におけるワークスペース | Microsoft Docs
description: Visual Studio でワークスペースを使用して、[フォルダーを開く] 内のファイルのコレクションを表す方法、およびワークスペース プロバイダーとサービスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 1ed660a5f52aba548d087b28f7caea4d1966fe45
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97876949"
---
# <a name="workspaces"></a>Workspaces

Visual Studio ではワークスペースを使用して、[[フォルダーを開く]](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md) 内のファイルのコレクションを表します。ワークスペースは <xref:Microsoft.VisualStudio.Workspace.IWorkspace> 型で表されます。 ワークスペース自体は、フォルダー内のファイルに関連するコンテンツや機能を認識しません。 その代わりに、他の機能で操作できるデータを生成して使用するための機能と拡張機能の一般的な API のセットを提供します。 プロデューサーは、[Managed Extensibility Framework](https://github.com/Microsoft/vs-mef/blob/master/doc/index.md) (MEF) を通じてさまざまなエクスポート属性を使用して構成されます。

## <a name="workspace-providers-and-services"></a>ワークスペース プロバイダーとサービス

ワークスペース プロバイダーとサービスは、ワークスペースのコンテンツに応答するためのデータと機能を提供します。 これらはコンテキスト ファイルの情報、ソース ファイル内のシンボル、またはビルド機能を提供する場合があります。

どちらの概念も [Factory パターン](https://en.wikipedia.org/wiki/Factory_method_pattern)を使用し、ワークスペースによって MEF を通じてインポートされます。 すべてのエクスポート属性は `IProviderMetadataBase` または `IWorkspaceServiceFactoryMetadata` を実装しますが、拡張機能ではエクスポートされた型に具象型を使用する必要があります。

プロバイダーとサービスの違いの 1 つは、ワークスペースとの関係です。 ワークスペースには特定の型のプロバイダーを多数含めることができますが、ワークスペースごとに作成される特定の型のサービスは 1 つだけです。 たとえば、ワークスペースには多数のファイル スキャナー プロバイダーがありますが、1 つのワークスペースに含まれているインデックス作成サービスは 1 つだけです。

もう 1 つの重要な違いは、プロバイダーとサービスからのデータの使用です。 ワークスペースは、いくつかの理由でプロバイダーからデータを取得するためのエントリ ポイントです。 まず、プロバイダーは通常、作成するデータのセットを絞り込みます。 このデータは、C# ソース ファイル用のシンボルまたは _CMakeLists.txt_ ファイル用のビルド ファイル コンテキストである場合があります。 ワークスペースでは、コンシューマーの要求と、メタデータがその要求と一致するプロバイダーを照合します。 また、多数のプロバイダーによる要求の処理が許可される場合もありますが、優先順位が最も高いプロバイダーが使用される場合もあります。

一方、拡張機能では、ワークスペース サービスのインスタンスを取得して、そのサービスと直接対話できます。 `IWorkspace` の拡張メソッドは、Visual Studio が提供するサービス (<xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper.GetFileWatcherService%2A> など) で使用できます。 拡張機能では、その機能内のコンポーネントまたは使用する他の拡張機能のためのワークスペース サービスを提供する場合があります。 コンシューマーでは、<xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper.GetServiceAsync%2A> または `IWorkspace` 型で指定した拡張メソッドを使用する必要があります。

>[!WARNING]
> Visual Studio と競合するサービスは作成しないでください。 予期しない問題が発生する可能性があります。

## <a name="disposal-on-workspace-closure"></a>ワークスペースの終了時の破棄

ワークスペースの終了時には、エクステンダーが破棄を実行し、非同期コードを呼び出さなければならない場合があります。 このコードを簡単に記述できるようにするために、<xref:Microsoft.VisualStudio.Threading.IAsyncDisposable> インターフェイスが用意されています。

## <a name="related-types"></a>関連する型

- <xref:Microsoft.VisualStudio.Workspace.IWorkspace> は、開いているフォルダーと同様に、開いているワークスペースの中心的なエンティティです。
- <xref:Microsoft.VisualStudio.Workspace.IWorkspaceProviderFactory`1> は、インスタンス化されたワークスペースごとにプロバイダーを作成します。
- <xref:Microsoft.VisualStudio.Workspace.IWorkspaceServiceFactory> は、インスタンス化されたワークスペースごとにサービスを作成します。
- <xref:Microsoft.VisualStudio.Threading.IAsyncDisposable> は、破棄の際に非同期コードを実行する必要のあるプロバイダーとサービスに実装してください。
- <xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper> は、既知のサービスまたは任意のサービスにアクセスするためのヘルパー メソッドを提供します。

## <a name="workspace-settings"></a>ワークスペースの設定

ワークスペースには、シンプルで強力な制御機能を備えた <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsManager> サービスがあります。 設定の基本的な概要については、[ビルド タスクとデバッグ タスクのカスタマイズ](../ide/customize-build-and-debug-tasks-in-visual-studio.md)に関する記事を参照してください。

ほとんどの `SettingsType` 型の設定は _.json_ ファイル (_VSWorkspaceSettings.json_、_tasks.vs.json_ など) です。

ワークスペースの設定の軸となるのは "スコープ" です。スコープは、ワークスペース内の単なるパスです。 コンシューマーが <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsManager.GetAggregatedSettings%2A> を呼び出すと、要求されたパスと設定の型を含むすべてのスコープが集計されます。 スコープ集計の優先順位は次のとおりです。

1. "ローカル設定" (通常は、ワークスペースのルートの `.vs` ディレクトリ)。
1. 要求されたパス自体。
1. 要求されたパスの親ディレクトリ。
1. ワークスペースのルートまでの (自身を含む) すべての親ディレクトリ。
1. "グローバル設定" (ユーザー ディレクトリ内)。

結果は <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettings> のインスタンスです。 このオブジェクトは特定の型の設定を保持し、`string` として格納されるキー名を設定するために照会できます。 <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettings.GetProperty%2A> メソッドと <xref:Microsoft.VisualStudio.Workspace.Settings.WorkspaceSettingsExtensions> 拡張メソッドは、要求される設定値の型を呼び出し元が認識していると想定します。 ほとんどの設定ファイルは _.json_ ファイルとして保持されるため、多くの呼び出しでは `string`、`bool`、`int`、およびこれらの型の配列が使用されます。 また、オブジェクトの種類もサポートされます。 その場合、`IWorkspaceSettings` 自体を型引数として使用できます。 次に例を示します。

```json
{
  "intValue": 1,
  "stringValue": "s",
  "boolValue": true,
  "stringArray": [
    "s1",
    "s2"
  ],
  "nestedIWorkspaceSettings": {
    "nestedString": "ns"
  }
}
```

これらの設定がユーザーの _VSWorkspaceSettings.json_ に含まれていると仮定すると、データには次のようにアクセスできます。

```csharp
using System.Collections.Generic;
using Microsoft.VisualStudio.Workspace;
using Microsoft.VisualStudio.Workspace.Settings;

private static void ReadSettings(IWorkspace workspace)
{
    IWorkspaceSettingsManager settingsManager = workspace.GetSettingsManager();
    IWorkspaceSettings settings = settingsManager.GetAggregatedSettings(SettingsTypes.Generic);

    // result == WorkspaceSettingsResult.Success
    WorkspaceSettingsResult result = settings.GetProperty("intValue", out int intValue);
    result = settings.GetProperty("stringValue", out string stringValue);
    result = settings.GetProperty("boolValue", out bool boolValue);
    result = settings.GetProperty("stringArray", out string[] stringArray);
    result = settings.GetProperty("nestedIWorkspaceSettings", out IWorkspaceSettings nestedIWorkspaceSettings);
    result = nestedIWorkspaceSettings.GetProperty("nestedString", out string nestedString);

    // Extension method alternative using default values.
    int intValueOrDefault = settings.Property("intValue", /* default */ 42);

    // Missing key. result == WorkspaceSettingsResult.Undefined
    result = settings.GetProperty("missing", out string missing);

    // Wrong type for a key. result == WorkspaceSettingsResult.Error
    result = settings.GetProperty("intValue", out IWorkspaceSettings notSettings);

    // Special ability to union "stringArray" across all scopes.
    IEnumerable<string> allStringArray = settings.UnionPropertyArray<string>("stringArray");
}
```

>[!NOTE]
>これらの設定 API は、`Microsoft.VisualStudio.Settings` 名前空間で使用できる API とは無関係です。 ワークスペースの設定はホストに依存せず、ワークスペース固有の設定ファイルまたは動的設定プロバイダーを使用します。

### <a name="providing-dynamic-settings"></a>動的設定の提供

拡張機能では <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsProvider> を提供できます。 これらのメモリ内プロバイダーを使用すると、拡張機能で設定を追加したり、他の設定をオーバーライドしたりできます。

`IWorkspaceSettingsProvider` のエクスポートは、他のワークスペース プロバイダーとは異なります。 Factory は `IWorkspaceProviderFactory` ではなく、特別な属性の型はありません。 代わりに、<xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsProviderFactory> を実装し、`[Export(typeof(IWorkspaceSettingsProviderFactory))]` を使用してください。

```csharp
// Common workspace provider factory pattern
[ExportFeatureProvider(some, args, to, export)]
internal class MyProviderFactory : IWorkspaceProviderFactory<IFeatureProvider>
{
     IFeatureProvider CreateProvider(IWorkspace workspace) => new Provider(workspace);
}

// IWorkspaceSettingsProvider pattern
[Export(typeof(IWorkspaceSettingsProviderFactory))]
internal class MySettingsProviderFactory : IWorkspaceSettingsProviderFactory
{
    // 100 is typically the value used by built-in settings providers. Lower value is higher priority.
    int Priority => 100;

    IWorkspaceSettingsProvider CreateSettingsProvider(IWorkspace workspace) => new MySettingsProvider(workspace);
}
```

>[!TIP]
>`IWorkspaceSettingsSource` を返すメソッド (`IWorkspaceSettingsProvider.GetSingleSettings` など) を実装する場合は、`IWorkspaceSettingsSource` ではなく `IWorkspaceSettings` のインスタンスを返します。 `IWorkspaceSettings` は、一部の設定の集計時に役立つ詳細情報を提供します。

### <a name="settings-related-apis"></a>設定に関連する API

- <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsManager> は、ワークスペースの設定を読み取って集計します。
- <xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper.GetSettingsManager%2A> は、ワークスペースの `IWorkspaceSettingsManager` を取得します。
- <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsManager.GetAggregatedSettings%2A> は、重複するすべてのスコープで集計された特定のスコープの設定を取得します。
- <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettings> には、特定のスコープの設定が格納されます。

## <a name="workspace-suggested-practices"></a>ワークスペースで推奨される手法

- `IWorkspaceProviderFactory.CreateProvider` または作成時に `Workspace` コンテキストを記憶している同様の API からオブジェクトを返します。 プロバイダー インターフェイスは、このオブジェクトが作成時に保持されることを想定して記述されます。
- ワークスペース固有のキャッシュまたは設定を、ワークスペースの "ローカル設定" パス内に保存します。 Visual Studio 2017 バージョン 15.6 以降では、`Microsoft.VisualStudio.Workspace.WorkspaceHelper.MakeRootedUnderWorkingFolder` を使用してファイルのパスを作成します。 15.6 より前のバージョンでは、次のスニペットを使用します。

```csharp
using System.IO;
using Microsoft.VisualStudio.Workspace;
using Microsoft.VisualStudio.Workspace.Settings;

private static string MakeRootedUnderWorkingFolder(IWorkspace workspace, string relativePath)
{
    string workingFolder = workspace.GetSettingsManager().GetAggregatedSettings(SettingsTypes.WorkspaceControlSettings).Property<string>("WorkingFolder");
    return Path.Combine(workingFolder, relativePath);
}
```

## <a name="solution-events-and-package-auto-load"></a>ソリューション イベントとパッケージの自動読み込み

読み込まれたパッケージでは `IVsSolutionEvents7` を実装して、`IVsSolution.AdviseSolutionEvents` を呼び出すことができます。 これには、Visual Studio でフォルダーを開いたり閉じたりする際のイベントが含まれます。

UI コンテキストを使用すると、パッケージを自動的に読み込むことができます。 値が `4646B819-1AE0-4E79-97F4-8A8176FDD664` です。

## <a name="troubleshooting"></a>トラブルシューティング

### <a name="the-sourceexplorerpackage-package-did-not-load-correctly"></a>SourceExplorerPackage パッケージが正しく読み込まれなかった

ワークスペースの拡張性は MEF に基づく部分が大きいため、構成エラーが発生すると、[フォルダーを開く] をホストしているパッケージの読み込みに失敗します。 たとえば、`ExportFileContextProviderAttribute` が指定された型を拡張機能でエクスポートする際、その型が `IWorkspaceProviderFactory<IFileContextActionProvider>` だけを実装する場合は、Visual Studio でフォルダーを開こうとするとエラーが発生します。

::: moniker range="vs-2017"

エラーの詳細は、 _%LOCALAPPDATA%\Microsoft\VisualStudio\15.0_id\ComponentModelCache\Microsoft.VisualStudio.Default.err_ で確認できます。 拡張機能によって実装された型に関するエラーをすべて解決してください。

::: moniker-end

::: moniker range=">=vs-2019"

エラーの詳細は、 _%LOCALAPPDATA%\Microsoft\VisualStudio\16.0_id\ComponentModelCache\Microsoft.VisualStudio.Default.err_ で確認できます。 拡張機能によって実装された型に関するエラーをすべて解決してください。

::: moniker-end

## <a name="next-steps"></a>次のステップ

* [ファイル コンテキスト](workspace-file-contexts.md) - ファイル コンテキスト プロバイダーにより、[フォルダーを開く] ワークスペースに対してコード インテリジェンスが提供されます。
* [インデックス作成](workspace-indexing.md)ワークスペースのインデックス作成では、ワークスペースに関する情報を収集して保持します。
