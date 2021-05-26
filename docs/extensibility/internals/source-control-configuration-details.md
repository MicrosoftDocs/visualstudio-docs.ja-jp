---
title: ソース管理構成の詳細 | Microsoft Docs
description: Visual Studio でプロジェクト タイプのソース管理を実装する方法について説明します。これには、アクセス許可を要求するようにプロジェクト システムまたはエディターを構成する作業が含まれます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], configuration details
ms.assetid: adbee9fc-7a2e-4abe-a3b8-e6615bcd797f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a5c93e690922057116b395bed3881627e8a37847
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069349"
---
# <a name="source-control-configuration-details"></a>ソース管理構成の詳細
ソース管理を実装するためには、次のことを実行するようにプロジェクト システムまたはエディターを適切に構成する必要があります。

- 変更済み状態に遷移するためのアクセス許可を要求する

- ファイルを保存するためのアクセス許可を要求する

- プロジェクト内のファイルを追加、削除、または名前変更するためのアクセス許可を要求する

## <a name="request-permission-to-transition-to-changed-state"></a>変更済み状態に遷移するためのアクセス許可を要求する
 プロジェクトまたはエディターでは、変更済み (ダーティ) 状態に遷移するためのアクセス許可を、<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> を呼び出して要求する必要があります。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty%2A> を実装する各エディターは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty%2A> に対して `True` を返す前に、<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> を呼び出し、ドキュメントを変更するための承認を環境から受ける必要があります。 プロジェクトは基本的にはプロジェクト ファイルのエディターであり、その結果、テキスト エディターがそのファイルに対して行うのと同じように、プロジェクト ファイルの状態変更追跡を実装する責任があります。 ソリューションの状態変更は環境によって処理されますが、プロジェクト ファイルやそのアイテムなど、ソリューションが参照するが保存はしないオブジェクトの状態変更は人の手で処理する必要があります。 一般に、アイテムの永続性管理についてプロジェクトまたはエディターに責任がある場合、状態変更追跡の実装についてはこれらに責任があります。

 `IVsQueryEditQuerySave2::QueryEditFiles` の呼び出しに応答して、環境では次の処理を実行できます。

- 変更のための呼び出しを拒否します。その場合、エディターまたはプロジェクトは未変更 (クリーン) 状態にとどまる必要があります。

- ドキュメント データを再度読み込む必要があることを示します。 プロジェクトの場合、プロジェクトの代わりに環境によってデータが再度読み込まれます。 エディターでは、その <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A> 実装を通じて、ディスクからデータを再度読み込む必要があります。 どちらの場合も、データが再度読み込まれると、プロジェクトまたはエディターのコンテキストが変化する可能性があります。

  それは、適切な `IVsQueryEditQuerySave2::QueryEditFiles` の呼び出しを既存のコード ベースに後付けするという複雑で困難なタスクです。 そのため、これらの呼び出しは、プロジェクトまたはエディターの作成中に統合する必要があります。

## <a name="request-permission-to-save-a-file"></a>ファイルを保存するためのアクセス許可を要求する
 プロジェクトまたはエディターでは、ファイルを保存する前に <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A> または <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A> を呼び出す必要があります。 プロジェクトファイルの場合、これらの呼び出しは、プロジェクト ファイルを保存するタイミングを認識しているソリューションによって自動的に完了されます。 `IVsPersistDocData2` のエディター実装でヘルパー関数 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A> を使用する場合を除き、これらの呼び出しを行うのはエディターの責任です。 エディターで `IVsPersistDocData2` をこのように実装した場合、`IVsQueryEditQuerySave2::QuerySaveFile` または `IVsQueryEditQuerySave2::QuerySaveFiles` の呼び出しは自動的に行われます。

> [!NOTE]
> これらの呼び出しは常にプリエンプティブに、つまり、エディターでキャンセルの受け付けが可能になった時点で行うようにしてください。

## <a name="request-permission-to-add-remove-or-rename-files-in-the-project"></a>プロジェクト内のファイルを追加、削除、または名前変更するためのアクセス許可を要求する
 プロジェクトでは、まず適切な `IVsTrackProjectDocuments2::OnQuery*` メソッドを呼び出して環境からのアクセス許可を要求しない限り、ファイルまたはディレクトリの追加、名前変更、または削除を実行できません。 アクセス許可が付与されている場合、プロジェクトでは、操作を完了した後、適切な `IVsTrackProjectDocuments2::OnAfter*` メソッドを呼び出して、操作が完了したことを環境に通知する必要があります。 プロジェクトでは、親ファイルだけでなくすべてのファイル (たとえば、特殊なファイル) に対して、<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> インターフェイスのメソッドを呼び出す必要があります。 ファイル呼び出しは必須ですが、ディレクトリ呼び出しは省略可能です。 プロジェクトにディレクトリの情報がある場合は、適切な <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> メソッドが呼び出されますが、この情報がない場合は、環境によってディレクトリの情報が推測されます。

 プロジェクトでは、プロジェクトのオープンまたはクローズ時に `IVsTrackProjectDocuments2` のメソッドを呼び出してはなりません。 起動時にこの情報が必要なリスナーは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenSolution%2A> イベントを待機し、ソリューションを反復処理して必要な情報を見つけることができます。 シャットダウン時には、この情報は必要ありません。 `IVsTrackProjectDocuments2` は <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments> から提供されます。

 追加、名前変更、削除の各操作には、`OnQuery*` メソッドと `OnAfter*` メソッドがあります。 ファイルまたはディレクトリを追加、名前変更、または削除するためのアクセス許可を要求するには、`OnQuery*` メソッドを呼び出します。 `OnAfter*` メソッドは、ファイルまたはディレクトリが追加、名前変更、または削除された後に呼び出します。これにより、プロジェクトの状態に新しい状態が反映されます。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>
- [ソース管理のサポート](../../extensibility/internals/supporting-source-control.md)
