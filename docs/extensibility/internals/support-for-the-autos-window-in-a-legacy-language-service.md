---
title: 従来の言語サービスで自動変数ウィンドウをサポートする
description: '[自動変数] ウィンドウのサポートを実装する方法について説明します。このウィンドウには、デバッグ中のプログラムが一時停止したときにスコープ内にある式が表示されます。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], Autos window
- Autos window, supporting in language services [managed package framework]
ms.assetid: 47d40aae-7a3c-41e1-a949-34989924aefb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 70a8697027cde07ca2b30d01a73a80d771155c5c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080633"
---
# <a name="support-for-the-autos-window-in-a-legacy-language-service"></a>従来の言語サービスでの自動変数ウィンドウのサポート

**[自動変数]** ウィンドウには、デバッグ中のプログラムが (ブレークポイントまたは例外によって) 一時停止したときにスコープ内にある、変数やパラメーターなどの式が表示されます。 式には、変数 (ローカルまたはグローバル)、およびローカル スコープで変更されているパラメーターが含まれる場合があります。 **[自動変数]** ウィンドウには、クラス、構造体、またはその他の型のインスタンス化が含まれる場合もあります。 式エバリュエーターで評価できるものはすべて、 **[自動変数]** ウィンドウに表示される可能性があります。

 Managed Package Framework (MPF) では、 **[自動変数]** ウィンドウの直接サポートは提供されません。 ただし、<xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> メソッドをオーバーライドすると、 **[自動変数]** ウィンドウに表示される式のリストを返すことができます。

## <a name="implementing-support-for-the-autos-window"></a>自動変数ウィンドウのサポートの実装

 **[自動変数]** ウィンドウをサポートするために必要なのは、<xref:Microsoft.VisualStudio.Package.LanguageService> クラスに <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> メソッドを実装することだけです。 実装では、ソース ファイル内の場所が指定されたら、どの式を **[自動変数]** ウィンドウに表示する必要があるかを決定する必要があります。 メソッドからは文字列のリストが返され、各文字列が 1 つの式を表しています。 戻り値 <xref:Microsoft.VisualStudio.VSConstants.S_OK> は、リストに式が含まれていることを示し、<xref:Microsoft.VisualStudio.VSConstants.S_FALSE> は、表示する式が存在しないことを示します。

 実際に返される式は、コード内のその場所に出現する変数またはパラメーターの名前です。 これらの名前が式エバリュエーターに渡されて値と型が取得され、その後 **[自動変数]** ウィンドウに表示されます。

### <a name="example"></a>例
 次の例は、解析理由 <xref:Microsoft.VisualStudio.Package.ParseReason> を使用して <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドから式のリストを取得する <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> メソッドの実装を示しています。 各式は、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsEnumBSTR> インターフェイスを実装する `TestVsEnumBSTR` としてラップされます。

 `GetAutoExpressionsCount` メソッドと `GetAutoExpression` メソッドは、`TestAuthoringSink` オブジェクトのカスタム メソッドであり、 この例をサポートするために追加されています。 これは、パーサーによって (<xref:Microsoft.VisualStudio.Package.AuthoringSink.AutoExpression%2A> メソッドを呼び出すことによって) `TestAuthoringSink` オブジェクトに追加された式にパーサーの外部でアクセスする 1 つの方法を表しています。

```csharp
using Microsoft.VisualStudio;
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        public override int GetProximityExpressions(IVsTextBuffer buffer,
                                                    int line,
                                                    int col,
                                                    int cLines,
                                                    out IVsEnumBSTR ppEnum)
        {
            int retval = VSConstants.E_NOTIMPL;
            ppEnum = null;
            if (buffer != null)
            {
                IVsTextLines textLines = buffer as IVsTextLines;
                if (textLines != null)
                {
                    Source src = this.GetSource(textLines);
                    if (src != null)
                    {
                        TokenInfo tokenInfo = new TokenInfo();
                        string text = src.GetText();
                        ParseRequest req = CreateParseRequest(src,
                                                              line,
                                                              col,
                                                              tokenInfo,
                                                              text,
                                                              src.GetFilePath(),
                                                              ParseReason.Autos,
                                                              null);
                        req.Scope = this.ParseSource(req);
                        TestAuthoringSink sink = req.Sink as TestAuthoringSink;

                        retval = VSConstants.S_FALSE;
                        int spanCount = sink.GetAutoExpressionsCount();
                        if (spanCount > 0) {
                            TestVsEnumBSTR bstrList = new TestVsEnumBSTR();
                            for (int i = 0; i < spanCount; i++)
                            {
                                TextSpan span;
                                sink.GetAutoExpression(i, out span);
                                string expression = src.GetText(span.iStartLine,
                                                                span.iStartIndex,
                                                                span.iEndLine,
                                                                span.iEndIndex);
                                bstrList.AddString(expression);
                            }
                            ppEnum = bstrList;
                            retval = VSConstants.S_OK;
                        }
                    }
                }
            }
            return retval;
        }
    }
}
```
