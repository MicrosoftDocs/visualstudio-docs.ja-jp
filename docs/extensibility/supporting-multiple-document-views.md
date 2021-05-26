---
title: 複数のドキュメント ビューのサポート | Microsoft Docs
description: Visual Studio SDK でカスタム エディターに個別のドキュメント データとドキュメント ビュー オブジェクトを使用して、ドキュメントの複数のビューを提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - multiple document views
ms.assetid: c7ec2366-91c4-477f-908d-e89068bdb3e3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e54ee028c6a7db2d5d2ea1ab609be6c2887c9829
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056208"
---
# <a name="supporting-multiple-document-views"></a>複数のドキュメント ビューのサポート
お使いのエディター用に個別のドキュメント データとドキュメント ビュー オブジェクトを作成して、ドキュメントの複数のビューを提供することができます。 以下の場合に、追加のドキュメント ビューが役に立ちます。

- 新しいウィンドウのサポート: お使いのエディターで同じ種類の複数のビューを提供する必要があります。そのため、エディターで既にウィンドウを開いているユーザーが、 **[ウィンドウ]** メニューから **[新しいウィンドウ]** コマンドを選択して新しいウィンドウを開くことができるようにします。

- フォームおよびコード ビューのサポート: お使いのエディターでさまざまな種類のビューを提供する必要があります。 たとえば、[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] にはフォーム ビューとコード ビューの両方が表示されます。

  詳細については、Visual Studio パッケージ テンプレートによって作成されたカスタム エディター プロジェクトの EditorFactory.cs ファイルにある CreateEditorInstance プロシージャをご覧ください。 このプロジェクトの詳細については、「[チュートリアル: カスタム エディターを作成する](../extensibility/walkthrough-creating-a-custom-editor.md)」をご覧ください。

## <a name="synchronizing-views"></a>ビューの同期
 複数のビューを実装する場合は、ドキュメント データ オブジェクトによって、すべてのビューが常にデータと同期されます。 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 上のイベント処理インターフェイスを使用すると、複数のビューをデータと同期させることができます。

 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> オブジェクトを使用せずに複数のビューを同期させる場合は、ドキュメント データ オブジェクトに加えられた変更を処理する独自のイベント システムを実装する必要があります。 さまざまな粒度レベルを使用して、複数のビューを最新の状態に保つことができます。 最大粒度の設定では、1 つのビューを入力すると、他のビューがすぐに更新されます。 最小粒度では、他のビューはアクティブ化されるまで更新されません。

## <a name="determining-whether-document-data-is-already-open"></a>ドキュメント データが既に開いているかどうかの確認
 次の図に示すように、統合開発環境 (IDE) の実行中のドキュメント テーブル (RDT) を使用すると、ドキュメントのデータが既に開いているかどうかを追跡できます。

 ![DocDataView の図](../extensibility/media/docdataview.gif "Docdataview") 複数のビュー

 既定では、各ビュー (ドキュメント ビュー オブジェクト) は独自のウィンドウ フレーム (<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>) に格納されています。 ただし、既に説明したように、ドキュメント データは複数のビューに表示できます。 これを有効にするために、Visual Studio では RDT を調べて、問題になっているドキュメントが既にエディターで開かれているかどうかを確認します。 IDE でエディターを作成するために <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> を呼び出した場合、`punkDocDataExisting` パラメーターで NULL 以外の値が返されると、ドキュメントは既に別のエディターで開かれていることになります。 RDT 機能の詳細については、「[実行中のドキュメント テーブル](../extensibility/internals/running-document-table.md)」をご覧ください。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> の実装では、`punkDocDataExisting` で返されたドキュメント データ オブジェクトを調べて、ドキュメント データがお使いのエディターに適しているかどうかを判断します (たとえば、HTML エディターで表示されるのは HTML データだけです)。それが適切な場合、エディター ファクトリによってデータの 2 つ目のビューが提供されます。 `punkDocDataExisting` パラメーターが `NULL` でない場合は、ドキュメント データ オブジェクトが別のエディターで開かれている可能性があります。あるいは、ドキュメント データが同じエディターを持つ別のビューで既に開かれている可能性が高くなります。 エディター ファクトリでサポートされていない別のエディターでドキュメント データが開かれている場合、Visual Studio ではエディター ファクトリを開くことができません。 詳細については、「[方法: ビューをドキュメントデータに添付する](../extensibility/how-to-attach-views-to-document-data.md)」をご覧ください。
