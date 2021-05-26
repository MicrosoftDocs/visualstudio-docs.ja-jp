---
title: '方法: プロジェクト固有のエディターを開く | Microsoft Docs'
description: プロジェクト固有のエディターを使用して OpenItem メソッドを実装する方法について説明します。これにより、プロジェクトでは、そのプロジェクト用のエディターにバインドされたファイルを開くことができます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- project types, opening a project-specific editor
- editors [Visual Studio SDK], opening project-specific editors
- projects [Visual Studio SDK], opening folders
ms.assetid: 83e56d39-c97b-4c6b-86d6-3ffbec97e8d1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b8fa68ff628212a207f860a3f9e6eca960481ee9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069882"
---
# <a name="how-to-open-project-specific-editors"></a>方法: プロジェクト固有のエディターを開く
プロジェクトによって開かれている項目ファイルが、そのプロジェクト用の特定のエディターに本質的にバインドされている場合、プロジェクトでは、プロジェクト固有のエディターを使用してファイルを開く必要があります。 エディターを選択するための IDE のメカニズムへファイルを委任することはできません。 たとえば、標準のビットマップ エディターを使用する代わりに、このプロジェクト固有のエディター オプションを使用して、プロジェクトに固有のファイル内にある情報を認識する特定のビットマップ エディターを指定できます。

 IDE では、特定のプロジェクトでファイルを開く必要があると判断したときに、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> メソッドを呼び出します。 詳細については、「[[ファイルを開く] コマンドを使用してファイルを表示する](../extensibility/internals/displaying-files-by-using-the-open-file-command.md)」を参照してください。 次のガイドラインを利用して、 プロジェクト固有のエディターを使用してプロジェクトでファイルを開くための `OpenItem` メソッドを実装します。

## <a name="to-implement-the-openitem-method-with-a-project-specific-editor"></a>プロジェクト固有のエディターを使用して OpenItem メソッドを実装するには

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A> メソッド (`RDT_EditLock`) を呼び出して、ファイル (ドキュメント データ オブジェクト) が既に開いているかどうかを確認します。

    > [!NOTE]
    > ドキュメント データとドキュメント ビュー オブジェクトの詳細については、「[カスタム エディターでのドキュメント データとドキュメント ビュー](../extensibility/document-data-and-document-view-in-custom-editors.md)」を参照してください。

2. ファイルが既に開いている場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> メソッドを呼び出して `grfIDO` パラメーターに IDO_ActivateIfOpen の値を指定して、ファイルを再表示します。

     ファイルが開いていて、ドキュメントが呼び出し元プロジェクト以外のプロジェクトによって所有されている場合は、開いているエディターが別のプロジェクトのものであることを示す警告がユーザーに表示されます。 次に、ファイル ウィンドウが表示されます。

3. テキスト バッファー (ドキュメント データ オブジェクト) が既に開いていて、別のビューをアタッチする場合は、自分でそのビューをフックする必要があります。 プロジェクトからビュー (ドキュメント ビュー オブジェクト) をインスタンス化する場合に推奨される方法は次のとおりです。

    1. <xref:Microsoft.VisualStudio.Shell.Interop.SLocalRegistry> サービスで `QueryService` を呼び出して、<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2> インターフェイスへのポインターを取得します。

    2. <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> メソッドを呼び出して、ドキュメント ビュー クラスのインスタンスを作成します。

4. <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A> メソッドを呼び出して、ドキュメント ビュー オブジェクトを指定します。

     このメソッドは、ドキュメント ウィンドウ内のドキュメント ビュー オブジェクトをサイト設定します。

5. <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.InitNew%2A> または <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.Load%2A> メソッドへの適切な呼び出しを実行します。

     この時点で、ビューは完全に初期化され、開く準備ができています。

6. <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> メソッドを呼び出して、ビューを表示して開きます。

## <a name="see-also"></a>関連項目
- [プロジェクト項目を開いて保存する](../extensibility/internals/opening-and-saving-project-items.md)
- [方法: 標準エディターを開く](../extensibility/how-to-open-standard-editors.md)
- [方法: 開いているドキュメントのエディターを開く](../extensibility/how-to-open-editors-for-open-documents.md)
