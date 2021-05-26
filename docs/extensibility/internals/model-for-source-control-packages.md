---
title: ソース管理パッケージのモデル |Microsoft Docs
description: このモデルは、ソース管理の実装を表します。 この記事では、ソース管理の実行方法を理解しやすくするために、クラスの名前を示しています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], model
ms.assetid: 6164b2d3-a622-4de8-bef3-a6de985e9ebd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e4e437afdfa0d3de03da6814e221840cbd0763fd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063202"
---
# <a name="model-for-source-control-packages"></a>ソース管理パッケージのモデル
次のモデルは、ソース管理の実装例を表しています。 モデルには、実装する必要があるインターフェイスと、呼び出す必要がある環境サービスが示されています。 すべてのサービスと同様に、実際には、サービスを経由して取得する特定のインターフェイスのメソッドを呼び出します。 ソース管理の実行方法を理解しやすくするために、クラスの名前を識別しています。

 ![SCC&#95;TUP の例](../../extensibility/internals/media/scc_tup.gif "SCC_TUP") ソース管理プロジェクトの例

## <a name="interfaces"></a>インターフェイス
 次の表に示すインターフェイスの一覧を使用して、Visual Studio で新しいプロジェクト タイプのソース管理を実装できます。

|インターフェイス|用途|
|---------------|---------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>|ファイル (ダーティ) を保存または変更する前に、プロジェクトおよびエディターによって呼び出されます。 このインターフェイスには、<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> サービスを使用してアクセスします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>|ファイルまたはディレクトリの追加、削除、または名前変更を行うためのアクセス許可を要求するために、プロジェクトによって呼び出されます。 このインターフェイスは、承認された追加、削除、または名前変更のアクションが完了したことを環境に通知するために、プロジェクトによっても呼び出されます。 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments> サービスを使用してアクセスします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>|プロジェクトがファイルまたはディレクトリを追加、名前変更、または削除したときに通知を受け取るように登録する任意のエンティティによって実装されます。 イベント通知に登録するには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2.AdviseTrackProjectDocumentsEvents%2A> を呼び出します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>|ソース管理パッケージに登録し、ソース管理の状態に関する情報を取得するために、プロジェクトによって呼び出されます。 このインターフェイスには、<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager> サービスを使用してアクセスします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>|ファイルに関する情報のソース管理要求に応答し、プロジェクト ファイルに必要なソース管理設定を取得するために、プロジェクトによって実装されます。|

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2.AdviseTrackProjectDocumentsEvents%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>
- [ソース管理のサポート](../../extensibility/internals/supporting-source-control.md)
