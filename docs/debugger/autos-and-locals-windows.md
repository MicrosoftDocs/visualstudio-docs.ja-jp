---
title: -変数の調査 [自動変数] と [ローカル] ウィンドウ |Microsoft Docs
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
ms.openlocfilehash: 60bb98644c1905b030176b28b97575b379bed38d
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60103096"
---
# <a name="inspect-variables-in-the-autos-and-locals-windows"></a>[自動変数] と [ローカル] ウィンドウに変数を検査します。

**[自動変数]** と**ローカル**windows は、デバッグ中に変数の値を表示します。 Windows はデバッグ セッション中にのみ使用できます。 **[自動変数]** ウィンドウには、現在のブレークポイントを使用する変数が表示されます。 **ローカル**ウィンドウには、現在の関数またはメソッドは、通常は、ローカル スコープで定義された変数が表示されます。 コードをデバッグしようとした初めての場合は、読み取りをする可能性があります[超初心者向けのデバッグ](../debugger/debugging-absolute-beginners.md)と[手法とツールをデバッグ](../debugger/write-better-code-with-visual-studio.md)にこの記事に進む前にします。

 **[自動変数]** ウィンドウが使用できるC#、Visual Basic、C++、および Python コードでは、JavaScript ではなくまたはF#します。

開くには、 **[自動変数]** ウィンドウで、デバッグ中に、**デバッグ** > **Windows** > **[自動変数]**、またはキーを押します**Ctrl**+**Alt**+**V** > **A**します。

開くには、**ローカル**ウィンドウで、デバッグ中に、**デバッグ** > **Windows** > **ローカル**、またはキーを押します**Alt**+**4**します。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac では、次を参照してください。 [Visual studio for Mac のデータの視覚化](/visualstudio/mac/data-visualizations)します。

## <a name="use-the-autos-and-locals-windows"></a>[自動変数] と [ローカル] ウィンドウを使用します。

配列とオブジェクトの表示で、 **[自動変数]** と**ローカル**ツリーのコントロールとして windows。 フィールドとプロパティを表示するビューを展開する変数名の左側にある矢印を選択します。 次の例に示します、<xref:System.IO.FileStream?displayProperty=fullName>オブジェクト、**ローカル**ウィンドウ。

![Locals-FileStream](../debugger/media/locals-filestream.png "Locals-FileStream")

赤の値で、**ローカル**または **[自動変数]** ウィンドウは、値が、最後の評価から変更されたことを意味します。 前のデバッグ セッションから、変更可能性がありますまたはウィンドウで値を変更したためです。

デバッガー ウィンドウで既定の数値書式指定は decimal です。 これを 16 進数を変更するのには右クリック、**ローカル**または **[自動変数]** ウィンドウと選択**16 進数の表示**します。 この変更では、すべてのデバッガー ウィンドウに影響します。

## <a name="edit-variable-values-in-the-autos-or-locals-window"></a>[自動変数] または [ローカル] ウィンドウで変数の値を編集します。

ほとんどの変数の値を編集する、 **[自動変数]** または**ローカル**windows は、値をダブルクリックし、新しい値を入力します。

たとえば `a + b`のように、値に式を入力することもできます。 デバッガーは、正しい言語式であれば大部分を受け入れます。

ネイティブの C++ コードでは、変数名のコンテキストを修飾しなければならない場合があります。 詳細については、[コンテキスト演算子 (C++)](../debugger/context-operator-cpp.md) に関するページを参照してください。

>[!CAUTION]
>値と式を変更する前に、結果を理解することを確認します。 いくつか考えられる問題は次のとおりです。
>
>- 式を評価すると、変数の値が変わる場合や、プログラムの状態に影響が及ぶ場合があります。 たとえば、評価`var1 = ++var2`両方の値を変更`var1`と`var2`します。 これらの式といいますが[副作用](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\))します。 副作用で、それらを認識していない場合、予期しない結果が生じる場合があります。
>
>- 浮動小数点値を編集すると、小数部分の 10 進とバイナリの変換により、多少の誤差が発生する場合があります。 一見無害の編集もバイトが、浮動小数点変数のビットの一部に変更します。

::: moniker range=">= vs-2019" 
## <a name="search-in-the-autos-or-locals-window"></a>[自動変数] または [ローカル] ウィンドウで検索します。

名前、値、および型の列に含まれるキーワードを検索することができます、 **[自動変数]** または**ローカル**各ウィンドウの上部の検索バーを使用してウィンドウ。 ENTER キーまたは検索を実行する矢印のいずれかを選択します。 進行中の検索をキャンセルするには、検索バーに"x"アイコンを選択します。

左と右矢印を使用して (Shift + F3 および F3、それぞれ) 間を移動する一致が見つかりました。

![[ローカル] ウィンドウで検索](../debugger/media/ee-search-locals.png "[ローカル] ウィンドウで検索")

検索をより小さいか完全に利用できるように、**検索より深い**の上部にあるドロップダウン リスト、 **[自動変数]** または**ローカル**ウィンドウに検索するレベルの深さを選択します。入れ子になったオブジェクト。 

::: moniker-end

## <a name="change-the-context-for-the-autos-or-locals-window"></a>[自動変数] または [ローカル] ウィンドウのコンテキストを変更します。

使用することができます、**デバッグの場所**必要な関数、スレッド、またはのコンテキストを変更するには、プロセスを選択するにはツールバー、 **[自動変数]** と**ローカル**windows。

有効にする、**デバッグの場所**ツールバーで、 をクリックし、ツールバー領域の空の部分で**デバッグの場所**ドロップダウンで、または選択から**ビュー**  >  **ツールバー** > **デバッグの場所**します。

ブレークポイントを設定し、デバッグを開始します。 実行の一時停止しては、内の場所を表示できます、ブレークポイントにヒットしたときに、**デバッグの場所**ツールバー。

![[デバッグの場所] ツールバー](../debugger/media/debuglocationtoolbar.png "デバッグの場所 ツールバー")

## <a name="bkmk_whatvariables"></a> [自動変数] ウィンドウで変数 (C#、C++、Visual Basic、Python)

別のコードの言語での異なる変数を表示する、 **[自動変数]** ウィンドウ。

- C# および Visual Basic では、**[自動変数]** ウィンドウに現在の行または前の行に使用されている変数がすべて表示されます。 たとえば、C#または Visual Basic のコードは、次の 4 つの変数を宣言します。

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

   行にブレークポイントを設定`c = 3;`、し、デバッガーを起動します。 実行が一時停止したときに、 **[自動変数]** ウィンドウに表示されます。

   ![[自動変数] CSharp](../debugger/media/autos-csharp.png "CSharp の [自動変数]")

   値`c`なので、行`c = 3`実行されていません。

- C++ では、 **[自動変数]** ウィンドウには、実行が一時停止している現在の行の前に少なくとも 3 つの行で使用される変数が表示されます。 たとえば、C++ コードでは、6 つの変数を宣言します。

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

    行にブレークポイントを設定`e = 5;`し、デバッガーを実行します。 実行が停止したとき、 **[自動変数]** ウィンドウに表示されます。

    ![[自動変数] C++](../debugger/media/autos-cplus.png "[自動変数] C++")

    変数`e`ために、初期化、されていない行`e = 5`が実行されていません。

## <a name="bkmk_returnValue"></a> View return values of method calls
 .NET および C++ のコードでの戻り値を確認することができます、 **[自動変数]** ステップ上またはメソッドの呼び出しからステップするときにウィンドウ。 表示メソッドの呼び出しを返す、ローカル変数に保存されていない場合、値が役に立ちます。 メソッドは、パラメーター、または別のメソッドの戻り値として使用できます。

 たとえば、次C#コードは、2 つの関数の戻り値を追加します。

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

戻り値を表示する、`sumVars()`と`subtractVars()`メソッドの呼び出しで、[自動変数] ウィンドウ。

1. `int x = sumVars(a, b) + subtractVars(c, d);` の行にブレークポイントを設定します。

1. デバッグを開始し、実行がブレークポイントで一時停止したときに選択**ステップ オーバー**またはキーを押します**F10**します。 次の戻り値を表示する必要があります、 **[自動変数]** ウィンドウ。

  ![[自動変数] は値を返すC# ](../debugger/media/autosreturnvaluecsharp2.png "戻り値を [自動変数]C#")

## <a name="see-also"></a>関連項目

- [デバッグとは](../debugger/what-is-debugging.md)
- [デバッグの技術とツール](../debugger/write-better-code-with-visual-studio.md)
- [デバッグの概要](../debugger/debugger-feature-tour.md)
- [デバッガー ウィンドウ](../debugger/debugger-windows.md)
