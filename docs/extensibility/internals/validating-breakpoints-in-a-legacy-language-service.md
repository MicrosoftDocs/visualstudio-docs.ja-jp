---
title: 従来の言語サービスでのブレークポイントの検証 | Microsoft Docs
description: 従来の言語サービスで ValidateBreakpointLocation メソッドをオーバーライドして、デバッガーが起動する前にブレークポイントを検証する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoint validation
- language services [managed package framework], breakpoint validation
ms.assetid: a7e873cd-dfe1-474f-bda5-fd7532774b15
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 86029300c34e111344157bf39a15dceab8c1b77a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085794"
---
# <a name="validating-breakpoints-in-a-legacy-language-service"></a>従来の言語サービスでのブレークポイントの検証
ブレークポイントは、デバッガーでの実行中に特定の位置でプログラムの実行を停止する必要があることを示します。 エディターではブレークポイントの位置が有効であるかどうかを判断できないため、ソース ファイル内の任意の行にブレークポイントを設定できます。 デバッガーを起動すると、マークされているすべてのブレークポイント (保留中のブレークポイントと呼ばれます) が、実行されているプログラム内の適切な位置にバインドされます。 同時に、有効なコードの位置がマークされていることを確認するために、ブレークポイントが検証されます。 たとえば、コメントに対するブレークポイントは無効です。これは、ソースコード内のその位置にはコードがないためです。 デバッガーによって、無効なブレークポイントが無効にされます。

 言語サービスでは表示されているソース コードを認識しているため、デバッガーを起動する前にブレークポイントを検証できます。 <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A> メソッドをオーバーライドして、ブレークポイントの有効な位置を指定する範囲を返すことができます。 デバッガーが起動されるときにもブレークポイントの位置が検証されますが、デバッガーが読み込まれるのを待つことなく、無効なブレークポイントがユーザーに通知されます。

## <a name="implementing-support-for-validating-breakpoints"></a>ブレークポイントの検証のサポートの実装

- <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A> メソッドには、ブレークポイントの位置が指定されます。 実装では、位置が有効であるかどうかを判断し、ブレークポイントの行の位置に関連付けられているコードを識別するテキスト範囲を返すことによってこれを示す必要があります。

- 位置が有効である場合は <xref:Microsoft.VisualStudio.VSConstants.S_OK> を返し、有効でない場合は <xref:Microsoft.VisualStudio.VSConstants.S_FALSE> を返します。

- ブレークポイントが有効な場合は、テキスト範囲がブレークポイントと共に強調表示されます。

- ブレークポイントが無効な場合は、エラー メッセージがステータス バーに表示されます。

### <a name="example"></a>例
 この例は、パーサーを呼び出して、指定した位置にあるコード (存在する場合) の範囲を取得する <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A> メソッドの実装を示しています。

 この例では、テキスト範囲を検証する <xref:Microsoft.VisualStudio.Package.AuthoringSink> クラスに `GetCodeSpan` メソッドを追加し、有効なブレークポイントの位置である場合は `true` が返されることを想定しています。

```csharp
using Microsoft VisualStudio;
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    class TestLanguageService : LanguageService
    {
        public override int ValidateBreakpointLocation(IVsTextBuffer buffer,
                                                       int line,
                                                       int col,
                                                       TextSpan[] pCodeSpan)
        {
            int retval = VSConstants.S_FALSE;
            if (pCodeSpan != null)
            {
                // Initialize span to current line by default.
                pCodeSpan[0].iStartLine = line;
                pCodeSpan[0].iStartIndex = col;
                pCodeSpan[0].iEndLine = line;
                pCodeSpan[0].iEndIndex = col;
            }

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
                                                              ParseReason.CodeSpan,
                                                              null);
                        req.Scope = this.ParseSource(req);
                        TestAuthoringSink sink = req.Sink as TestAuthoringSink;

                        TextSpan span = new TextSpan();
                        if (sink.GetCodeSpan(out span))
                        {
                            pCodeSpan[0] = span;
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

## <a name="see-also"></a>関連項目
- [従来の言語サービスの機能](../../extensibility/internals/legacy-language-service-features1.md)
