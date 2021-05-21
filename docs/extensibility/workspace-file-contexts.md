---
title: Visual Studio におけるワークスペースのファイル コンテキスト | Microsoft Docs
description: IFileContextProvider インターフェイスを実装して、[フォルダーを開く] ワークスペースの分析情報をサポートするファイル コンテキスト プロバイダーについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 271b05d78123136d47cb618e8ed38cea64b7beac
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877066"
---
# <a name="workspace-file-contexts"></a>ワークスペースのファイル コンテキスト

[[フォルダーを開く]](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md) ワークスペースのすべての分析情報は、<xref:Microsoft.VisualStudio.Workspace.IFileContextProvider> インターフェイスを実装する "ファイル コンテキスト プロバイダー" によって生成されます。 これらの拡張機能により、フォルダーまたはファイル内のパターンの検索、MSBuild ファイルとメイクファイルの読み取り、パッケージの依存関係の検出などを行って、ファイル コンテキストを定義するために必要な分析情報を蓄積できます。 ファイル コンテキスト自体はアクションを実行しませんが、別の拡張機能で操作できるデータを提供します。

各 <xref:Microsoft.VisualStudio.Workspace.FileContext> には、受け渡すデータの型を識別する `Guid` が関連付けられています。 ワークスペースではこの `Guid` を後から使用して、<xref:Microsoft.VisualStudio.Workspace.FileContext.Context> プロパティを通じてデータを使用する拡張機能と一致させます。 ファイル コンテキスト プロバイダーは、データの生成対象となるファイル コンテキストの `Guid` を識別するメタデータと共にエクスポートされます。

定義されたファイル コンテキストは、ワークスペース内の任意の数のファイルまたはフォルダーに関連付けることができます。 指定されたファイルまたはフォルダーを、任意の数のファイル コンテキストに関連付けることができます。 これは多対多リレーションシップです。

ファイル コンテキストの最も一般的なシナリオは、ビルド、デバッグ、および言語サービスに関連するものです。 詳細については、これらのシナリオに関する別のトピックを参照してください。

## <a name="file-context-lifecycle"></a>ファイル コンテキストのライフサイクル

`FileContext` のライフサイクルは非確定的です。 コンポーネントはいつでも、何らかのコンテキスト型のセットを非同期的に要求できます。 要求コンテキスト型の一部のサブセットをサポートするプロバイダーに対してクエリが実行されます。 `IWorkspace` インスタンスは、<xref:Microsoft.VisualStudio.Workspace.IWorkspace.GetFileContextsAsync%2A> メソッドを通じてコンシューマーとプロバイダーの間の中間者として機能します。 コンシューマーは、コンテキストを要求し、そのコンテキストに基づいて短期的なアクションを実行します。一方、コンテキストを要求し、有効期間の長い参照を維持するコンシューマーも存在します。

ファイル コンテキストの期限切れを引き起こすファイルは変更される可能性があります。 プロバイダーは `FileContext` でイベントを発生させて、コンシューマーに更新を通知できます。 たとえば、あるファイルに対してビルド コンテキストが提供されていても、ディスク上の変更によってそのコンテキストが無効になった場合、元のプロデューサーはイベントを呼び出すことができます。 その `FileContext` を参照しているコンシューマーは、新しい `FileContext` のクエリを再び実行できます。

>[!NOTE]
>コンシューマーに対するプッシュ モデルはありません。 要求後にコンシューマーがプロバイダーの新しい `FileContext` について通知を受け取ることはありません。

## <a name="expensive-file-context-computations"></a>負荷のかかるファイル コンテキストの計算

ディスクからのファイルのコンテンツの読み取りには負荷がかかる可能性があります (特に、プロバイダーがファイル間のリレーションシップを解決する必要がある場合)。 たとえば、ソース ファイルのファイル コンテキストのクエリをプロバイダーに対して実行することは可能ですが、ファイル コンテキストはプロジェクト ファイルのメタデータに依存します。 プロジェクト ファイルを解析したり、MSBuild で評価したりする処理は負荷が高くなります。 代わりに、拡張機能によって `IFileScanner` をエクスポートして、ワークスペースのインデックス作成中に `FileDataValue` データを作成できます。 これで、ファイル コンテキストを要求されたときに、`IFileContextProvider` はそのインデックス付きデータのクエリを迅速に実行できるようになります。 インデックス作成の詳細については、「[ワークスペースのインデックス作成](workspace-indexing.md)」を参照してください。

>[!WARNING]
>他の方法でも `FileContext` の計算に負荷がかかる可能性があることに注意してください。 一部の UI 操作は同期的であり、大量の `FileContext` 要求に依存します。 たとえば、エディター タブを開く操作や **ソリューション エクスプローラー** のコンテキスト メニューを開く操作などです。 これらのアクションは、多数のビルド コンテキスト型の要求を行います。

## <a name="file-context-related-apis"></a>ファイル コンテキストに関連する API

- <xref:Microsoft.VisualStudio.Workspace.FileContext> は、データとメタデータを保持します。
- <xref:Microsoft.VisualStudio.Workspace.IFileContextProvider> と <xref:Microsoft.VisualStudio.Workspace.IFileContextProvider`1> は、ファイル コンテキストを作成します。
- <xref:Microsoft.VisualStudio.Workspace.ExportFileContextProviderAttribute> は、ファイル コンテキスト プロバイダーをエクスポートします。
- <xref:Microsoft.VisualStudio.Workspace.IWorkspace.GetFileContextsAsync%2A> は、ファイル コンテキストを取得するためにコンシューマーで使用されます。
- <xref:Microsoft.VisualStudio.Workspace.Build.BuildContextTypes> は、[フォルダーを開く] で使用するビルド コンテキスト型を定義します。

## <a name="file-context-actions"></a>ファイル コンテキスト アクション

`FileContext` 自体は一部のファイルに関するデータにすぎませんが、<xref:Microsoft.VisualStudio.Workspace.IFileContextAction> はそのデータを表現して操作するための方法です。 `IFileContextAction` は柔軟に使用できます。 最も一般的な 2 つのケースはビルドとデバッグです。

## <a name="reporting-progress"></a>進行状況を報告する

<xref:Microsoft.VisualStudio.Workspace.IFileContextActionBase.ExecuteAsync%2A> メソッドによって `IProgress<IFileContextActionProgressUpdate>` が渡されますが、引数をその型として使用することはできません。 `IFileContextActionProgressUpdate` は空のインターフェイスであり、`IProgress<IFileContextActionProgressUpdate>.Report(IFileContextActionProgressUpdate)` を呼び出すと `NotImplementedException` がスローされる場合があります。 代わりに、`IFileContextAction` がシナリオに応じて引数を別の型にキャストする必要があります。

Visual Studio で提供される型については、各シナリオのドキュメントを参照してください。

## <a name="file-context-action-related-apis"></a>ファイル コンテキスト アクションに関連する API

- <xref:Microsoft.VisualStudio.Workspace.IFileContextAction> は、`FileContext` に基づいて動作を実行します。
- <xref:Microsoft.VisualStudio.Workspace.IFileContextActionProvider> は、`IFileContextAction` のインスタンスを作成します。
- <xref:Microsoft.VisualStudio.Workspace.ExportFileContextActionProviderAttribute> は、`IWorkspaceProviderFactory<IFileContextActionProvider>` 型をエクスポートします。

## <a name="file-watching"></a>ファイルの監視

ワークスペースは、ファイルの変更通知をリッスンし、<xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper.GetFileWatcherService%2A> を通じて <xref:Microsoft.VisualStudio.Workspace.IFileWatcherService> を提供します。 "ExcludedItems" 設定が一致するファイルは、ファイル通知イベントを生成しません。 イベント間のしきい値は、通知の簡略化と重複の削減に使用されます。 ファイルの変更に対処する必要がある場合は、このサービスをサブスクライブしてください。

>[!TIP]
>ワークスペースの[インデックス作成サービス](workspace-indexing.md)では、既定でファイル イベントをサブスクライブします。 ファイルの追加と変更により、関連する `IFileScanner` イベントがそのファイルの新しいデータに対して呼び出されます。 ファイルの削除により、インデックス付きデータが削除されます。 ファイル監視サービスに対して `IFileScanner` をサブスクライブする必要はありません。

## <a name="next-steps"></a>次のステップ

* [インデックス作成](workspace-indexing.md)ワークスペースのインデックス作成では、ワークスペースに関する情報を収集して保持します。
* [ワークスペース](workspaces.md) - ワークスペースの概念と設定の格納について確認します。
