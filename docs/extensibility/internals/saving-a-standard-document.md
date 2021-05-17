---
title: 標準ドキュメントの保存 |Microsoft Docs
description: Visual Studio IDE に追加するプロジェクトの種類の標準ドキュメントに対して発生するプロセスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], saving standard documents
- projects [Visual Studio SDK], saving standard documents
- persistence, saving standard documents
ms.assetid: d692fedf-b46e-4d60-84bd-578635042235
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a1864ec689c1068b97775ca1a8bddbd390e7b43a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080893"
---
# <a name="saving-a-standard-document"></a>標準ドキュメントの保存
環境では、[保存]、[名前を付けて保存]、[すべてを保存] コマンドが処理されます。 ユーザーが **[ファイル]** メニューの **[保存]** 、 **[名前を付けて保存]** 、または **[すべて保存]** を選択するか、ソリューションを閉じると、 **[すべて保存]** が行われ、次のプロセスが実行されます。

 ![標準エディター](../../extensibility/internals/media/public.gif "パブリック") 標準エディターの [保存]、[名前を付けて保存]、[すべて保存] コマンドの処理

 このプロセスについては次の手順で詳細に説明します。

1. **[保存]** および **[名前を付けて保存]** コマンドを選択すると、環境では <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> サービスを使用して、アクティブなドキュメント ウィンドウと、保存する必要がある項目が決定されます。 アクティブなドキュメント ウィンドウが判明すると、環境では、実行中のドキュメント テーブル内のドキュメントの階層ポインターと項目識別子 (itemID) が検索されます。 詳細については、「[実行中のドキュメント テーブル](../../extensibility/internals/running-document-table.md)」を参照してください。

    **[すべて保存]** コマンドを選択すると、環境では実行中のドキュメント テーブルの情報を使用して、保存するすべての項目の一覧がコンパイルされます。

2. ソリューションでは <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 呼び出しを受け取ると、選択された一連の項目 (つまり、<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> サービスによって公開される複数の選択項目) を反復処理します。

3. ソリューションで、選択項目の各項目に対して、階層ポインターを使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IsItemDirty%2A> メソッドが呼び出され、 **[保存]** メニュー コマンドを有効にする必要があるかどうかが判断されます。 1 つ以上の項目がダーティの場合、 **[保存]** コマンドが有効になります。 階層で標準のエディターが使用されている場合、階層では <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.IsDocDataDirty%2A> メソッドを呼び出して、ダーティ状態のクエリをエディターに委任します。

4. 選択された各項目がダーティである場合、ソリューションでは階層ポインターを使用して、適切な階層で <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A> メソッドを呼び出します。

    階層では、標準のエディターを使用してドキュメントを編集するのが一般的です。 この場合、そのエディターのドキュメント データ オブジェクトでは <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> インターフェイスがサポートされている必要があります。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A> メソッド呼び出しを受け取った時点で、ドキュメント データ オブジェクトの <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.SaveDocData%2A> メソッドを呼び出すことによって、ドキュメントが保存されていることをエディターに通知する必要があります。 エディターでは、<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> インターフェイスに対して `Query Service` を呼び出すことで、環境で **[名前を付けて保存]** ダイアログ ボックスを処理できます。 これで、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> インターフェイスへのポインターが返されます。 次に、エディターでは <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A> メソッドを呼び出し、`pPersistFile` パラメーターを使ってエディターの <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> 実装へのポインターを渡す必要があります。 その後、環境で保存操作が実行され、エディターの **[名前を付けて保存]** ダイアログ ボックスが表示されます。 次に、環境では、<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> を使用してエディターにコールバックします。

5. ユーザーが無題のドキュメント (つまり、以前に保存されていないドキュメント) を保存しようとすると、[名前を付けて保存] コマンドが実際に実行されます。

6. [名前を付けて保存] コマンドでは、環境に [名前を付けて保存] ダイアログ ボックスが表示され、ユーザーはファイル名を入力するように求められます。

    ファイルの名前が変更されている場合、階層では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.SetProperty%2A>(VSFPROPID_MkDocument) を呼び出して、ドキュメント フレームのキャッシュされた情報を更新する必要があります。

   **[名前を付けて保存]** コマンドを使用してドキュメントの場所を移動した場合、階層がドキュメントの場所の影響を受けるときは、階層で、開いているドキュメント ウィンドウの所有権を別の階層に渡す必要があります。 たとえば、ファイルがプロジェクトに関連する内部または外部のファイル (その他のファイル) であるかどうかがプロジェクトによって追跡される場合にこれが発生します。 ファイルの所有権をその他のファイル プロジェクトに変更するには、次の手順を使用します。

## <a name="changing-file-ownership"></a>ファイル所有権の変更

#### <a name="to-change-file-ownership-to-the-miscellaneous-files-project"></a>ファイル所有権をその他のファイル プロジェクトに変更するには

1. <xref:Microsoft.VisualStudio.Shell.Interop.SVsExternalFilesManager> インターフェイスのサービスのクエリを実行します。

     <xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager2> へのポインターが返されます。

2. ドキュメントを新しい階層に転送するには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager2.TransferDocument%2A> (`pszMkDocumentNew`, `punkWindowFrame`) メソッドを呼び出します。 [名前を付けて保存] コマンドを実行する階層では、このメソッドが呼び出されます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [プロジェクト項目のオープンと保存](../../extensibility/internals/opening-and-saving-project-items.md)
