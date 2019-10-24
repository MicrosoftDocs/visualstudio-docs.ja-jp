---
title: 従来の言語サービスの構文色分け |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], syntax highlighting
- colorization, supporting in language services [managed package framework]
- syntax highlighting, supporting in language services [managed package framework]
- language services [managed package framework], colorization
ms.assetid: 1ca1736a-f554-42e4-a9c7-fe8c3c1717df
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 19561363affada05154e15142bd32a30a5d051d0
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72722829"
---
# <a name="syntax-colorizing-in-a-legacy-language-service"></a>従来の言語サービスでの構文の配色変更
構文の色づけは、プログラミング言語のさまざまな要素を異なる色やスタイルのソースファイルに表示する機能です。 この機能をサポートするには、ファイル内の字句要素またはトークンの種類を識別できるパーサーまたはスキャナーを用意する必要があります。 多くの言語では、キーワード、区切り記号 (かっこや中かっこなど)、コメントを区別するためにさまざまな方法で色分けしています。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能を実装するための新しい方法として、MEF 拡張機能を使用することをお勧めします。 詳細については、「[エディターと言語サービスの拡張](../../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、エディターの新機能を利用できるようになります。

## <a name="implementation"></a>実装
 色付けをサポートするために、managed package framework (MPF) には、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> インターフェイスを実装する <xref:Microsoft.VisualStudio.Package.Colorizer> クラスが含まれています。 このクラスは、トークンと色を決定するために <xref:Microsoft.VisualStudio.Package.IScanner> と対話します。 スキャナーの詳細については、「[従来の言語サービスパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)」を参照してください。 @No__t_0 クラスは、トークンの各文字に色情報をマークし、その情報をソースファイルを表示するエディターに返します。

 エディターに返されるカラー情報は、装飾項目の一覧のインデックスです。 各装飾項目は、カラー値と、太字や取り消し線などのフォント属性のセットを指定します。 このエディターには、言語サービスで使用できる既定の装飾項目のセットが用意されています。 必要なのは、トークンの種類ごとに適切な色のインデックスを指定することだけです。 ただし、カスタム装飾項目のセットと、トークン用に提供するインデックスを指定し、既定のリストではなく、独自の装飾項目のリストを参照することができます。 また、カスタムの色をサポートするには、`RequestStockColors` レジストリエントリを 0 (または `RequestStockColors` エントリをまったく指定しない) に設定する必要があります。 このレジストリエントリは、名前付きパラメーターを使用して <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> ユーザー定義属性に設定できます。 言語サービスの登録とそのオプションの設定の詳細については、「[従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)」を参照してください。

## <a name="custom-colorable-items"></a>カスタムの配色可能な項目
 独自のカスタム装飾項目を指定するには、<xref:Microsoft.VisualStudio.Package.LanguageService> クラスの <xref:Microsoft.VisualStudio.Package.LanguageService.GetItemCount%2A> および <xref:Microsoft.VisualStudio.Package.LanguageService.GetColorableItem%2A> メソッドをオーバーライドする必要があります。 最初のメソッドは、言語サービスがサポートするカスタム装飾項目の数を返します。2番目のメソッドは、インデックスを使用してカスタム装飾項目を取得します。 カスタム装飾項目の既定の一覧を作成します。 言語サービスのコンストラクターでは、各装飾項目に名前を指定するだけで済みます。 ユーザーが別の装飾項目のセットを選択した場合は、Visual Studio によって自動的に処理されます。 この名前は、 **[オプション]** ダイアログボックス (Visual Studio の **[ツール]** メニューから利用可能) の **[フォントおよび色]** プロパティページに表示されます。この名前によって、ユーザーが上書きした色が決まります。 ユーザーの選択は、レジストリのキャッシュに格納され、色の名前によってアクセスされます。 **[フォントおよび色]** プロパティページには、すべての色名がアルファベット順に一覧表示されるため、各色の名前の前に使用する言語名を使用して、カスタムの色をグループ化できます。たとえば、"**Testlanguage-Comment**" や "**Testlanguage-Keyword**" などです。 または、「**Comment (testlanguage)** 」と「**Keyword (testlanguage)** 」と入力して、装飾項目をグループ化することもできます。 言語名でグループ化することをお勧めします。

> [!CAUTION]
> 既存の装飾項目名との競合を避けるために、装飾項目名に言語名を含めることを強くお勧めします。

> [!NOTE]
> 開発中にいずれかの色の名前を変更した場合は、最初に色にアクセスしたときに Visual Studio によって作成されたキャッシュをリセットする必要があります。 これを行うには、Visual Studio SDK の プログラム メニューから **実験用ハイブのリセット** コマンドを実行します。

 装飾項目の一覧の最初の項目が参照されないことに注意してください。 Visual Studio では、常に、その項目の既定のテキストの色と属性が提供されます。 これを処理する最も簡単な方法は、プレースホルダー装飾 item を最初の項目として指定することです。

### <a name="high-color-colorable-items"></a>High Color 装飾 Items
 装飾項目では、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> インターフェイスを使用して、24ビットまたは高色の値をサポートすることもできます。 MPF <xref:Microsoft.VisualStudio.Package.ColorableItem> クラスは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> インターフェイスをサポートし、24ビットの色は通常の色と共にコンストラクターで指定されます。 詳細については、<xref:Microsoft.VisualStudio.Package.ColorableItem> クラスのトピックを参照してください。 次の例は、キーワードとコメントに24ビットの色を設定する方法を示しています。 24ビット色は、ユーザーのデスクトップで24ビットカラーがサポートされている場合に使用されます。それ以外の場合は、通常のテキストの色が使用されます。

 これらは言語の既定の色であることに注意してください。ユーザーは、必要に応じてこれらの色を変更できます。

### <a name="example"></a>例
 この例では、<xref:Microsoft.VisualStudio.Package.ColorableItem> クラスを使用して、カスタム装飾項目の配列を宣言して設定する方法の1つを示します。 この例では、24ビットカラーを使用して、キーワードとコメントの色を設定します。

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
 基本 <xref:Microsoft.VisualStudio.Package.LanguageService> クラスには、<xref:Microsoft.VisualStudio.Package.Colorizer> クラスを instantiantes する <xref:Microsoft.VisualStudio.Package.LanguageService.GetColorizer%2A> メソッドがあります。 @No__t_0 メソッドから返されたスキャナーは、<xref:Microsoft.VisualStudio.Package.Colorizer> クラスコンストラクターに渡されます。

 @No__t_0 メソッドは、<xref:Microsoft.VisualStudio.Package.LanguageService> クラスの独自のバージョンで実装する必要があります。 @No__t_0 クラスは、スキャナーを使用して、すべてのトークンカラー情報を取得します。

 スキャナーは、検出されたすべてのトークンの <xref:Microsoft.VisualStudio.Package.TokenInfo> 構造を設定する必要があります。 この構造体には、トークンが占有するスパン、使用する色インデックス、トークンの種類、トークントリガー (「<xref:Microsoft.VisualStudio.Package.TokenTriggers>」を参照) などの情報が含まれます。 @No__t_0 クラスによる色付けに必要なのは、span と color インデックスだけです。

 @No__t_0 構造体に格納されている色のインデックスは、通常、<xref:Microsoft.VisualStudio.Package.TokenColor> 列挙の値です。これにより、キーワードや演算子など、さまざまな言語要素に対応する名前付きインデックスがいくつか提供されます。 カスタム装飾 items リストが <xref:Microsoft.VisualStudio.Package.TokenColor> 列挙に示されている項目と一致する場合は、列挙体を各トークンの色としてのみ使用できます。 ただし、追加の装飾項目がある場合、または既存の値をその順序で使用しない場合は、必要に応じてカスタム装飾項目リストを配置し、そのリストに適切なインデックスを返すことができます。 @No__t_1 構造に格納する場合は、インデックスを <xref:Microsoft.VisualStudio.Package.TokenColor> にキャストするだけで済みます。 [!INCLUDE[vs_current_short](../../code-quality/includes/vs_current_short_md.md)] には、インデックスのみが表示されます。

### <a name="example"></a>例
 次の例では、スキャナーが3種類のトークンを識別する方法を示します。数値、句読点、識別子 (数字または句読点ではないもの) です。 この例は、説明を目的としたものであり、包括的なパーサーとスキャナーの実装を表しているわけではありません。 これは、文字列を返す `GetNextToken()` メソッドを持つ `Lexer` クラスがあることを前提としています。

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
- [従来の言語サービスの特徴](../../extensibility/internals/legacy-language-service-features1.md)
- [従来の言語サービスのパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)