---
title: エディターと言語サービスの拡張 | Microsoft Docs
description: 言語サービス機能をエディターに追加し、Visual Studio コード エディターの機能を拡張することができます。 Managed Extensibility Framework について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new -
ms.assetid: 8d04f8db-eda7-4b3e-b6eb-c06df104502a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8d85b018b4e0ea7d5ed1c91e617afcb2759d49b8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070116"
---
# <a name="extend-the-editor-and-language-services"></a>エディターと言語サービスを拡張する
言語サービス機能 (IntelliSense) などを独自のエディターに追加し、Visual Studio コード エディターのほとんどの機能を拡張することができます。  拡張できるものの完全な一覧については、「[言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)」を参照してください。

 ほとんどのエディター機能は、Managed Extensibility Framework (MEF) を使用して拡張します。 たとえば、拡張するエディター機能が構文の色分け表示である場合は、異なる色分け表示を必要とする分類とその処理方法を定義する MEF *コンポーネント パーツ* を記述できます。 エディターでは、同じ機能の複数の拡張機能もサポートされています。

 エディターのプレゼンテーション レイヤーは、Windows Presentation Framework (WPF) に基づいています。 WPF には柔軟なテキスト書式設定用のグラフィックス ライブラリが用意されています。また、グラフィックスやアニメーションなどの視覚エフェクトも用意されています。

 Visual Studio SDK には、以前のバージョン用に記述された VSPackage をサポートするために *shim* と呼ばれるアダプターが用意されています。 ただし、既存の VSPackage がある場合は、パフォーマンスと信頼性を向上させるために、新しいテクノロジに更新することをお勧めします。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[言語サービスとエディターの拡張機能の概要](../extensibility/getting-started-with-language-service-and-editor-extensions.md)|エディターの拡張機能を作成する方法について説明します。|
|[エディターの内部](../extensibility/inside-the-editor.md)|エディターの一般的な構造について説明し、その機能の一部を示します。|
|[エディター内の Managed Extensibility Framework](../extensibility/managed-extensibility-framework-in-the-editor.md)|エディターで Managed Extensibility Framework (MEF) を使用する方法について説明します。|
|[言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)|エディターの拡張ポイントを一覧表示します。 拡張ポイントは、拡張可能なエディター機能のことです。|
|[チュートリアル: ビューの表示要素、コマンド、設定の作成 (垂直グリッド ガイド)](../extensibility/walkthrough-creating-a-view-adornment-commands-and-settings-column-guides.md)|コードを特定の表示幅に維持できるように、垂直グリッド ガイド線を描画するビューの表示要素の構築についてのチュートリアルと説明です。  また、設定の読み取りと書き込みに加え、コマンド ウィンドウから呼び出すことができるコマンドの宣言と実装についても説明します。|
|[エディターのインポート](../extensibility/editor-imports.md)|拡張機能がインポートできるサービスを一覧表示します。|
|[レガシ コードをエディターに適合させる](/previous-versions/visualstudio/visual-studio-2015/extensibility/adapting-legacy-code-to-the-editor?preserve-view=true&view=vs-2015)|エディターを拡張するためにレガシ コード (Visual Studio 2010 より前) を適合させるためのさまざまな方法について説明します。|
|[従来の言語サービスの移行](../extensibility/internals/migrating-a-legacy-language-service.md)|VSPackage ベースの言語サービスを移行する方法について説明します。|
|[チュートリアル: コンテンツ タイプとファイル名拡張子とをリンクさせる](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)|コンテンツ タイプとファイル名拡張子とをリンクさせる方法について説明します。|
|[チュートリアル: 余白のグリフを作成する](../extensibility/walkthrough-creating-a-margin-glyph.md)|余白にアイコンを追加する方法について説明します。|
|[チュートリアル: テキストの強調表示](../extensibility/walkthrough-highlighting-text.md)|*タグ* を使用してテキストを強調表示する方法について説明します。|
|[チュートリアル: アウトラインの追加](../extensibility/walkthrough-outlining.md)|特定の種類のかっこにアウトラインを追加する方法について説明します。|
|[チュートリアル: 対応するかっこを表示する](../extensibility/walkthrough-displaying-matching-braces.md)|対応する中かっこを強調表示する方法について説明します。|
|[チュートリアル: QuickInfo ツールヒントの表示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)|プロパティ、メソッド、イベントなどのコード要素を記述する QuickInfo ポップアップを表示する方法について説明します。|
|[チュートリアル: シグネチャ ヘルプの表示](../extensibility/walkthrough-displaying-signature-help.md)|シグネチャのパラメーターの数と型に関する情報を提供するポップアップを表示する方法について説明します。|
|[チュートリアル: 入力候補の表示](../extensibility/walkthrough-displaying-statement-completion.md)|ステートメント入力候補を実装する方法について説明します。|
|[チュートリアル: コード スニペットの実装](../extensibility/walkthrough-implementing-code-snippets.md)|コード スニペットの拡張を実装する方法について説明します。|
|[チュートリアル: 電球アイコンによる提案の表示](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)|コード候補に電球アイコンを表示する方法について説明します。|
|[チュートリアル: エディター拡張機能でシェル コマンドを使用する](../extensibility/walkthrough-using-a-shell-command-with-an-editor-extension.md)|VSPackage のメニュー コマンドを MEF コンポーネントに関連付ける方法について説明します。|
|[チュートリアル: エディター拡張機能でショートカット キーを使用する](../extensibility/walkthrough-using-a-shortcut-key-with-an-editor-extension.md)|VSPackage のメニュー ショートカットを MEF コンポーネントに関連付ける方法について説明します。|
|[MEF (Managed Extensibility Framework)](/dotnet/framework/mef/index)|Managed Extensibility Framework (MEF) に関する情報を提供します。|
|[Windows Presentation Foundation](/dotnet/framework/wpf/index)|Windows Presentation Foundation (WPF) に関する情報を提供します。|

## <a name="reference"></a>関連項目
 Visual Studio エディターには、次の名前空間が含まれています。

 <xref:Microsoft.VisualStudio.Language.Intellisense>

 <xref:Microsoft.VisualStudio.Language.StandardClassification>

 <xref:Microsoft.VisualStudio.Editor>

 <xref:Microsoft.VisualStudio.Text>

 <xref:Microsoft.VisualStudio.Text.Adornments>

 <xref:Microsoft.VisualStudio.Text.Classification>

 <xref:Microsoft.VisualStudio.Text.Differencing>

 <xref:Microsoft.VisualStudio.Text.Document>

 <xref:Microsoft.VisualStudio.Text.Editor>

 <xref:Microsoft.VisualStudio.Text.Editor.OptionsExtensionMethods>

 <xref:Microsoft.VisualStudio.Text.Formatting>

 <xref:Microsoft.VisualStudio.Text.IncrementalSearch>

 <xref:Microsoft.VisualStudio.Text.Operations>

 <xref:Microsoft.VisualStudio.Text.Outlining>

 <xref:Microsoft.VisualStudio.Text.Projection>

 <xref:Microsoft.VisualStudio.Text.Tagging>

 <xref:Microsoft.VisualStudio.Utilities>