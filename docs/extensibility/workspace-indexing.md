---
title: Visual Studio におけるワークスペースのインデックス作成 | Microsoft Docs
description: ワークスペースのインデックス作成について説明します。これは、[フォルダーを開く] ワークスペースの豊富な IDE 機能をサポートするためのデータの収集と永続的な格納です。
ms.custom: SEO-VS-2020
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 6b5c069ce3ae993f2d2371bffae3ac58b286fa70
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877053"
---
# <a name="workspace-indexing"></a>ワークスペースのインデックス作成

ソリューションでは、プロジェクト システムがビルド、デバッグ、シンボルへ **移動** の検索などの機能を提供する役割を担います。 プロジェクト システムはプロジェクト内のファイルの関係と機能を把握しているため、この作業を行うことができます。 [[フォルダーを開く]](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md) ワークスペースにも、豊富な IDE 機能を提供するために同じ分析情報が必要です。 このデータの収集と永続的な格納が、ワークスペースのインデックス作成と呼ばれるプロセスです。 このインデックス付きデータは、一連の非同期 API を使用して照会できます。 エクステンダーは、特定の種類のファイルの処理方法を認識する <xref:Microsoft.VisualStudio.Workspace.Indexing.IFileScanner> を指定することによって、インデックス作成プロセスに参加できます。

## <a name="types-of-indexed-data"></a>インデックス付きデータの型

3 種類のデータのインデックスが作成されます。 ファイル スキャナーから要求される型は、インデックスから逆シリアル化される型とは異なることに注意してください。

|Data|ファイル スキャナーの型|インデックス クエリの結果の型|関連する型|
|--|--|--|--|
|References|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileReferenceInfo>|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileReferenceResult>|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileReferenceInfoType>|
|記号|<xref:Microsoft.VisualStudio.Workspace.Indexing.SymbolDefinition>|<xref:Microsoft.VisualStudio.Workspace.Indexing.SymbolDefinitionSearchResult>|クエリに対しては、`IIndexWorkspaceService` ではなく <xref:Microsoft.VisualStudio.Workspace.Indexing.ISymbolService> を使用する必要があります。|
|データの値|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileDataValue>|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileDataResult`1>||

## <a name="querying-for-indexed-data"></a>インデックス付きデータのクエリ

持続的なデータにアクセスするには、2 つの非同期型を使用できます。 1 つ目は <xref:Microsoft.VisualStudio.Workspace.Indexing.IIndexWorkspaceData> を使用する方法です。 これは、1 つのファイルの `FileReferenceResult` と `FileDataResult` データへの基本的なアクセスを提供し、結果をキャッシュします。 2 つ目は <xref:Microsoft.VisualStudio.Workspace.Indexing.IIndexWorkspaceService> です。これはキャッシュを使用しませんが、より多くのクエリ機能に対応しています。

```csharp
using Microsoft.VisualStudio.Workspace;
using Microsoft.VisualStudio.Workspace.Indexing;

private static IIndexWorkspaceData GetCachedIndexedData(IWorkspace workspace)
{
    // Gets access to indexed data wrapped in a cache.
    return workspace?.GetIndexWorkspaceDataService()?.CreateIndexWorkspaceData();
}

private static IIndexWorkspaceService GetDirectIndexedData(IWorkspace workspace)
{
    // Gets direct access to indexed data.
    // Can also be casted to IIndexWorkspaceService2.
    return workspace?.GetIndexWorkspaceService();
}
```

## <a name="participating-in-indexing"></a>インデックス作成への参加

大まかなワークスペースのインデックス作成順序は次のとおりです。

1. ワークスペース内のファイル システム エンティティの検出と永続化 (最初に開いているスキャンの場合のみ)。
1. ファイルごとに、優先順位が最も高い一致プロバイダーが `FileReferenceInfo` をスキャンするよう求められます。
1. ファイルごとに、優先順位が最も高い一致プロバイダーが `SymbolDefinition` をスキャンするよう求められます。
1. ファイルごとに、すべてのプロバイダーに対して `FileDataValue` が要求されます。

拡張機能では、<xref:Microsoft.VisualStudio.Workspace.Indexing.ExportFileScannerAttribute> を使用して `IWorkspaceProviderFactory<IFileScanner>` を実装し、型をエクスポートすることによって、スキャナーをエクスポートできます。 `SupportedTypes` 属性引数は、<xref:Microsoft.VisualStudio.Workspace.Indexing.FileScannerTypeConstants> から取得する 1 つ以上の値である必要があります。 スキャナーの例については、VS SDK の[サンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples/blob/master/Open_Folder_Extensibility/C%23/SymbolScannerSample/TxtFileSymbolScanner.cs)を参照してください。

> [!WARNING]
> `FileScannerTypeConstants.FileScannerContentType` 型をサポートするファイル スキャナーをエクスポートしないでください。 これは、Microsoft の内部目的にのみ使用されます。

高度な状況では、任意のセットのファイルの種類が拡張機能で動的にサポートされる場合があります。 MEF による `IWorkspaceProviderFactory<IFileScanner>` のエクスポートの代わりに、拡張機能で `IWorkspaceProviderFactory<IFileScannerProvider>` をエクスポートできます。 インデックス作成が開始されると、このファクトリ型がインポートされ、インスタンス化されて、その <xref:Microsoft.VisualStudio.Workspace.Indexing.IFileScannerProvider.GetSymbolScannersAsync%2A> メソッドが呼び出されます。 シンボルだけでなく、`FileScannerTpeConstants` から取得する任意の値をサポートする `IFileScanner` インスタンスが受け入れられます。

## <a name="next-steps"></a>次のステップ

* [ワークスペースと言語サービス](workspace-language-services.md) - 言語サービスを [フォルダーを開く] ワークスペースに統合する方法について説明します。
* [ワークスペース ビルド](workspace-build.md) - [フォルダーを開く] では、MSBuild やメイクファイルなどのビルド システムがサポートされます。