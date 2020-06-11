---
title: 変数を確認する - [自動変数] ウィンドウと [ローカル] ウィンドウ | Microsoft Docs
ms.custom: seodec18
ms.date: 10/18/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.autos
- vs.debug.locals
helpviewer_keywords:
- debugger, variable windows
- debugging [Visual Studio], variable windows
ms.assetid: bb6291e1-596d-4af0-9f22-5fd713d6b84b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b159f631534135ac568fb03dbffa46ae0360fc47
ms.sourcegitcommit: 0b90e1197173749c4efee15c2a75a3b206c85538
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2019
ms.locfileid: "74904098"
---
# <a name="inspect-variables-in-the-autos-and-locals-windows"></a>[自動変数] ウィンドウと [ローカル] ウィンドウで変数を確認する

デバッグしている間、 **[自動変数]** ウィンドウと **[ローカル]** ウィンドウに変数の値が表示されます。 こウィンドウは、デバッグ セッション中にのみ使用できます。 **[自動変数]** ウィンドウには、現在のブレークポイントに関連して使用される変数が表示されます。 **[ローカル]** ウィンドウには、ローカル スコープ (通常は現在の関数またはメソッド) で定義されている変数が表示されます。 コードのデバッグを試みるのが今回初めてである場合は、この記事を先に進む前に「[入門者向けのデバッグ](../debugger/debugging-absolute-beginners.md)」および「[デバッグの技術とツール](../debugger/write-better-code-with-visual-studio.md)」を参照することをお勧めします。

 **[自動変数]** ウィンドウは、C#、Visual Basic、C++、および Python コードで使用できますが、JavaScript または F# では使用できません。

デバッグ中に **[自動変数]** ウィンドウを開くには、 **[デバッグ]**  >  **[ウィンドウ]**  >  **[自動変数]** を選択するか、**Ctrl**+**Alt**+**V** > **A** を押します。

デバッグ中に **[ローカル]** ウィンドウを開くには、 **[デバッグ]**  >  **[ウィンドウ]**  >  **[ローカル]** を選択するか、**Alt**+**4** を押します。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、[Visual Studio for Mac でのデータの視覚化](/visualstudio/mac/data-visualizations)に関するページを参照してください。

## <a name="use-the-autos-and-locals-windows"></a>[自動変数] ウィンドウと [ローカル] ウィンドウを使用する

配列とオブジェクトは、 **[自動変数]** ウィンドウと **[ローカル]** ウィンドウにツリー コントロールで表示されます。 変数名の左側にある矢印を選択するとビューが展開され、フィールドとプロパティが表示されます。 以下に、 **[ローカル]** ウィンドウに表示されている <xref:System.IO.FileStream?displayProperty=fullName> オブジェクトの例を示します。

![Locals-FileStream](../debugger/media/locals-filestream.png "Locals-FileStream")

**[ローカル]** または **[自動変数]** ウィンドウの赤い値は、最後の評価移行に値が変更されたことを意味します。 この変更は前のデバッグ セッションに由来する場合もあれば、ユーザーがウィンドウで値を変更したための場合もあります。

デバッガー ウィンドウの既定の数値書式は 10 進数です。 16 進数に変更するには、 **[ローカル]** または **[自動変数]** ウィンドウ内で右クリックし、 **[16 進数で表示]** を選びます。 この変更は、すべてのデバッガー ウィンドウに反映されます。

## <a name="edit-variable-values-in-the-autos-or-locals-window"></a>[自動変数] ウィンドウまたは [ローカル] ウィンドウで変数の値を編集する

**[自動変数]** または **[ローカル]** ウィンドウのほとんどの変数の値を編集するには、値をダブルクリックして、新しい値を入力します。

たとえば `a + b`のように、値に式を入力することもできます。 デバッガーは、正しい言語式であれば大部分を受け入れます。

ネイティブの C++ コードでは、変数名のコンテキストを修飾しなければならない場合があります。 詳細については、[コンテキスト演算子 (C++)](../debugger/context-operator-cpp.md) に関するページを参照してください。

>[!CAUTION]
>値や式を変更する前に、結果を理解する必要があります。 考えられる問題のいくつかを次に示します。
>
>- 式を評価すると、変数の値が変わる場合や、プログラムの状態に影響が及ぶ場合があります。 たとえば、 `var1 = ++var2` を評価すると `var1` と `var2` 両方の値が変更されます。 このような式には、[副作用](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\))があると言われます。 副作用に気付いていないと、そのために予期しない結果が発生する可能性があります。
>
>- 浮動小数点値を編集すると、小数部分の 10 進とバイナリの変換により、多少の誤差が発生する場合があります。 特に影響のないように見える編集でも、浮動小数点値の一部のビットが変化する場合があります。

::: moniker range=">= vs-2019" 
## <a name="search-in-the-autos-or-locals-window"></a>[自動変数] ウィンドウまたは [ローカル] ウィンドウで検索する

各ウィンドウの上にある検索バーを使用して、 **[自動変数]** ウィンドウまたは **[ローカル]** ウィンドウの [名前]、[値]、[種類] 列でキーワードを検索できます。 Enter キーを押すか、いずれかの矢印を選択して検索を実行します。 進行中の検索を取り消すには、検索バーの [x] アイコンを選択します。

検出された一致の間を移動するには、左矢印と右矢印 (それぞれ、Shift + F3 キーと F3 キー) を使用します。

![[ローカル] ウィンドウでの検索](../debugger/media/ee-search-locals.png "[ローカル] ウィンドウでの検索")

検索の詳細さを変更するには、 **[自動変数]** または **[ローカル]** ウィンドウの上部にある **[詳細検索]** ドロップダウンを使用して、入れ子になったオブジェクトを検索するレベルの深さを選択します。 

## <a name="pin-properties-in-the-autos-or-locals-window"></a>[自動変数] ウィンドウまたは [ローカル] ウィンドウでプロパティをピン留めする

> [!NOTE]
> この機能は、.NET Core 3.0 以降でサポートされています。

**ピン留め可能なプロパティ** ツールを使用して、[自動変数] および [ローカル] ウィンドウでオブジェクトをプロパティごとにすばやく調べることができます。  このツールを使用するには、プロパティをポイントして、表示される画鋲のアイコンを選択するか、右クリックし、表示されるコンテキスト メニューの **[メンバーをお気に入りとしてピン留め]** オプションを選択します。  これにより、そのプロパティがオブジェクトのプロパティ リストの先頭に表示され、プロパティの名前と値が **[値]** 列に表示されます。  プロパティの固定を解除するには、画鋲のアイコンをもう一度選択するか、コンテキスト メニューの **[メンバーをお気に入りから削除]** オプションを選択します。

![[ローカル] ウィンドウでのプロパティをピン留め](../debugger/media/basic-pin.gif "[ローカル] ウィンドウでのプロパティをピン留め")

また、[自動変数] または [ローカル] ウィンドウでオブジェクトのプロパティ リストを表示するときに、プロパティ名を切り替えたり、ピン留めされていないプロパティをフィルターで除外したりすることもできます。  各オプションにアクセスするには、[自動変数] または [ローカル] ウィンドウの上のツール バーにあるボタンを選択します。

![お気に入りのプロパティのフィルター](../debugger/media/filter-pinned-properties-locals.png "お気に入りのプロパティのフィルター")
![プロパティ名の切り替え](../debugger/media/toggle-property-names.gif "プロパティ名の切り替え")

::: moniker-end

## <a name="change-the-context-for-the-autos-or-locals-window"></a>[自動変数] ウィンドウまたは [ローカル] ウィンドウのコンテキストを変更する

**[デバッグの場所]** ツール バーを使用して、必要な関数、スレッド、またはプロセスを選択できます。これによって、 **[自動変数]** ウィンドウと **[ローカル]** ウィンドウのコンテキストが変更されます。

**[デバッグの場所]** ツール バーを有効にするには、ツール バー領域の何もない部分をクリックし、ドロップダウンから **[デバッグの場所]** を選択するか、 **[表示]**  >  **[ツール バー]**  >  **[デバッグの場所]** を選択します。

ブレークポイントを設定し、デバッグを開始します。 ブレークポイントにヒットすると、実行が一時停止し、 **[デバッグの場所]** ツール バーで場所を確認できます。

![[デバッグの場所] ツール バー](../debugger/media/debuglocationtoolbar.png "[デバッグの場所] ツール バー")

## <a name="variables-in-the-autos-window-c-c-visual-basic-python"></a><a name="bkmk_whatvariables"></a> [自動変数] ウィンドウの変数 (C#、C++、Visual Basic、Python)

異なるコード言語によってさまざまな変数が **[自動変数]** ウィンドウに表示されます。

- C# および Visual Basic では、 **[自動変数]** ウィンドウに現在の行または前の行に使用されている変数がすべて表示されます。 たとえば、C# または Visual Basic コードでは、次の 4 つの変数を宣言します。

   ```csharp
       public static void Main()
       {
          int a, b, c, d;
          a = 1;
          b = 2;
          c = 3;
          d = 4;
       }
   ```

   `c = 3;` 行内にブレークポイントを設定し、デバッガーを開始します。 実行が一時停止すると、 **[自動変数]** ウィンドウに次のように表示されます。

   ![Autos-CSharp](../debugger/media/autos-csharp.png "Autos-CSharp")

   `c` の値が 0 です。これは、行 `c = 3` がまだ実行されていないからです。

- C++ では、現在の行 (実行が一時停止した行) の前の少なくとも 3 行で使用された変数が **[自動変数]** ウィンドウに表示されます。 たとえば、C++ コードで 6 個の変数を宣言します。

   ```C++
       void main() {
           int a, b, c, d, e, f;
           a = 1;
           b = 2;
           c = 3;
           d = 4;
           e = 5;
           f = 6;
       }
   ```

    `e = 5;` 行内にブレークポイントを設定し、デバッガーを実行します。 実行が停止すると、 **[自動変数]** ウィンドウに次のように表示されます。

    ![Autos-C++](../debugger/media/autos-cplus.png "Autos-C++")

    変数 `e`が初期化されていないことにご注意ください。これは行 `e = 5` がまだ実行されていないからです。

## <a name="view-return-values-of-method-calls"></a><a name="bkmk_returnValue"></a> View return values of method calls
 .NET および C++ のコードでは、メソッド呼び出しのステップ オーバーまたはステップ アウトをするときに **[自動変数]** ウィンドウで戻り値を確認できます。 メソッド呼び出しの戻り値の確認は、それらがローカル変数に格納されていない場合に便利です。 メソッドは、パラメーターとして使用されることも、別のメソッドの戻り値として使用されることもあります。

 たとえば、次の C# コードは、2 つの関数の戻り値を加算します。

```csharp
static void Main(string[] args)
{
    int a, b, c, d;
    a = 1;
    b = 2;
    c = 3;
    d = 4;
    int x = sumVars(a, b) + subtractVars(c, d);
}

private static int sumVars(int i, int j)
{
    return i + j;
}

private static int subtractVars(int i, int j)
{
    return j - i;
}
```

`sumVars()` および `subtractVars()` メソッド呼び出しの戻り値を [自動変数] ウィンドウで確認するには:

1. `int x = sumVars(a, b) + subtractVars(c, d);` の行にブレークポイントを設定します。

1. デバッグを開始し、ブレークポイントで実行が一時停止したとき、 **[ステップ オーバー]** を選択するか **F10** キーを押します。 **[自動変数]** ウィンドウに戻り値が次のように表示されます。

  ![[自動変数] の C# の戻り値](../debugger/media/autosreturnvaluecsharp2.png "[自動変数] の C# の戻り値")

## <a name="see-also"></a>関連項目

- [デバッグとは](../debugger/what-is-debugging.md)
- [デバッグの技術とツール](../debugger/write-better-code-with-visual-studio.md)
- [デバッグの概要](../debugger/debugger-feature-tour.md)
- [デバッガー ウィンドウ](../debugger/debugger-windows.md)
