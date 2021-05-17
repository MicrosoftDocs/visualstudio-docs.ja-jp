---
title: 従来の言語サービスのパーサーとスキャナー | Microsoft Docs
description: 表示されているコードに関する情報を選択する、従来の言語サービスのパーサーとスキャナーについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- parsers, language services [managed package framework]
- language services [managed package framework], Parsers
ms.assetid: 1ac3de27-a23b-438d-9593-389e45839cfa
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9c57bd9f8b71f861fd5be4176211af6907b27e74
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090838"
---
# <a name="legacy-language-service-parser-and-scanner"></a>従来の言語サービスのパーサーとスキャナー
パーサーは言語サービスの中核です。 Managed Package Framework (MPF) 言語クラスでは、表示されているコードに関する情報を選択するために言語パーサーが必要です。 パーサーはテキストを字句トークンに分割してから、種類と機能によってそれらのトークンを識別します。

## <a name="discussion"></a>ディスカッション
 C# のメソッドを次に示します。

```csharp
namespace MyNamespace
{
    class MyClass
    {
        public void MyFunction(int arg1)
        {
            int var1 = arg1;
        }
    }
}
```

 この例では、トークンは単語と句読点です。 トークンの種類は次のとおりです。

|Token Name (トークン名)|トークンの種類|
|----------------|----------------|
|namespace、class、public、void、int|キーワード (keyword)|
|=|operator|
|{ } ( ) ;|delimiter|
|MyNamespace、MyClass、MyFunction、arg1、var1|identifier|
|MyNamespace|namespace|
|MyClass|class|
|MyFunction|メソッド|
|arg1|パラメーター (parameter)|
|var1|ローカル変数 (local variable)|

 パーサーの役割は、トークンを識別することです。 トークンによっては、複数の種類を持つことができます。 パーサーによってトークンが識別された後、言語サービスでは、この情報を使用して、構文の強調表示、かっこの照合、IntelliSense 操作などの有用な機能を提供します。

## <a name="types-of-parsers"></a>パーサーの種類
 言語サービスのパーサーは、コンパイラの一部として使用されるパーサーと同じではありません。 ただし、この種のパーサーでは、スキャナーとパーサーの両方をコンパイラ パーサーと同じ方法で使用する必要があります。

- スキャナーは、トークンの種類を識別するために使用されます。 この情報は、構文の強調表示に使用されたり、トークンの種類をすばやく特定して、かっこの照合のような他の操作を行うために使用されます。 このスキャナーは、<xref:Microsoft.VisualStudio.Package.IScanner> インターフェイスによって表されます。

- パーサーは、トークンの機能とスコープを記述するために使用されます。 この情報は、メソッド、変数、パラメーター、宣言などの言語要素を識別したり、コンテキストに基づいてメンバーとメソッド シグネチャの一覧を提供したりするために、IntelliSense 操作で使用されます。 このパーサーは、中かっこやかっこなど、対応する言語要素のペアを見つけるためにも使用されます。 このパーサーには、<xref:Microsoft.VisualStudio.Package.LanguageService> クラスの <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドを使用してアクセスします。

  スキャナーとパーサーを言語サービス用にどのように実装するかは、ユーザー次第です。 パーサーのしくみと独自のパーサーの記述方法を説明するいくつかのリソースが用意されています。 また、パーサーの作成に役立つ、いくつかの無料および市販の製品が用意されています。

### <a name="the-parsesource-parser"></a>ParseSource パーサー
 コンパイラの一部として使用されるパーサー (トークンがなんらかの形式の実行可能コードに変換される) とは異なり、言語サービスのパーサーはさまざまな理由やさまざまなコンテキストで呼び出すことができます。 <xref:Microsoft.VisualStudio.Package.LanguageService> クラス <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> のメソッドにこの方法をどのように実装するかは、ユーザー次第です。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドがバックグラウンド スレッドで呼び出される可能性があることに注意することが重要です。

> [!CAUTION]
> <xref:Microsoft.VisualStudio.Package.ParseRequest> 構造体には <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> オブジェクトへの参照が含まれています。 この <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> オブジェクトをバックグラウンド スレッドで使用することはできません。 実際、基本 MPF クラスの多くは、バックグラウンド スレッドでは使用できません。 これには <xref:Microsoft.VisualStudio.Package.Source>、<xref:Microsoft.VisualStudio.Package.ViewFilter>、<xref:Microsoft.VisualStudio.Package.CodeWindowManager> の各クラスと、ビューと直接または間接的に通信するその他のクラスが含まれます。

 このパーサーは、通常、初めて呼び出されたとき、または <xref:Microsoft.VisualStudio.Package.ParseReason> の解析理由の値が指定されたときに、ソース ファイル全体を解析します。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドへの後続の呼び出しでは、解析されたコードの小さい部分が処理され、前の完全解析操作の結果を使用することで、より短時間で実行することができます。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドは、<xref:Microsoft.VisualStudio.Package.AuthoringSink> および <xref:Microsoft.VisualStudio.Package.AuthoringScope> オブジェクトを使用して解析操作の結果を伝えます。 <xref:Microsoft.VisualStudio.Package.AuthoringSink> オブジェクトは、特定の解析理由に関する情報を収集するために使用されます。たとえば、対応する中かっこやパラメーター リストが含まれているメソッド シグネチャの範囲に関する情報などです。 <xref:Microsoft.VisualStudio.Package.AuthoringScope> には、宣言とメソッド シグネチャのコレクションが用意されています。また、[移動] の高度な編集オプション ( **[定義に移動]** 、 **[宣言に移動]** 、 **[参照に移動]** ) もサポートされています。

### <a name="the-iscanner-scanner"></a>IScanner スキャナー
 <xref:Microsoft.VisualStudio.Package.IScanner> を実装するスキャナーも実装する必要があります。 ただし、このスキャナーは <xref:Microsoft.VisualStudio.Package.Colorizer> クラスによって 1 行ずつ動作するため、通常はより簡単に実装できます。 各行の先頭では、MPF により、スキャナーに渡される状態変数として使用する値が <xref:Microsoft.VisualStudio.Package.Colorizer> クラスに指定されます。 各行の末尾では、更新された状態変数がスキャナーから返されます。 MPF は各行のこの状態情報をキャッシュするため、スキャナーは、ソース ファイルの先頭から開始しなくても、任意の行から解析を開始できます。 この 1 行の高速スキャンにより、エディターはユーザーに迅速なフィードバックを提供できます。

## <a name="parsing-for-matching-braces"></a>対応する中かっこの解析
 この例は、ユーザーが入力した右中かっこの照合のための制御フローを示しています。 このプロセスでは、色付けに使用されるスキャナーを使用して、トークンの種類と、トークンが対応する中かっこの検索操作をトリガーできるかどうかを確認します。 トリガーが見つかった場合は、対応する中かっこを見つけるために <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドが呼び出されます。 最後に、2 つの中かっこが強調表示されます。

 トリガーの名前と解析理由で中かっこが使用されている場合でも、このプロセスは実際の中かっこに限定されません。 対応するペアとして指定されている文字のペアはすべてサポートされています。 例として、( と )、\< and >、および [ と ] などがあります。

 言語サービスで対応する中かっこがサポートされていると仮定します。

1. ユーザーが右中かっこ (}) を入力します。

2. 中かっこがソース ファイルのカーソル位置に挿入され、カーソルが 1 つ進められます。

3. 型指定された右中かっこで、<xref:Microsoft.VisualStudio.Package.Source> クラスの <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> メソッドが呼び出されます。

4. <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> メソッドは、<xref:Microsoft.VisualStudio.Package.Source> クラスの <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> メソッドを呼び出して、現在のカーソル位置の直前の位置にあるトークンを取得します。 このトークンは、型指定された右中かっこ ) に対応します。

    1. <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> メソッドは、<xref:Microsoft.VisualStudio.Package.Colorizer> オブジェクト上の <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> メソッドを呼び出して、現在の行のすべてのトークンを取得します。

    2. <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> メソッドは、現在の行のテキストを含む <xref:Microsoft.VisualStudio.Package.IScanner> オブジェクト上の <xref:Microsoft.VisualStudio.Package.IScanner.SetSource%2A> メソッドを呼び出します。

    3. <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> メソッドは、<xref:Microsoft.VisualStudio.Package.IScanner> オブジェクト上の <xref:Microsoft.VisualStudio.Package.IScanner.ScanTokenAndProvideInfoAboutIt%2A> メソッドを繰り返し呼び出して、現在の行からすべてのトークンを収集します。

    4. <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> メソッドは、<xref:Microsoft.VisualStudio.Package.Source> クラスのプライベート メソッドを呼び出して、目的の位置が含まれているトークンを取得し、<xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> メソッドから取得したトークンの一覧を渡します。

5. <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> メソッドは、<xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> メソッドから返されたトークン、つまり、右中かっこ ) を表すトークンのトークン トリガー フラグ <xref:Microsoft.VisualStudio.Package.TokenTriggers> を検索します。

6. <xref:Microsoft.VisualStudio.Package.TokenTriggers> トリガー フラグが見つかった場合 は、<xref:Microsoft.VisualStudio.Package.Source> クラスのメソッド <xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A> が呼び出されます。

7. <xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A> メソッドは、解析理由の値 <xref:Microsoft.VisualStudio.Package.ParseReason> で解析操作を開始します。 この操作により、最終的に <xref:Microsoft.VisualStudio.Package.LanguageService> クラスの <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドが呼び出されます。 非同期解析が有効になっている場合、<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドへのこの呼び出しはバックグラウンド スレッドで行われます。

8. 解析操作が完了すると、`HandleMatchBracesResponse` という内部完了ハンドラー (コールバック メソッドとも呼ばれます) が <xref:Microsoft.VisualStudio.Package.Source> クラスで呼び出されます。 この呼び出しは、パーサーによってではなく、<xref:Microsoft.VisualStudio.Package.LanguageService> 基本クラスによって自動的に行われます。

9. `HandleMatchBracesResponse` メソッドは、<xref:Microsoft.VisualStudio.Package.AuthoringSink> オブジェクトに格納されている <xref:Microsoft.VisualStudio.Package.ParseRequest> オブジェクトから範囲の一覧を取得します。 (範囲は、ソース ファイル内の行と文字の範囲を指定する <xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan> 構造体です)。この範囲の一覧には、通常、2 つの範囲 (左と右の中かっこのそれぞれに 1 つ) が含まれています。

10. `HandleBracesResponse` メソッドは、<xref:Microsoft.VisualStudio.Package.ParseRequest> オブジェクトに格納されている <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> オブジェクト上の <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A> メソッドを呼び出します。 これにより、指定された範囲が強調表示されます。

11. <xref:Microsoft.VisualStudio.Package.LanguagePreferences> プロパティ <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A> が有効になっている場合、`HandleBracesResponse` メソッドは、一致する範囲に含まれているテキストを取得し、その範囲の最初の 80 文字をステータス バーに表示します。 これは、対応するペアに付随する言語要素が <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドに含まれている場合に最も適切に動作します。 詳細については、<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A> プロパティを参照してください。

12. 完了しました。

### <a name="summary"></a>まとめ
 対応する中かっこの検索操作は、通常、単純な言語要素のペアに限定されます。 対応するトリプル ("`if(...)`"、"`{`" と "`}`"、または "`else`"、"`{`" と "`}`") などのより複雑な要素は、単語補完操作の一環として強調表示することができます。 たとえば、"else" という単語が終了したときに、対応する "`if`" ステートメントを強調表示することができます。 一連の `if`/`else if` ステートメントがある場合は、そのすべてを、対応する中かっこと同じメカニズムを使用して強調表示することができます。 <xref:Microsoft.VisualStudio.Package.Source> 基本クラスでは、次のように、これが既にサポートされています。スキャナーは、カーソル位置の前にあるトークンのトリガー値 <xref:Microsoft.VisualStudio.Package.TokenTriggers> と組み合わせたトークン トリガー値 <xref:Microsoft.VisualStudio.Package.TokenTriggers> を返す必要があります。

 詳細については、[従来の言語サービスでの中かっこの照合](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)に関するページを参照してください。

## <a name="parsing-for-colorization"></a>色付けの解析
 ソース コードの配色変更は簡単です。トークンの種類を識別し、その種類に関する色情報を返すだけです。 <xref:Microsoft.VisualStudio.Package.Colorizer> クラスは、エディターとスキャナー間の仲介役として機能し、すべてのトークンに関する色情報を提供します。 <xref:Microsoft.VisualStudio.Package.Colorizer> クラスは、<xref:Microsoft.VisualStudio.Package.IScanner> オブジェクトを使用して、行を色付けできるようにしたり、ソース ファイル内のすべての行の状態情報を収集したりします。 MPF 言語サービスのクラスでは、<xref:Microsoft.VisualStudio.Package.Colorizer> クラスは <xref:Microsoft.VisualStudio.Package.IScanner> インターフェイスを介してのみスキャナーと通信するため、オーバーライドする必要はありません。 <xref:Microsoft.VisualStudio.Package.LanguageService> クラスの <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> メソッドをオーバーライドすることによって、<xref:Microsoft.VisualStudio.Package.IScanner> インターフェイスを実装するオブジェクトを指定します。

 <xref:Microsoft.VisualStudio.Package.IScanner> スキャナーには、<xref:Microsoft.VisualStudio.Package.IScanner.SetSource%2A> メソッドを使用して 1 行のソース コードが提供されます。 <xref:Microsoft.VisualStudio.Package.IScanner.ScanTokenAndProvideInfoAboutIt%2A> メソッドの呼び出しは、この行のトークンがなくなるまで、行の次のトークンを取得するために繰り返されます。 色付けの場合、MPF では、すべてのソース コードが行のシーケンスとして扱われます。 そのため、スキャナーは、それを行としてとらえるソースに対処できる必要があります。 また、任意の行をいつでもスキャナーに渡すことができます。保証されるのは、スキャナーがスキャン対象の行の前の状態変数を受け取ることだけです。

 <xref:Microsoft.VisualStudio.Package.Colorizer> クラスは、トークン トリガーを識別するためにも使用されます。 これらのトリガーは、特定のトークンが単語補完や対応する中かっこなどのより複雑な操作を開始できることを MPF に伝えます。 このようなトリガーは高速である必要があり、任意の場所で行われる必要があるため、スキャナーはこのタスクに最適です。

 詳細については、[従来の言語サービスでの構文の配色変更](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)に関するページを参照してください。

## <a name="parsing-for-functionality-and-scope"></a>機能とスコープの解析
 機能とスコープの解析には、検出されたトークンの種類の識別だけでなく、より多くの作業が必要になります。 パーサーは、トークンの種類だけでなく、トークンを使用する機能も識別する必要があります。 たとえば、識別子は単なる名前ですが、お使いの言語では、コンテキストによっては識別子がクラス、名前空間、メソッド、または変数の名前である可能性があります。 トークンの一般的な種類は識別子である場合がありますが、識別子は、それが何で、どこに定義されているかによっては、他の意味がある場合もあります。 この識別には、パーサーが解析対象の言語についてのより広範な知識を持っている必要があります。 ここで <xref:Microsoft.VisualStudio.Package.AuthoringSink> クラスの出番です。 <xref:Microsoft.VisualStudio.Package.AuthoringSink> クラスは、識別子、メソッド、対応する言語ペア (中かっこやかっこなど)、言語トリプル ("`foreach()`" "`{`" および "`}`"など、3 つの部分がある点を除いて言語ペアに類似) に関する情報を収集します。 さらに、<xref:Microsoft.VisualStudio.Package.AuthoringSink> クラスをオーバーライドして、コード識別 (ブレークポイントの早期検証で使用して、デバッガーを読み込む必要がないようにする) と、**Autos** デバッグ ウィンドウ (プログラムのデバッグ時にローカルの変数とパラメーターが自動的に表示され、デバッガーが提示するものに加えて、パーサーが適切なローカルの変数とパラメーターを識別ために必要) をサポートすることができます。

 <xref:Microsoft.VisualStudio.Package.AuthoringSink> オブジェクトは <xref:Microsoft.VisualStudio.Package.ParseRequest> オブジェクトの一部としてパーサーに渡され、新しい <xref:Microsoft.VisualStudio.Package.ParseRequest> オブジェクトが作成されるたびに新しい <xref:Microsoft.VisualStudio.Package.AuthoringSink> オブジェクトが作成され ます。 また、<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドは、さまざまな IntelliSense 操作を処理するために使用される <xref:Microsoft.VisualStudio.Package.AuthoringScope> オブジェクトを返す必要があります。 <xref:Microsoft.VisualStudio.Package.AuthoringScope> オブジェクトは、解析の理由に応じて宣言の一覧とメソッドの一覧 (どちらにもデータが設定されている) を保持します。 <xref:Microsoft.VisualStudio.Package.AuthoringScope> クラスを実装する必要があります。

## <a name="see-also"></a>関連項目
- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service1.md)
- [従来の言語サービスの概要](../../extensibility/internals/legacy-language-service-overview.md)
- [従来の言語サービスでの構文の配色変更](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)
- [従来の言語サービスでのかっこの一致](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)
