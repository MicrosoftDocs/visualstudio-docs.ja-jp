---
title: 従来の言語サービスでのパラメーター ヒント 1 | Microsoft Docs
description: 従来の言語サービスでユーザーにヒントを提供する IntelliSense の [パラメーター ヒント] ツールヒントを実装する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, method tips
- method tips
- language services, parameter info tooltip
- IVsMethodData interface
- Parameter Info (IntelliSense)
ms.assetid: f367295e-45b6-45d2-9ec8-77481743beef
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4dade924ef89be22161c598ba0ae64084c0697ea
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061148"
---
# <a name="parameter-info-in-a-legacy-language-service-1"></a>従来の言語サービスでのパラメーター ヒント 1
IntelliSense の [パラメーター ヒント] ツールヒントは、ユーザーに、自分がいる言語構成要素内の場所に関するヒントを提供します。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能の新しい実装方法では MEF 拡張機能が使用されます。 詳細については、「[エディターと言語サービスの拡張](../../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

> [!NOTE]
> 新しいエディターの API をできるだけ早く使い始めることをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="how-parameter-info-tooltips-work"></a>[パラメーター ヒント] ツールヒントのしくみ
 エディターでステートメントを入力すると、VSPackage には、入力されているステートメントの定義を含む小さなツールヒント ウィンドウが表示されます。 たとえば、Microsoft Foundation Classes (MFC) のステートメント (`pMainFrame ->UpdateWindow` など) を入力し、左中かっこキーを押してパラメーターの一覧表示を開始すると、メソッド ヒントが現れ `UpdateWindow` メソッドの定義が表示されます。

 [パラメーター ヒント] ツールヒントは通常、ステートメント補完と組み合わせて使用されます。 これらは、メソッド名またはキーワードの後にパラメーターやその他のフォーマットされた情報が続く言語の場合に最も役立ちます。

 [パラメーター ヒント] ツールヒントは、コマンド インターセプトを経由して、言語サービスによって開始されます。 ユーザー文字をインターセプトするには、言語サービス オブジェクトで <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスを実装し、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> インターフェイスの <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> メソッドを呼び出すことによって、テキスト ビューに <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 実装へのポインターを渡す必要があります。 コマンド フィルターでは、ユーザーがコード ウィンドウに入力したコマンドをインターセプトします。 ユーザーにパラメーター ヒントを表示するタイミングを知るには、コマンド情報を監視します。 同じコマンド フィルターをステートメント補完やエラー マーカーなどにも使用できます。

 言語サービスでヒントを提供できるキーワードが入力されると、言語サービスでは <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> オブジェクトを作成し、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> インターフェイスの <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> メソッドを呼び出して IDE にヒントを表示するよう通知します。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> オブジェクトは、`VSLocalCreateInstance` を使用し、コクラス `CLSID_VsMethodTipWindow` を指定して作成します。 `VsLocalCreateInstance` は、ローカル レジストリのために `QueryService` を呼び出し、`CLSID_VsMethodTipWindow` のためにこのオブジェクトで `CreateInstance` を呼び出す、ヘッダー ファイル vsdoc.h で定義されている関数です。

## <a name="providing-a-method-tip"></a>メソッド ヒントの提供
 メソッド ヒントを提供するには、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> インターフェイスの <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> メソッドを呼び出し、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> インターフェイスの実装を渡します。

 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> クラスが呼び出されると、そのメソッドは次の順序で呼び出されます。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetContextStream%2A>

     現在のテキスト バッファー内の関連データの位置と長さを返します。 これは、IDE に、そのデータをツールヒント ウィンドウで隠さないように指示します。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetCurMethod%2A>

     最初に表示するメソッド番号 (0 から始まるインデックス) を返します。 たとえば、0 を返した場合は、最初にオーバーロードされたメソッドが最初に表示されます。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetOverloadCount%2A>

     現在のコンテキストで適用できるオーバーロードされたメソッドの数を返します。 このメソッドで 1 より大きい値を返した場合、テキスト ビューには上矢印と下矢印が自動的に表示されます。 下矢印をクリックすると、IDE では <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.NextMethod%2A> メソッドを呼び出します。 上矢印をクリックすると、IDE では <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.PrevMethod%2A> メソッドを呼び出します。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetMethodText%2A>

     [パラメーター ヒント] ツールヒントのテキストは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetMethodText%2A> メソッドと <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterText%2A> メソッドを何回か呼び出している間に構成されます。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterCount%2A>

     このメソッドで表示するパラメーターの数を返します。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterText%2A>

     表示するオーバーロードに対応するメソッド番号を返した場合は、このメソッドが呼び出され、その後に <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A> メソッドが呼び出されます。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A>

     メソッド ヒントが表示されたとき、言語サービスにエディターを更新するよう通知します。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A> メソッドでは、次を呼び出します。

    ```
    <pTxWin> ->UpdateTipWindow(<pTip>, UTW_CONTENTCHANGED | UTW_CONTEXTCHANGED).
    ```

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A>

     メソッド ヒント ウィンドウを閉じると、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A> メソッドの呼び出しを受信します。
