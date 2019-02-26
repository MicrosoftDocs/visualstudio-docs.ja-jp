---
title: 従来の言語サービスでのブレークポイントの検証 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoint validation
- language services [managed package framework], breakpoint validation
ms.assetid: a7e873cd-dfe1-474f-bda5-fd7532774b15
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3142d854a3a6371983dc6c5851ad007c387f1480
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56603041"
---
# <a name="validating-breakpoints-in-a-legacy-language-service"></a>従来の言語サービスでのブレークポイントの検証
ブレークポイントは、デバッガーで実行されている間に特定の時点でプログラムの実行を停止することを示します。 ユーザーは、エディターには、ブレークポイントの有効な場所の構成要素の知識があるないため、ソース ファイルの任意の行にブレークポイントを配置できます。 デバッガーが起動されのすべてのマークされたブレークポイント (保留中のブレークポイントと呼ばれます) は実行中のプログラムで適切な場所にバインドされます。 ブレークポイントが検証されていることを確認すると同時に有効なコードの場所をマークします。 などのソース コード内の場所にコードがないため、コメントのブレークポイントが有効でありません。 デバッガーは、無効なブレークポイントを無効にします。

 言語サービスが表示されているソース コードを認識しているために、デバッガーが起動される前に、ブレークポイントを検証できます。 オーバーライドすることができます、<xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A>ブレークポイントの有効な場所を指定する範囲を返します。 デバッガーが起動されが、デバッガーを読み込むを待たず、ユーザーに通知が無効なブレークポイントとブレークポイントの位置はまだ検証されます。

## <a name="implementing-support-for-validating-breakpoints"></a>ブレークポイントを検証するためのサポートの実装

-   <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A>メソッドには、ブレークポイントの位置が与えられます。 実装には、場所が有効期限、およびコードを特定するテキスト範囲を返すことによってこれに関連付けられている行位置ブレークポイントを示すかどうかを決める必要があります。

-   返す<xref:Microsoft.VisualStudio.VSConstants.S_OK>の場所が、有効な場合または<xref:Microsoft.VisualStudio.VSConstants.S_FALSE>が有効でない場合。

-   ブレークポイントが有効な場合は、ブレークポイントと共に、テキスト範囲が強調表示されます。

-   ブレークポイントが有効でない場合は、ステータス バーに、エラー メッセージが表示されます。

### <a name="example"></a>例
 この例の実装を示しています、<xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A>を指定した場所 (ある場合)、コードの範囲を取得するためにパーサーを呼び出すメソッド。

 この例では、追加した、`GetCodeSpan`メソッドを<xref:Microsoft.VisualStudio.Package.AuthoringSink>テキスト範囲を返しますを検証するクラスを`true`ブレークポイントが有効な場所である場合。

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
- [従来の言語サービスの特徴](../../extensibility/internals/legacy-language-service-features1.md)