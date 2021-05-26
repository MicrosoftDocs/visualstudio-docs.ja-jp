---
title: '方法: 標準エディターを開く | Microsoft Docs'
description: 標準エディターを使用して OpenItem メソッドを実装する方法について説明します。 IDE では、指定されたファイルの種類に合わせて標準エディターが決定されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], opening
- projects [Visual Studio SDK], opening standard editors
ms.assetid: d5ce10f9-047a-4b74-aa1d-295128898b89
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1b0de198e96ff268a0744a4a97a4a160c585af9c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069908"
---
# <a name="how-to-open-standard-editors"></a>方法: 標準エディターを開く
標準エディターを開くときは、指定されたファイルの種類に対して、プロジェクト固有のエディターを指定するのではなく、IDE で標準エディターが決定されます。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> メソッドを実装するには、次の手順を完了します。 これにより、標準エディターでプロジェクト ファイルが開きます。

## <a name="to-implement-the-openitem-method-with-a-standard-editor"></a>標準エディターを使用して OpenItem メソッドを実装するには

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> (`RDT_EditLock`) を呼び出して、ドキュメント データ オブジェクト ファイルが既に開いているかどうかを判断します。

2. ファイルが既に開いている場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> メソッドを呼び出して `grfIDO` パラメーターに `IDO_ActivateIfOpen` の値を指定して、ファイルを再表示します。

     ファイルが開いていて、ドキュメントが呼び出し元プロジェクトとは異なるプロジェクトによって所有されている場合、プロジェクトには、開いているエディターが別のプロジェクトのものであることを示す警告が表示されます。 次に、ファイル ウィンドウが表示されます。

3. ドキュメントが開いていない場合、または実行中のドキュメント テーブルにない場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> メソッド (`OSE_ChooseBestStdEditor`) を呼び出して、ファイルの標準エディターを開きます。

     メソッドを呼び出すと、IDE では次のタスクを実行します。

    1. IDE では、Editors/{guidEditorType}/Extensions サブキーをスキャンして、ファイルを開くことができるエディターのうち、この実行に最も高い優先順位を持つものを特定します。

    2. ファイルを開くことができるエディターが特定されると、IDE では <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> を呼び出します。 エディターでのこのメソッドの実装では、IDE で <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A> を呼び出して新しく開いたドキュメントをサイト設定するために必要な情報を返します。

    3. 最後に、IDE では通常の永続化インターフェイス (<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> など) を使用してドキュメントを読み込みます。

    4. 以前に IDE で階層または階層項目が使用可能であると判断されている場合、IDE ではプロジェクトで <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.GetItemContext%2A> メソッドを呼び出して、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A> メソッド呼び出しで渡し返すプロジェクトレベルのコンテキスト <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> ポインターを取得します。

4. エディターでプロジェクトからコンテキストを取得できるようにする場合は、IDE で <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.GetItemContext%2A> をプロジェクトで呼び出すと、<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> へのポインターが IDE に返されます。

     この手順を実行すると、プロジェクトではエディターに追加のサービスを提供できます。

     ドキュメント ビューまたはドキュメント ビュー オブジェクトがウィンドウ フレームで正常にサイト設定されている場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.LoadDocData%2A> を呼び出すことによって、オブジェクトがそのデータで初期化されます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>
- [プロジェクト項目を開いて保存する](../extensibility/internals/opening-and-saving-project-items.md)
- [方法: プロジェクト固有のエディターを開く](../extensibility/how-to-open-project-specific-editors.md)
- [方法: 開いているドキュメントのエディターを開く](../extensibility/how-to-open-editors-for-open-documents.md)
- [[プログラムから開く] コマンドを使用してファイルを表示する](../extensibility/internals/displaying-files-by-using-the-open-file-command.md)
