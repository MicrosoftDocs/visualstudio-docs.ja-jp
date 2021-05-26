---
title: 従来の言語サービスの基本情報 |Microsoft Docs
description: 従来の言語サービスで使用できる、Visual Studio にプログラミング言語を統合するための重要な機能について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- languages, integrating into Visual Studio
- language services, integrating programming languages
- Visual Studio, integrating programming languages
- programming languages, integrating into Visual Studio
ms.assetid: c15e0ccb-e7c5-4dbb-affb-fe3d3244debe
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fa3fc358e7557360f02a80f108bcbec74ae48e5f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074562"
---
# <a name="legacy-language-service-essentials"></a>従来の言語サービスの基本情報
Visual Studio にプログラミング言語を統合するには、言語サービスを提供する必要があります。 このトピックでは、従来の言語サービスで使用できる機能について説明します。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能の新しい実装方法では MEF 拡張機能が使用されます。 言語サービスの新しい実装方法の詳細については、「[エディターと言語サービスの拡張機能](../../extensibility/editor-and-language-service-extensions.md)」を参照してください。

> [!NOTE]
> 新しいエディターの API をできるだけ早く使い始めることをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

 従来の言語サービスは、次の機能を提供します。

|機能|説明|
|-------------|-----------------|
|構文の色分け表示|エディター ビューで、言語のさまざまな要素に対してさまざまな色とフォント スタイルを表示します。 このような区別により、ファイルの読み取りや編集が容易になります。<br /><br /> 一般的な情報については、「[従来の言語サービスでの構文の色分け表示](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)」を参照してください。<br /><br /> マネージド パッケージ フレームワーク (MPF) のこの機能の詳細については、「[従来の言語サービスでの構文の色分け表示](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)」を参照してください。|
|ステートメント入力候補|ユーザーが入力を開始したステートメントまたはキーワードを補完します。 ステートメント入力候補により、入力が少なくなり、エラーが発生する可能性が低くなるため、ユーザーは難しいステートメントをより簡単に入力できます。<br /><br /> 一般的な情報については、「[従来の言語サービスでのステートメント入力候補](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)」を参照してください。<br /><br /> MPF のこの機能の詳細については、「[従来の言語サービスでの単語補完](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)」を参照してください。|
|かっこの一致|中かっこなどのペアの文字を強調表示します。 ユーザーが "}" などの終了文字を入力すると、かっこの一致により、対応する開始文字 ("{" など) が強調表示されます。 囲み文字が複数ある場合にこの機能を使用すると、ユーザーは、囲み文字が正しくペアになっていることを確認できます。<br /><br /> MPF のこの機能の詳細については、「[従来の言語サービスでの中かっこの一致](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)」を参照してください。|
|パラメーター ヒントのツールヒント|ユーザーが現在入力しているオーバーロードされたメソッドに使用できるシグネチャの一覧を表示します。<br /><br /> 一般的な情報については、[従来の言語サービスでのパラメーター ヒント](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)に関するページを参照してください。<br /><br /> MPF のこの機能の詳細については、[従来の言語サービスでのパラメーター ヒント](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)に関するページを参照してください。|
|エラー マーカー|構文が正しくないテキストの下に赤い波形の下線 (波線とも呼ばれます) を表示します。 通常、エラー マーカーは、スペルが間違っているキーワード、閉じられていないかっこ、無効な文字、および類似したエラーをユーザーに認識させるために使用されます。<br /><br /> MPF クラスでは、エラー マーカーは <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddError%2A> クラスの <xref:Microsoft.VisualStudio.Package.AuthoringSink> メソッドで自動的に処理されます。|

 これらの機能の多くでは、言語サービスでソース コードを解析する必要があります。 多くの場合、コンパイラまたはインタープリターのトークン化および解析コードを再利用できます。

 次の機能はプログラミング言語のサポートに関連していますが、言語サービスには含まれていません。

| 機能 | 説明 |
|-----------------------| - |
| 式エバリュエーター | ブレークポイントを検証し、 **[自動変数]** デバッグ ウィンドウに表示される式の一覧を指定することにより、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッガーをサポートします。<br /><br /> 詳細については、「[デバッグのための言語サービスのサポート](../../extensibility/internals/language-service-support-for-debugging.md)」を参照してください。 |
| シンボル参照ツール | "**オブジェクト ブラウザー**"、"**クラス ビュー**"、"**呼び出しブラウザー**"、および "**シンボル結果の検索**" をサポートします。 |
