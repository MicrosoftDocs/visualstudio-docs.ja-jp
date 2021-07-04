---
title: 従来の言語サービスのインターフェイス | Microsoft Docs
description: Visual Studio SDK で使用可能な、従来の言語サービスの機能を提供するインターフェイスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IVsLanguageInfo interface
- language services, objects
ms.assetid: 03b2d507-f463-417e-bc22-bdac68eeda52
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 75697e1d212b24b743fed62284b384985749fe7b
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898605"
---
# <a name="legacy-language-service-interfaces"></a>従来の言語サービスのインターフェイス
特定のプログラミング言語では、言語サービスのインスタンスは一度に 1 つしか存在できません。 ただし、1 つの言語サービスで複数のエディターを使用できます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、言語サービスは特定のエディターに関連付けられません。 そのため、言語サービス操作を要求する場合は、適切なエディターをパラメーターとして識別する必要があります。

## <a name="common-interfaces-associated-with-language-services"></a>言語サービスに関連付けられている共通のインターフェイス
 エディターは、適切な VSPackage で <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> を呼び出すことによって言語サービスを取得します。 この呼び出しで渡されるサービス ID (SID) は、要求されている言語サービスを識別します。

 言語サービスのコア インターフェイスは、任意の数の個別のクラスに実装できます。 ただし、一般的な方法は、1 つのクラスに次のインターフェイスを実装することです。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageBlock> (省略可)

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> インターフェイスは、すべての言語サービスに実装する必要があります。 言語のローカライズされた名前、言語サービスに関連付けられているファイル名拡張子、色分けツールを取得する方法など、言語サービスに関する情報を提供します。

## <a name="additional-language-service-interfaces"></a>言語サービスのその他のインターフェイス
 その他のインターフェイスは、言語サービスで提供することができます。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、テキスト バッファーのインスタンスごとに、これらのインターフェイスの個別のインスタンスを要求します。 そのため、これらの各インターフェイスを独自のオブジェクトに実装する必要があります。 次の表は、テキスト バッファーのインスタンスごとに 1 つのインスタンスを必要とするインターフェイスを示しています。

|インターフェイス|説明|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|ドロップダウン バーなどのコード ウィンドウの表示要素を管理します。 このインターフェイスは <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A> メソッドを使用して取得できます。 コード ウィンドウごとに 1 つの <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> があります。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>|言語のキーワードと区切り記号を色分けします。 このインターフェイスは <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> メソッドを使用して取得できます。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> は、描画時に呼び出されます。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 内での計算量の多い作業は避けてください。パフォーマンスが低下する可能性があります。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>|IntelliSense パラメーターに関するヒントを提供します。 言語サービスでは、メソッドのデータを表示する必要があることを示す文字 (左かっこなど) を認識すると、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> メソッドを呼び出して、言語サービスがパラメーター ヒントのツールヒントを表示する準備ができていることをテキスト ビューに通知します。 その後、テキスト ビューは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> インターフェイスのメソッドを使用して言語サービスにコールバックし、ツールヒントを表示するために必要な情報を取得します。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>|IntelliSense ステートメント入力候補を提供します。 言語サービスは、入力候補一覧を表示する準備ができると、テキスト ビューで <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> メソッドを呼び出します。 その後、テキスト ビューは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> オブジェクトのメソッドを使用して言語サービスにコールバックします。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>|コマンド ハンドラーを使用してテキスト ビューを変更できるようにします。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> インターフェイスを実装するクラスは、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスも実装する必要があります。 テキスト ビューは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> メソッドに渡された <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> オブジェクトをクエリすることによって、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> オブジェクトを取得し ます。 ビューごとに 1 つの <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> オブジェクトが存在する必要があります。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|ユーザーがコード ウィンドウに入力するコマンドをインターセプトします。 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 実装からの出力を監視して、カスタムの完了情報とビューの変更を提供します<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> オブジェクトをテキスト ビューに渡すには、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> を呼び出します。|

## <a name="see-also"></a>関連項目
- [従来の言語サービスの開発](../../extensibility/internals/developing-a-legacy-language-service.md)
- [チェックリスト: 従来の言語サービスの作成](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)
