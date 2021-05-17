---
title: 従来の言語サービスでのかっこの一致 | Microsoft Docs
description: 従来の言語サービスでのかっこの一致について説明します。これは、かっこと中かっこなど、一緒に出現する必要がある言語要素を追跡するために役立ちます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- brace matching
- language services [managed package framework], brace matching
ms.assetid: 4e3d0a70-f22f-49dd-92d8-edf48ab62b52
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a92a3ca34e6314463bbfecbd8c4236789f213635
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086106"
---
# <a name="brace-matching-in-a-legacy-language-service"></a>従来の言語サービスでのかっこの一致
かっこの一致により、開発者は、かっこと中かっこなど、一緒に出現する必要がある言語要素を追跡できます。 開発者が右かっこを入力すると、左かっこが強調表示されます。

 同時に出現する 2 つまたは 3 つの要素 (ペアとトリプルと呼ばれます) を一致させることができます。 トリプルは、同時に出現する 3 つの要素のセットです。 たとえば、C# の `foreach` ステートメントでは `foreach()`、`{`、`}` のトリプルが形成されます。 右中かっこを入力すると、3 つの要素がすべて強調表示されます。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能の新しい実装方法では MEF 拡張機能が使用されます。 かっこの一致の新しい実装方法の詳細については、「[チュートリアル: 一致する中かっこの表示](../../extensibility/walkthrough-displaying-matching-braces.md)」を参照してください。

> [!NOTE]
> 新しいエディターの API をできるだけ早く使い始めることをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

 <xref:Microsoft.VisualStudio.Package.AuthoringSink> クラスでは、<xref:Microsoft.VisualStudio.Package.AuthoringSink.MatchPair%2A> および <xref:Microsoft.VisualStudio.Package.AuthoringSink.MatchTriple%2A> メソッドを使用して、ペアとトリプルの両方がサポートされます。

## <a name="implementation"></a>実装
 言語サービスでは、その言語の一致するすべての要素を識別し、一致するすべてのペアを見つける必要があります。 通常、これを行うには、<xref:Microsoft.VisualStudio.Package.IScanner> を実装して照合する言語を検出し、<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドを使用して要素を照合します。

 <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> メソッドでは、スキャナーを呼び出して行をトークン化し、カレットの直前にそのトークンを返します。 スキャナーでは、現在のトークンに <xref:Microsoft.VisualStudio.Package.TokenTriggers> のトークン トリガー値を設定することによって、言語要素のペアが見つかったことを示します。 <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> メソッドによって、<xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A> メソッドが呼び出されます。このメソッドによって、<xref:Microsoft.VisualStudio.Package.ParseReason> の解析理由値を指定して <xref:Microsoft.VisualStudio.Package.LanguageService.BeginParse%2A> メソッドが呼び出され、一致する言語要素が検索されます。 一致する言語要素が見つかると、両方の要素が強調表示されます。

 かっこを入力するとかっこの強調表示がトリガーされる仕組みの詳細については、「[従来の言語サービスのパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)」の記事の "*解析操作の例*" に関するセクションを参照してください。

## <a name="enable-support-for-brace-matching"></a>かっこの一致のサポートの有効化
 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 属性では、<xref:Microsoft.VisualStudio.Package.LanguagePreferences> クラスの対応するプロパティを設定する **MatchBraces**、**MatchBracesAtCaret**、**ShowMatchingBrace** レジストリ エントリを設定できます。 言語設定のプロパティは、ユーザーが設定することもできます。

|レジストリ エントリ|プロパティ|説明|
|--------------------|--------------|-----------------|
|MatchBraces|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableMatchBraces%2A>|かっこの一致を有効にします。|
|MatchBracesAtCaret|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableMatchBracesAtCaret%2A>|キャレットの移動に応じたかっこの一致を有効にします。|
|ShowMatchingBrace|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A>|一致するかっこを強調表示します。|

## <a name="match-conditional-statements"></a>条件付きステートメントの照合
 `if`、`else if`、`else` または `#if`、`#elif`、`#else`、`#endif` などの条件付きステートメントを区切り記号の照合と同じ方法で照合することができます。 <xref:Microsoft.VisualStudio.Package.AuthoringSink> クラスをサブクラス化して、テキスト範囲と区切り記号を一致する要素の内部配列に追加できるメソッドを提供できます。

## <a name="set-the-trigger"></a>トリガーの設定
 次の例は、一致するかっこ、中かっこ、角かっこを検出し、スキャナーにそのトリガーを設定する方法を示しています。 <xref:Microsoft.VisualStudio.Package.Source> クラスの <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> メソッドでは、トリガーを検出し、パーサーを呼び出して一致するペアを見つけます (この記事の "*一致の検索*" に関するセクションを参照してください)。 この例は、説明のみを目的としています。 テキスト行でトークンを識別して返すメソッド `GetNextToken` がスキャナーに含まれていることを想定しています。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestScanner : IScanner
    {
        private const string braces = "()[]{}";
        private Lexer lex;

        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,
                                                   ref int state)
        {
            bool foundToken = false;
            string token = lex.GetNextToken();
            if (token != null)
            {
                foundToken = true;
                char firstChar = token[0];
                if (Char.IsPunctuation(firstChar) && token.Length > 0)
                {
                    if (braces.IndexOf(firstChar) != -1)
                    {
                        tokenInfo.Trigger = TokenTriggers.MatchBraces;
                    }
                }
            }
            return foundToken;
        }
```

## <a name="match-the-braces"></a>かっこの照合
 言語要素 `{ }`、`( )`、`[ ]` を照合し、それらの範囲を <xref:Microsoft.VisualStudio.Package.AuthoringSink> オブジェクトに追加する簡略化された例を次に示します。 この方法は、ソース コードの解析で推奨される方法ではありません。これは説明のみを目的としています。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class Parser
    {
         private IList<TextSpan[]> m_braces;
         public IList<TextSpan[]> Braces
         {
             get { return m_braces; }
         }
         private void AddMatchingBraces(TextSpan braceSpan1, TextSpan braceSpan2)
         {
             if IsMatch(braceSpan1, braceSpan2)
                 m_braces.Add(new TextSpan[] { braceSpan1, braceSpan2 });
         }

         private bool IsMatch(TextSpan braceSpan1, TextSpan braceSpan2)
         {
             //definition for matching here
          }
    }

    public class TestLanguageService : LanguageService
    {
         Parser parser = new Parser();
         Source source = (Source) this.GetSource(req.FileName);

         private AuthoringScope ParseSource(ParseRequest req)
         {
             if (req.Sink.BraceMatching)
             {
                 if (req.Reason==ParseReason.MatchBraces)
                 {
                     foreach (TextSpan[] brace in parser.Braces)
                     {
                         req.Sink.MatchPair(brace[0], brace[1], 1);
                     }
                 }
             }
             return new TestAuthoringScope();
         }
    }
}
```

## <a name="see-also"></a>関連項目
- [従来の言語サービスの機能](../../extensibility/internals/legacy-language-service-features1.md)
- [従来の言語サービスのパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
