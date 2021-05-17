---
title: 従来の言語サービスでの構文の配色変更 | Microsoft Docs
description: 字句要素またはトークンの種類を識別できるパーサーまたはスキャナーを用意して、従来の言語サービスで構文の配色をサポートする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], syntax highlighting
- colorization, supporting in language services [managed package framework]
- syntax highlighting, supporting in language services [managed package framework]
- language services [managed package framework], colorization
ms.assetid: 1ca1736a-f554-42e4-a9c7-fe8c3c1717df
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 627c0b5184588f77188928b6355a9034a3a3465e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080545"
---
# <a name="syntax-colorizing-in-a-legacy-language-service"></a>従来の言語サービスでの構文の配色変更
構文の配色は、ソース ファイル内にあるプログラミング言語のさまざまな要素を異なる色やスタイルで表示する機能です。 この機能をサポートするには、ファイル内の字句要素またはトークンの種類を識別できるパーサーまたはスキャナーを用意する必要があります。 多くの言語では、さまざまな方法で配色することにより、キーワード、区切り記号 (かっこや中かっこなど)、およびコメントを区別しています。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能の新しい実装方法では MEF 拡張機能が使用されます。 詳細については、「[エディターと言語サービスの拡張](../../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

> [!NOTE]
> 新しいエディターの API をできるだけ早く使い始めることをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="implementation"></a>実装
 配色をサポートするために、マネージド パッケージ フレームワーク (MPF) には、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> インターフェイスを実装する <xref:Microsoft.VisualStudio.Package.Colorizer> クラスが含まれています。 このクラスでは、<xref:Microsoft.VisualStudio.Package.IScanner> と連携してトークンと色を決定します。 スキャナーの詳細については、「[従来の言語サービスパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)」を参照してください。 次に、<xref:Microsoft.VisualStudio.Package.Colorizer> クラスではトークンの各文字を色情報でマークし、その情報をソース ファイルを表示するエディターに返します。

 エディターに返される色情報は、配色可能な項目の一覧のインデックスです。 それぞれの配色可能な項目では、色の値と、太字や取り消し線などのフォント属性のセットを指定します。 エディターには、言語サービスで使用できる既定の配色可能な項目のセットが用意されています。 必要なのは、トークンの種類ごとに適切な色のインデックスを指定することだけです。 ただし、カスタムの配色可能な項目のセットと、トークン用に提供するインデックスを用意して、既定の一覧ではなく独自の配色可能な項目の一覧を参照することができます。 また、カスタム色をサポートするには、`RequestStockColors` レジストリ エントリを 0 に設定する (または `RequestStockColors` エントリをまったく指定しない) 必要があります。 このレジストリ エントリは、名前付きパラメーターを使用して <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> ユーザー定義属性に設定できます。 言語サービスの登録とそのオプションの設定の詳細については、[従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)に関するページを参照してください。

## <a name="custom-colorable-items"></a>カスタムの配色可能な項目
 独自のカスタムの配色可能な項目を指定するには、<xref:Microsoft.VisualStudio.Package.LanguageService> クラスの <xref:Microsoft.VisualStudio.Package.LanguageService.GetItemCount%2A> メソッドと <xref:Microsoft.VisualStudio.Package.LanguageService.GetColorableItem%2A> メソッドをオーバーライドする必要があります。 最初のメソッドでは、言語サービスがサポートするカスタムの配色可能な項目の数を返します。2 番目のメソッドでは、インデックスを使用してカスタムの配色可能な項目を取得します。 カスタムの配色可能な項目の既定の一覧を作成します。 言語サービスのコンストラクターでは、それぞれの配色可能な項目に名前を指定するだけで済みます。 ユーザーが配色可能な項目の別のセットを選択した場合は、Visual Studio によって自動的に処理されます。 この名前は、 **[オプション]** ダイアログ ボックス (Visual Studio の **[ツール]** メニューから利用可能) の **[フォントおよび色]** プロパティ ページに表示され、この名前によってユーザーが上書きした色が決まります。 ユーザーの選択は、レジストリのキャッシュに格納され、色の名前によってアクセスされます。 **[フォントおよび色]** プロパティ ページにはすべての色名がアルファベット順に一覧表示されるため、"**Testlanguage-Comment**" や "**Testlanguage-Keyword**" のように各色名の前に言語名を追加して、カスタムの色をグループ化できます。 または、"**Comment (TestLanguage)** " や "**Keyword (TestLanguage)** " と入力して、配色可能な項目をグループ化することもできます。 言語名でグループ化することをお勧めします。

> [!CAUTION]
> 既存の配色可能な項目の名前との競合を避けるために、配色可能な項目の名前に言語名を含めることを強くお勧めします。

> [!NOTE]
> 開発中にいずれかの色の名前を変更した場合、その色に最初にアクセスしたときに、Visual Studio によって作成されたキャッシュをリセットする必要があります。 これを行うには、Visual Studio SDK のプログラム メニューから **[実験用 Hive のリセット]** コマンドを実行します。

 配色可能な項目の一覧の最初の項目は参照されないことに注意してください。 Visual Studio では、常に、その項目に既定のテキストの色と属性が使用されます。 これに対処する最も簡単な方法は、プレースホルダーの配色可能な項目を最初の項目として指定することです。

### <a name="high-color-colorable-items"></a>ハイカラーの配色可能な項目
 配色可能な項目では、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> インターフェイスを使用して、24 ビットまたはハイカラーの値をサポートすることもできます。 MPF <xref:Microsoft.VisualStudio.Package.ColorableItem> クラスでは <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> インターフェイスをサポートしているため、24 ビット カラーは標準カラーと共にコンストラクターで指定されます。 詳細については、<xref:Microsoft.VisualStudio.Package.ColorableItem> クラスのトピックを参照してください。 次の例は、キーワードとコメントに 24 ビット カラーを設定する方法を示しています。 24 ビット カラーは、ユーザーのデスクトップで 24 ビット カラーがサポートされている場合に使用されます。それ以外の場合は、標準のテキスト色が使用されます。

 これらは言語の既定の色であることに注意してください。ユーザーは、必要に応じてこれらの色を変更できます。

### <a name="example"></a>例
 この例では、<xref:Microsoft.VisualStudio.Package.ColorableItem> クラスを使用してカスタムの配色可能な項目の配列を宣言および設定する 1 つの方法を示します。 この例では、24 ビット カラーを使用して、キーワードとコメントの色を設定します。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        private ColorableItem[] m_colorableItems;

        TestLanguageService() : base()
        {
            m_colorableItems = new ColorableItem[] {
                new ColorableItem("TestLanguage - Text",
                                  "Text",
                                  COLORINDEX.CI_SYSPLAINTEXT_FG,
                                  COLORINDEX.CI_SYSPLAINTEXT_BK,
                                  System.Drawing.Color.Empty,
                                  System.Drawing.Color.Empty,
                                  FONTFLAGS.FF_DEFAULT),
                new ColorableItem("TestLanguage - Keyword",
                                  "Keyword",
                                  COLORINDEX.CI_MAROON,
                                  COLORINDEX.CI_SYSPLAINTEXT_BK,
                                  System.Drawing.Color.FromArgb(192,32,32),
                                  System.Drawing.Color.Empty,
                                  FONTFLAGS.FF_BOLD),
                new ColorableItem("TestLanguage - Comment",
                                  "Comment",
                                  COLORINDEX.CI_DARKGREEN,
                                  COLORINDEX.CI_LIGHTGRAY,
                                  System.Drawing.Color.FromArgb(32,128,32),
                                  System.Drawing.Color.Empty,
                                  FONTFLAGS.FF_DEFAULT)
                // ...
                // Add as many colorable items as you want to support.
            };
        }
    }
}
```

## <a name="the-colorizer-class-and-the-scanner"></a>Colorizer クラスとスキャナー
 基本 <xref:Microsoft.VisualStudio.Package.LanguageService> クラスには、<xref:Microsoft.VisualStudio.Package.Colorizer> クラスをインスタンス化する <xref:Microsoft.VisualStudio.Package.LanguageService.GetColorizer%2A> メソッドがあります。 <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> メソッドから返されるスキャナーは、<xref:Microsoft.VisualStudio.Package.Colorizer> クラス コンストラクターに渡されます。

 <xref:Microsoft.VisualStudio.Package.LanguageService> クラスの独自のバージョンで <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> メソッドを実装する必要があります。 <xref:Microsoft.VisualStudio.Package.Colorizer> クラスでは、スキャナーを使用してすべてのトークンの色情報を取得します。

 スキャナーでは、検出されたトークンごとに <xref:Microsoft.VisualStudio.Package.TokenInfo> 構造体を設定する必要があります。 この構造体には、トークンが占有する範囲、使用する色インデックス、トークンの種類、トークン トリガー (<xref:Microsoft.VisualStudio.Package.TokenTriggers> に関するページを参照) などの情報が含まれています。 <xref:Microsoft.VisualStudio.Package.Colorizer> クラスによる配色に必要なのは、範囲と色インデックスだけです。

 <xref:Microsoft.VisualStudio.Package.TokenInfo> 構造体に格納される色インデックスは、通常、<xref:Microsoft.VisualStudio.Package.TokenColor> 列挙体からの値です。この列挙体では、キーワードや演算子など、さまざまな言語要素に対応する多数の名前付きインデックスを提供します。 カスタムの配色可能な項目の一覧が <xref:Microsoft.VisualStudio.Package.TokenColor> 列挙体で提示される項目と一致する場合は、この列挙体だけで各トークンの色として使用できます。 ただし、追加の配色可能な項目がある場合、または既存の値をその順序で使用しない場合は、必要に応じてカスタムの配色可能な項目の一覧を並べ替え、その一覧で適切なインデックスを返すことができます。 <xref:Microsoft.VisualStudio.Package.TokenInfo> 構造体に格納する場合は、インデックスを <xref:Microsoft.VisualStudio.Package.TokenColor> にキャストするだけで済みます。[!INCLUDE[vs_current_short](../../code-quality/includes/vs_current_short_md.md)] はこのインデックスのみを認識します。

### <a name="example"></a>例
 次の例では、数値、句読点、識別子 (数字でも句読点でもないもの) という 3 種類のトークンをスキャナーが識別する方法を示します。 この例は、説明を目的としたものであり、パーサーとスキャナーの包括的な実装を表しているわけではありません。 これは、文字列を返す `GetNextToken()` メソッドを持つ `Lexer` クラスがあることを前提としています。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    private Lexer lex;

    public class TestScanner : IScanner
    {
        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,
                                                   ref int state)
        {
            bool foundToken = false;
            string token = lex.GetNextToken();
            if (token != null)
            {
                char firstChar = token[0];
                if (Char.IsPunctuation(firstChar))
                {
                    tokenInfo.Type = TokenType.Operator;
                    tokenInfo.Color = TokenColor.Keyword;
                }
                else if (Char.IsNumber(firstChar))
                {
                    tokenInfo.Type = TokenType.Literal;
                    tokenInfo.Color = TokenColor.Number;
                }
                else
                {
                    tokenInfo.Type = TokenType.Identifier;
                    tokenInfo.Color = TokenColor.Identifier;
                }
            }
            return foundToken;
        }
```

## <a name="see-also"></a>関連項目
- [従来の言語サービスの機能](../../extensibility/internals/legacy-language-service-features1.md)
- [従来の言語サービスのパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)
