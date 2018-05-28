---
title: for ループを foreach ステートメントに変換するためのコードのリファクタリング
ms.date: 05/10/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 6a200874cec92fada17c13eb45e226ce26119a60
ms.sourcegitcommit: 209c2c068ff0975994ed892b62aa9b834a7f6077
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2018
---
# <a name="refactoring-to-convert-between-a-for-loop-and-a-foreach-statement"></a>for ループと foreach ステートメント間で変換するためのリファクタリング

この記事では、2 つのループ構造を変換するクイック アクション リファクタリングについて説明します。 コード内の [for](/dotnet/csharp/language-reference/keywords/for) ループと [foreach](/dotnet/csharp/language-reference/keywords/foreach-in) ステートメントを切り替える必要がある場合にはいくつかの理由があります。

## <a name="convert-a-for-loop-to-a-foreach-statement"></a>for ループを foreach ステートメントに変換する

コード内に [for](/dotnet/csharp/language-reference/keywords/for) ループがある場合、このリファクタリングを使用してそれを [foreach](/dotnet/csharp/language-reference/keywords/foreach-in) ステートメントに変換できます。

このリファクタリングは以下に適用されます。

- C#

> [!NOTE]
> **['foreach' に変換]** クイック アクション リファクタリングは、初期化子、条件、反復子の 3 つの部分をすべて含む [for](/dotnet/csharp/language-reference/keywords/for) ループに対してのみ使用できます。

### <a name="why-convert"></a>変換する理由

[for](/dotnet/csharp/language-reference/keywords/for) ループを [foreach](/dotnet/csharp/language-reference/keywords/foreach-in) ステートメントに変換する理由には、次のものがあります。

- 項目にアクセスするインデックスとして使用する場合を除き、ループ内でローカル ループ変数を使用しない。

- コードを簡略化して、初期化子、条件、反復子セクションの論理エラーの可能性を軽減したい。

### <a name="how-to-use-it"></a>使用方法

1. `for` キーワード内にキャレットを配置します。

1. 行の任意の場所で **Ctrl**+**.** キーを押すと、 またはコード ファイルの余白でねじ回し ![ねじ回しアイコン](../media/screwdriver-icon.png) アイコンをクリックします。

   ![['foreach' に変換] メニュー](media/convert-to-foreach.png)

1. **['foreach' に変換]** を選択します。 または、**[変更のプレビュー]** を選択して [[変更のプレビュー]](../../ide/preview-changes.md) ダイアログを開いて **[適用]** を選択します。

## <a name="convert-a-foreach-statement-to-a-for-loop"></a>foreach ステートメントを for ループに変換する

コード内に [foreach (C#)](/dotnet/csharp/language-reference/keywords/foreach-in) または [For Each...Next (Visual Basic)](/dotnet/visual-basic/language-reference/statements/for-each-next-statement) ステートメントがある場合、このリファクタリングを使用してそれを [for](/dotnet/csharp/language-reference/keywords/for) ループに変換できます。

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

### <a name="why-convert"></a>変換する理由

[foreach](/dotnet/csharp/language-reference/keywords/foreach-in) ステートメントを [for](/dotnet/csharp/language-reference/keywords/for) ループに変換する理由には、次のものがあります。

- 項目にアクセスするだけでなく、ループ内でローカル ループ変数を使用したい。

- [多次元配列を反復処理していて](/dotnet/csharp/programming-guide/arrays/using-foreach-with-arrays)、配列要素をさらに制御したい。

### <a name="how-to-use-it"></a>使用方法

1. `foreach` または `For Each` キーワード内にキャレットを配置します。

1. 行の任意の場所で **Ctrl**+**.** キーを押すと、 またはコード ファイルの余白でねじ回し ![ねじ回しアイコン](../media/screwdriver-icon.png) アイコンをクリックします。

   ![['for' に変換] メニュー](media/convert-to-for.png)

1. **['for' に変換]** を選択します。 または、**[変更のプレビュー]** を選択して [[変更のプレビュー]](../../ide/preview-changes.md) ダイアログを開いて **[適用]** を選択します。

1. リファクタリングにより新しい反復回数変数が導入されるため、エディターの右上隅に **[名前を変更]** ボックスが表示されます。 変数に別の名前を選択する場合は、その名前を入力してから、**Enter** キーを押すか、**[名前を変更]** ボックスで **[適用]** を選択します。 新しい名前を選択しない場合は、**Esc** キーを押すか、**[適用]** を選択して、**[名前を変更]** ボックスを閉じます。

> [!NOTE]
> C# の場合、これらのリファクタリングによって生成されるコードでは、コレクション内の項目の型には明示的な型または [var](/dotnet/csharp/language-reference/keywords/var) が使われます。 生成されるコードが明示的または暗黙的のどちらになるかは、スコープ内にのコード スタイルの設定によって決まります。 これらの特定のコード スタイルの設定は、コンピューター レベルの **[ツール]** > **[オプション]** > **[テキスト エディター]** > **[C#]** > **[コード スタイル]** > **[全般]** > **[\'var' を優先]** で、またはソリューション レベルの [EditorConfig](../../ide/editorconfig-code-style-settings-reference.md#implicit-and-explicit-types) ファイルで構成します。 コード スタイルの設定を **[オプション]** で変更した場合、変更を有効にするにはコード ファイルを開きなおします。

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)