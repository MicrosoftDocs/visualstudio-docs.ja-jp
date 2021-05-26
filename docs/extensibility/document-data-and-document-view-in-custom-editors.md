---
title: カスタム エディターでのドキュメント データとドキュメント ビュー | Microsoft Docs
description: カスタムエディターのコンポーネント (ドキュメント データ オブジェクトとドキュメント ビュー オブジェクト) について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - document data and document view
ms.assetid: 71eea623-f566-4feb-84cd-ca1ba71bc493
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 391bec513f1f6d32d7ff2f87d70abdbf491ab8be
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091241"
---
# <a name="document-data-and-document-view-in-custom-editors"></a>ドキュメント データとドキュメント ビュー
カスタム エディターは、ドキュメント データオブジェクトとドキュメント ビュー オブジェクトの 2 つの部分から構成されます。 名前が示すように、ドキュメント データ オブジェクトは、表示される適すとデータを表します。 同様に、ドキュメント ビュー オブジェクト (または "ビュー") は、ドキュメント データ オブジェクトを表示する 1 つ以上のウィンドウを表します。

## <a name="document-data-object"></a>ドキュメント データ オブジェクト
 ドキュメント データ オブジェクトは、テキスト バッファー内のテキストのデータ表現です。 これは、ドキュメント テキストやその他の情報を格納する COM オブジェクトです。 また、ドキュメント データ オブジェクトは、ドキュメントの永続化を処理し、データの複数のビューを有効にします。 詳細については、「

 <xref:EnvDTE80.Window2.DocumentData%2A>」と「[ドキュメント ウィンドウ](../extensibility/internals/document-windows.md)」を参照してください。

 カスタム エディターとデザイナーでは、<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> オブジェクトを使用するか、独自のカスタム バッファーを使用するかを選択できます。 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> では、標準エディターの簡略化された埋め込みモデルに従い、複数のビューをサポートし、複数のビューを管理するために使用されるイベント インターフェイスを提供します。

## <a name="document-view-object"></a>ドキュメント ビュー オブジェクト
 コードやその他のテキストを表示するウィンドウは、ドキュメント ビューまたはビューと呼ばれます。 エディターを作成するときに、単一のウィンドウにテキストを表示する単一ビューを選択することも、 複数のウィンドウにテキストを表示する複数ビューを選択することもできます。 どれを選択するかは用途によって異なります。 たとえば、サイドバイサイド編集が必要な場合は、複数ビューを選択します。 それぞれのビューは、統合開発環境 (IDE) の実行中のドキュメント テーブル (RDT) におけるエントリに関連付けられています。 ビュー ウィンドウは、プロジェクトまたは <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> オブジェクトに属しています。

 エディターが複数ビューのドキュメント データ オブジェクトをサポートしている場合は、ドキュメント データ オブジェクトとドキュメント ビュー オブジェクトが分かれている必要があります。 それ以外の場合は、これらは一緒にグループ化できます。 詳細については、「[複数のドキュメント ビューのサポート](../extensibility/supporting-multiple-document-views.md)」をご覧ください。

 IDE では、実行中のドキュメント テーブル内のエントリごとに項目識別子 (ItemID) を照合して、イベント (たとえば、ドキュメントを含むソリューションが閉じられたとき) に関するビューを通知します。 詳細については、「[ドキュメント テーブルの実行](../extensibility/internals/running-document-table.md)」を参照してください。

 カスタム エディター用のビューを作成するオプションは 2 つあります。 1 つ目はインプレース アクティブ化モデルで、ここでは ActiveX コントロールかドキュメント データ オブジェクトのどちらかを使用して、ビューがウィンドウでホストされます。 2 つ目は、簡略化された埋め込みモデルで、ここではビューが [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] でホストされ、ウィンドウ コマンドを処理するために <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> が実装されます。 インプレース アクティブ化モデルの詳細については、[インプレース アクティブ化](/previous-versions/visualstudio/visual-studio-2015/misc/in-place-activation?preserve-view=true&view=vs-2015)に関するページを参照してください。 簡略化された埋め込みモデルの詳細については、[簡略化された埋め込み](../extensibility/simplified-embedding.md)に関するページを参照してください。

## <a name="see-also"></a>関連項目

- [複数のドキュメント ビューのサポート](../extensibility/supporting-multiple-document-views.md)
- [簡略化された埋め込み](../extensibility/simplified-embedding.md)
- [方法: ビューをドキュメントデータに添付する](../extensibility/how-to-attach-views-to-document-data.md)
- [ドキュメント ロック ホルダーの管理](../extensibility/document-lock-holder-management.md)
- [単一タブと複数タブのビュー](../extensibility/single-and-multi-tab-views.md)
- [標準ドキュメントの保存](../extensibility/internals/saving-a-standard-document.md)
- [永続性と実行中のドキュメント テーブル](../extensibility/internals/persistence-and-the-running-document-table.md)
- [プロジェクト内のファイルを開くエディターを決定する](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)