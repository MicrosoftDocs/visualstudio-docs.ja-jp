---
title: 従来の言語サービスのアウトライン | Microsoft Docs
description: 従来の言語サービスに非表示領域を実装してアウトラインをサポートする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- outlining
- language services [managed package framework], outlining
- outlining, supporting in language services [managed package framework]
ms.assetid: 7b5578b4-a20a-4b94-ad4c-98687ac133b9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a56d755341aa611f0e2762f6bae8940778fe0864
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062955"
---
# <a name="outlining-in-a-legacy-language-service"></a>従来の言語サービスのアウトライン
アウトラインを使用すると、複雑なプログラムを概要やアウトラインに折りたたむことができます。 たとえば、C# では、すべてのメソッドを 1 行に折りたたんで、メソッドのシグネチャのみを表示することができます。 また、構造体とクラスを折りたたんで、構造体とクラスの名前のみを表示することもできます。 1 つのメソッド内で、`foreach`、`if`、`while` など、ステートメントの最初の行のみを表示して、複雑なロジックを折りたたんでフロー全体を表示できます。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能の新しい実装方法では MEF 拡張機能が使用されます。 詳細については、「[チュートリアル: アウトライン](../../extensibility/walkthrough-outlining.md)」を参照してください。

> [!NOTE]
> 新しいエディターの API をできるだけ早く使い始めることをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="enabling-support-for-outlining"></a>アウトラインのサポートの有効化
 自動アウトラインを有効にするには、`AutoOutlining` レジストリ エントリを 1 に設定します。 自動アウトラインでは、非表示領域を識別してアウトライン グリフを表示するために、ファイルの読み込み時または変更時にソース全体の解析が設定されます。 アウトラインは、ユーザーが手動で制御することもできます。

 `AutoOutlining` レジストリ エントリの値は、<xref:Microsoft.VisualStudio.Package.LanguagePreferences> クラスの <xref:Microsoft.VisualStudio.Package.LanguagePreferences.AutoOutlining%2A> プロパティを使用して取得できます。 `AutoOutlining` レジストリ エントリは、<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 属性の名前付きパラメーターを使用して初期化できます (詳細については、「[従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)」を参照してください)。

## <a name="the-hidden-region"></a>非表示領域
 アウトラインを提供するには、言語サービスで非表示領域がサポートされている必要があります。 これらは、展開または折りたたむことができるテキストの範囲です。 非表示領域は、標準の言語シンボル (中かっこなど) またはカスタム シンボルで区切ることができます。 たとえば、C# には、非表示の領域を区切る `#region`/`#endregion` のペアがあります。

 非表示領域は、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> インターフェイスとして公開されている非表示領域マネージャーによって管理されます。

 アウトラインでは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenRegion> インターフェイスで非表示領域を使用し、非表示領域のスパン、現在の表示状態、スパンが折りたたまれているときに表示されるバナーが含まれます。

 言語サービス パーサーでは、<xref:Microsoft.VisualStudio.Package.AuthoringSink.AddHiddenRegion%2A> メソッドを使用して、非表示領域の既定の動作で新しい非表示領域を追加しますが、<xref:Microsoft.VisualStudio.Package.AuthoringSink.AddHiddenRegion%2A> メソッドを使用すると、アウトラインの外観と動作をカスタマイズできます。 非表示領域が非表示領域セッションに与えられると、言語サービスに代わって [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] により非表示領域が管理されます。

 非表示領域セッションが破棄されるタイミングを判断する必要がある場合、非表示領域を変更する場合、または特定の非表示領域が表示されるようにする必要がある場合は、<xref:Microsoft.VisualStudio.Package.Source> クラスからクラスを派生させ、それぞれ適切なメソッドである <xref:Microsoft.VisualStudio.Package.Source.OnBeforeSessionEnd%2A>、<xref:Microsoft.VisualStudio.Package.Source.OnHiddenRegionChange%2A>、<xref:Microsoft.VisualStudio.Package.Source.MakeBaseSpanVisible%2A> をオーバーライドする必要があります。

### <a name="example"></a>例
 中かっこのすべてのペアに対して非表示領域を作成する簡単な例を次に示します。 言語にかっこの一致が用意されており、一致するかっこに少なくとも中かっこ ({ と }) が含まれていることを前提としています。 このアプローチは、説明のみを目的としています。 完全に実装すれば、<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> のケースを完全に処理できます。 この例では、<xref:Microsoft.VisualStudio.Package.LanguagePreferences.AutoOutlining%2A> 基本設定を一時的に `true` に設定する方法も示しています。 別の方法としては、言語パッケージの `ProvideLanguageServiceAttribute` 属性で `AutoOutlining` 名前付きパラメーターを指定することもできます。

 この例では、コメント、文字列、リテラルに C# の規則を前提としています。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace MyLanguagePackage
{

    public class MyLanguageService : LanguageService
    {
        private LanguagePreferences m_preferences;

        public override LanguagePreferences  GetLanguagePreferences()
        {
            if (m_preferences == null)
            {
                m_preferences = new LanguagePreferences(this.Site,
                                                        typeof(MyLanguageService).GUID,
                                                        Name);
                m_preferences.Init();
                // Temporarily enabled auto-outlining
                m_preferences.AutoOutlining = true;
            }
            return m_preferences;
        }

        public override AuthoringScope  ParseSource(ParseRequest req)
        {
            Source source = (Source) this.GetSource(req.FileName);
            switch (req.Reason)
            {
               case ParseReason.HighlightBraces:
               case ParseReason.MatchBraces:
               case ParseReason.MemberSelectAndHighlightBraces:
                  if (source.Braces != null)
                  {
                      foreach (TextSpan[] brace in source.Braces)
                      {
                         if (brace.Length == 2)
                         {
                             if (req.Sink.HiddenRegions == true
                                   && source.GetText(brace[0]).Equals("{")
                                   && source.GetText(brace[1]).Equals("}"))
                             {
                                //construct a TextSpan of everything between the braces
                                TextSpan hideSpan = new TextSpan();
                                hideSpan.iStartIndex = brace[0].iStartIndex;
                                hideSpan.iStartLine = brace[0].iStartLine;
                                hideSpan.iEndIndex = brace[1].iEndIndex;
                                hideSpan.iEndLine = brace[1].iEndLine;
                                req.Sink.ProcessHiddenRegions = true;
                                req.Sink.AddHiddenRegion(hideSpan);
                             }
                             req.Sink.MatchPair(brace[0], brace[1], 1);
                         }
                         else if (brace.Length >= 3)
                             req.Sink.MatchTriple(brace[0], brace[1], brace[2], 1);
                  }
        }
                   break;
               default:
                   break;
      }
            // Must always return a valid AuthoringScope object.
            return new MyAuthoringScope();
        }
    }
}
```

## <a name="see-also"></a>関連項目
- [従来の言語サービスの機能](../../extensibility/internals/legacy-language-service-features1.md)
- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)
