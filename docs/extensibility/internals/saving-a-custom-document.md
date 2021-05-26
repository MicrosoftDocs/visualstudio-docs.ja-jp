---
title: カスタム ドキュメントの保存 | Microsoft Docs
description: Visual Studio IDE に追加するプロジェクト タイプのカスタム ドキュメントに対して発生するプロセスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- persistence, saving custom documents
- projects [Visual Studio SDK], saving custom documents
- editors [Visual Studio SDK], saving custom documents
ms.assetid: 040b36d6-1f0a-4579-971c-40fbb46ade1d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a536a5f0f2b1cac09c65079974c661e09e9139ab
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080919"
---
# <a name="saving-a-custom-document"></a>カスタム ドキュメントの保存
環境では、 **[保存]** 、 **[名前を付けて保存]** 、 **[すべてを保存]** コマンドが処理されます。 ユーザーが **[ファイル]** メニューの **[保存]** 、 **[名前を付けて保存]** 、または **[すべて保存]** をクリックすると、[すべて保存] が行われ、次のプロセスが実行されます。

 ![カスタマー エディター保存](../../extensibility/internals/media/private.gif "プライベート") カスタム エディターの [保存]、[名前を付けて保存]、[すべて保存] コマンドの処理

 このプロセスについては次の手順で詳細に説明します。

1. **[保存]** および **[名前を付けて保存]** コマンドの場合、環境では <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> サービスを使用して、アクティブなドキュメント ウィンドウと、保存する必要がある項目が決定されます。 アクティブなドキュメント ウィンドウが判明すると、環境では、実行中のドキュメント テーブル内のドキュメントの階層ポインターと項目識別子 (itemID) が検索されます。 詳細については、「[実行中のドキュメント テーブル](../../extensibility/internals/running-document-table.md)」を参照してください。

     [すべて保存] コマンドの場合、環境では実行中のドキュメント テーブルの情報を使用して、保存するすべての項目の一覧がコンパイルされます。

2. ソリューションでは <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 呼び出しを受け取ると、選択された一連の項目 (つまり、<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> サービスによって公開される複数の選択項目) を反復処理します。

3. ソリューションで、選択項目の各項目に対して、階層ポインターを使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IsItemDirty%2A> メソッドが呼び出され、[保存] メニュー コマンドを有効にする必要があるかどうかが判断されます。 1 つ以上の項目がダーティの場合、[保存] コマンドが有効になります。 階層で標準のエディターが使用されている場合、階層では <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.IsDocDataDirty%2A> メソッドを呼び出して、ダーティ状態のクエリをエディターに委任します。

4. 選択された各項目がダーティである場合、ソリューションでは階層ポインターを使用して、適切な階層で <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A> メソッドを呼び出します。

     カスタム エディターの場合、ドキュメント データ オブジェクトとプロジェクトの間の通信はプライベートになります。 したがって、永続化に関する特別な問題がある場合は、この 2 つのオブジェクトの間で処理されます。

    > [!NOTE]
    > 独自の永続性を実装する場合は、時間を節約するために必ず <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A> メソッドを呼び出してしてください。 このメソッドは、ファイルを保存しても安全かどうか (たとえば、ファイルが読み取り専用ではないこと) を確認します。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [プロジェクト項目のオープンと保存](../../extensibility/internals/opening-and-saving-project-items.md)
