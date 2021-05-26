---
title: カスタム エディターとデザイナーの作成 | Microsoft Docs
description: Visual Studio IDE でホストできるさまざまな種類のエディター (コア エディター、カスタム エディター、外部エディター、デザイナー) について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- designers [Visual Studio SDK]
- editors [Visual Studio SDK], custom
ms.assetid: b6a5e8b2-0ae1-4fc3-812d-09d40051b435
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c2882cfa103627672e5c96a0e3d4b2a23b4b4ba9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055779"
---
# <a name="create-custom-editors-and-designers"></a>カスタム エディターとデザイナーを作成する

Visual Studio 統合開発環境 (IDE) では、さまざまな種類のエディターをホストできます。

- Visual Studio のコア エディター

- カスタム エディター

- 外部エディター

- デザイナー

次の情報は、必要なエディターの種類を選択する場合に役立ちます。

## <a name="types-of-editor"></a>エディターの種類

Visual Studio のコア エディターの詳細については、「[エディターと言語サービスを拡張する](../extensibility/extending-the-editor-and-language-services.md)」をご覧ください。

### <a name="custom-editors"></a>カスタム エディター
 カスタム エディターとは、特殊な環境で動作するように設計されたものです。 たとえば、Microsoft Exchange サーバー などの特定のリポジトリに対してデータの読み取りや書き込みを行う機能を持つエディターを作成できます。 プロジェクト タイプのみを扱うエディターが必要な場合、または特定のいくつかのコマンドのみを含むエディターが必要な場合は、カスタム エディターを選択してください。 ただし、ユーザーはカスタム エディターを使用して標準の [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロジェクトを編集できないので注意してください。

 カスタム エディターでは、エディターファクトリを使用して、エディターに関する情報をレジストリに追加できます。 ただし、カスタム エディターに関連付けられているプロジェクト タイプでは、他の方法でカスタム エディターをインスタンス化できます。

 カスタム エディターでは、インプレース アクティブ化または簡略化された埋め込みを使用して、ビューを実装できます。

### <a name="external-editors"></a>外部エディター
 外部エディターとは、Microsoft Word、メモ帳、Microsoft FrontPage など、Visual Studio に組み込まれていないエディターです。 たとえば、VSPackage からテキストを渡す場合に、このようなエディターを呼び出すことができます。 外部エディターは、それ自体を登録しておくと、Visual Studio の外部で使用できます。 外部エディターを呼び出し、それをホスト ウィンドウに埋め込むことができる場合は、IDE のウィンドウに表示されます。 そうでない場合、IDE によってそれに代わる別のウィンドウが作成されます。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> メソッドでは、<xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> 列挙型を使用してドキュメントの優先度を設定します。 `DP_External` 値を指定した場合は、外部エディターでファイルを開くことができます。

## <a name="editor-design-decisions"></a>エディターの設計上の決定事項
 設計に関する次の質問は、お客様のアプリケーションに最適なエディターの種類を選択する場合に役立ちます。

- お客様のアプリケーションのデータはファイルに保存されますか、それともされませんか? そのデータがファイルに保存される場合、それらはカスタム形式ですか、それとも標準形式ですか?

   標準のファイル形式を使用する場合は、お客様のプロジェクトに加えて他のプロジェクト タイプでも、ファイルを開いたり、データの読み取り/書き込みを行ったりすることができます。 一方、カスタムのファイル形式を使用する場合は、お客様のプロジェクト タイプでのみ、ファイルを開いたり、データの読み取り/書き込みを行ったりすることができます。

   プロジェクトでファイルを使用する場合は、標準のエディターをカスタマイズする必要があります。 プロジェクトでファイルではなく、データベースまたは他のリポジトリ内の項目を使用する場合は、カスタム エディターを作成する必要があります。

- お使いのエディターで ActiveX コントロールをホストする必要がありますか?

   エディターで ActiveX コントロールをホストする場合は、[インプレース アクティブ化](/previous-versions/visualstudio/visual-studio-2015/misc/in-place-activation?preserve-view=true&view=vs-2015)に関するページで説明されているように、インプレース アクティブ化エディターを実装します。 ActiveX コントロールをホストしない場合は、簡略化された埋め込みエディターを使用するか、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の既定のエディターをカスタマイズします。

- お使いのエディターで複数のビューをサポートしますか? お使いのエディターのビューを既定のエディターと同時に表示する場合は、複数のビューをサポートする必要があります。

   お使いのエディターで複数のビューをサポートする必要がある場合は、エディターのドキュメント データ オブジェクトとドキュメント ビューオブジェクトを別々のオブジェクトにする必要があります。 詳細については、「[複数のドキュメント ビューのサポート](../extensibility/supporting-multiple-document-views.md)」をご覧ください。

   お使いのエディターで複数のビューをサポートする場合、ドキュメント データ オブジェクトに [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] コア エディターのテキスト バッファー実装 (<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> オブジェクト) を使用する予定ですか? つまり、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] コア エディターとのエディター ビューの side-by-side 実行をサポートしますか? これを行う機能は、フォーム デザイナーの原点です。

- 外部エディターをホストする必要がある場合は、そのエディターを [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の内部に埋め込むことができますか?

   それを埋め込むことができる場合は、外部エディター用のホスト ウィンドウを作成した後、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> メソッドを呼び出して、<xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> 列挙型値を `DP_External` に設定する必要があり ます。 エディターを埋め込むことができない場合は、IDE によってそれに代わる別のウィンドウが自動的に作成されます。

## <a name="in-this-section"></a>このセクションの内容

[チュートリアル: カスタム エディターを作成する](../extensibility/walkthrough-creating-a-custom-editor.md)\
カスタム エディターを作成する方法について説明します。

[チュートリアル: カスタム エディターに機能を追加する](../extensibility/walkthrough-adding-features-to-a-custom-editor.md)\
カスタム エディターに機能を追加する方法について説明します。

[デザイナーの初期化とメタデータの構成](../extensibility/designer-initialization-and-metadata-configuration.md)\
デザイナーを初期化する方法について説明します。

[デザイナー向けの元に戻す操作のサポートを提供する](../extensibility/supplying-undo-support-to-designers.md)\
デザイナー向けの元に戻す操作を提供する方法について説明します。

[カスタム エディターでの構文の色分け表示](../extensibility/syntax-coloring-in-custom-editors.md)\
コア エディターとカスタム エディターでの構文の色分け表示の違いについて説明します。

[カスタム エディターでのドキュメント データとドキュメント ビュー](../extensibility/document-data-and-document-view-in-custom-editors.md)\
カスタム エディターでドキュメント データとドキュメント ビューを実装する方法について説明します。

## <a name="related-sections"></a>関連項目

[エディターのレガシ インターフェイス](/previous-versions/visualstudio/visual-studio-2015/extensibility/legacy-interfaces-in-the-editor?preserve-view=true&view=vs-2015)\
レガシ API を使用してコア エディターにアクセスする方法について説明します。

[従来の言語サービスを開発する](../extensibility/internals/developing-a-legacy-language-service.md)\
言語サービスを実装する方法について説明します。

[Visual Studio の他の部分を拡張する](../extensibility/extending-other-parts-of-visual-studio.md)\
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の他の部分に相当する UI 要素を作成する方法について説明します。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>
