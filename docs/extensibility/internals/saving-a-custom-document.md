---
title: カスタム ドキュメントの保存 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- persistence, saving custom documents
- projects [Visual Studio SDK], saving custom documents
- editors [Visual Studio SDK], saving custom documents
ms.assetid: 040b36d6-1f0a-4579-971c-40fbb46ade1d
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0f02c4a98920fc575b5ab7c557dd469deb76a586
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63427465"
---
# <a name="saving-a-custom-document"></a>カスタム ドキュメントの保存
環境ハンドル、**保存**、**名前を付けて保存**、および**すべて保存**コマンド。 ユーザーがクリックすると**保存**、**名前を付けて保存**、**すべてを保存または**上、**ファイル**メニューまたはすべてを保存、次に、ソリューションを閉じる処理が行われます。

 ![カスタマー エディター保存](../../extensibility/internals/media/private.gif "プライベート")保存、名前を付けて保存および処理のカスタム エディターをすべて保存 コマンド

 このプロセスの詳細については、次の手順。

1. **保存**と**名前を付けて保存**、環境を使用して、コマンド、<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>サービスのアクティブなドキュメント ウィンドウを確認して、どのような項目を保存するためです。 アクティブなドキュメント ウィンドウがわかったら、環境は、実行中の document テーブル内のドキュメントの階層のポインターと項目の識別子 (itemID) を検索します。 詳細については、次を参照してください。[を実行しているドキュメント テーブル](../../extensibility/internals/running-document-table.md)します。

     すべて保存 コマンドは、環境は、保存するのにすべての項目の一覧をコンパイルするのに、実行中の document テーブルの情報を使用します。

2. ソリューションが受信すると、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>呼び出し、選択した項目のセットを反復処理 (によって公開されている複数の選択は、<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>サービス)。

3. ソリューションの選択範囲の各項目を呼び出す階層ポインターを使用して、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IsItemDirty%2A>メソッドを上書き保存 メニュー コマンドを有効にするかどうかを判断します。 1 つまたは複数の項目がダーティの場合は、[保存] コマンドが有効にします。 階層は、標準のエディターを使用している場合のクエリを実行する階層デリゲート ダーティ状態、エディターを呼び出すことによって、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.IsDocDataDirty%2A>メソッド。

4. ソリューションがダーティ選択項目ごとに呼び出す階層ポインターを使用して、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A>メソッドを適切な階層。

     カスタム エディターでは、場合は、ドキュメント データ オブジェクトと、プロジェクト間の通信はプライベートです。 したがって、任意の特殊な永続化の問題は、これら 2 つのオブジェクトの間で処理されます。

    > [!NOTE]
    > 独自の永続化を実装する場合を呼び出すことを確認する、<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>時間を節約するメソッド。 このメソッドは、ファイルを保存しても安全であるかどうかを確認するチェック (たとえば、ファイルは読み取り専用)。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [プロジェクト項目のオープンと保存](../../extensibility/internals/opening-and-saving-project-items.md)