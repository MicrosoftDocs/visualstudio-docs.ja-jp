---
title: "コード スニペット | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-general
ms.topic: article
f1_keywords:
- vs.ExpansionManagerImport
- vs.codesnippetmanager
helpviewer_keywords:
- surround with
- code snippets
author: gewarren
ms.author: gewarren
manager: ghogen
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.openlocfilehash: 514408ff2dbbde12d243a1458c380a2e17b516cc
ms.sourcegitcommit: 205d15f4558315e585c67f33d5335d5b41d0fcea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2018
---
# <a name="code-snippets"></a>コード スニペット

コードスニペットは、コンテキスト メニュー コマンドまたはホット キーの組み合わせを使用してコード ファイルに挿入できる、再利用可能なコードの小さなブロックです。 通常、スニペットには `try-finally` や `if-else` などのよく使われるコード ブロックが含まれていますが、スニペットを使ってクラス全体またはメソッド全体を挿入することもできます。

コード スニペットは、C#、C++、Visual Basic、XML、T-SQL など、多数の言語で利用できます。 ある言語で使用可能なすべてのインストール済みスニペットを表示するには、Visual Studio で **[ツール]** メニューの **[コード スニペット マネージャー]** を開き、上部のドロップダウン メニューから言語を選択します。

![[コード スニペット マネージャー] ダイアログ ボックス](media/code-snippets-manager.png)

コード スニペットは、次の一般的な方法でアクセスできます。

- メニュー バーで、**[編集]** > **[IntelliSense]** > **[スニペットの挿入]** の順に選択します

- コード エディターの右クリック メニューまたはコンテキスト メニューから、**[スニペット]** > **[スニペットの挿入]** を選択します

- キーボードで **Ctrl** + **K** + **X** キーを押します

## <a name="expansion-snippets-and-surround-with-snippets"></a>拡張スニペットとブロックの挿入用スニペット

Visual Studio には、2 種類のコード スニペットがあります。1 つ目は、指定した挿入ポイントに追加され、スニペット ショートカットを置換できる拡張スニペットで、2 つ目は、選択したコード ブロックの周囲に追加される、ブロックの挿入用スニペット (C# および C++ のみ) です。

拡張スニペットの例: C# では、ショートカット tryf は try-finally ブロックの挿入に使用されます。

```csharp
try
{

}
finally
{

}
```

このスニペットを挿入するには、コード ウィンドウのコンテキスト メニューで **[スニペットの挿入]** をクリックしてから、**[Visual C#]** をクリックし、「`tryf`」と入力して、**Tab** キーを押します。または、「`tryf`」と入力して **Tab** キーを 2 回押します。

ブロックの挿入用スニペットの例: C++ では、ショートカット `if` は挿入スニペットまたはブロックの挿入用スニペットとして使用できます。 コード行 (例: `return FALSE;`) を選択した場合は、**[ブロックの挿入]** > **[if]** を選択すると、行の周りにスニペットが展開されます。

```cpp
if (true)
{
    return FALSE;
}
```

## <a name="snippet-replacement-parameters"></a>スニペットの置換パラメーター

スニペットには置換パラメーターを含めることができます。置換パラメーターとは、作成中の実際のコードに応じた置換を必要とするプレースホルダーです。 前の例で、`true` は置換パラメーターであり、適切な条件への置換が必要です。 置換を行うと、スニペット内の同じ置換パラメーターのすべてのインスタンスでもこれが繰り返されます。

たとえば、Visual Basic には、プロパティを挿入するコード スニペットがあります。 スニペットを挿入するには、Visual Basic コード ファイルの右クリック メニューまたはコンテキスト メニューから **[スニペット]** > **[スニペットの挿入]** を選択します。 続いて、**[コード パターン]** > **[プロパティ、プロシージャ、イベント]** > **[プロパティの定義]** の順に選択します。

![[プロパティの定義] のコード スニペット メニュー](media/code-snippets-vb-property.png)

次のコードが挿入されます。

```vb
Private newPropertyValue As String
Public Property NewProperty() As String
    Get
        Return newPropertyValue
    End Get
    Set(ByVal value As String)
        newPropertyValue = value
    End Set
End Property
```

`newPropertyValue` を `m_property` に変更すると、`newPropertyValue` のすべてのインスタンスが変更されます。 プロパティ宣言の `String` を `Int` に変更すると、set メソッド内の値も `Int` に変更されます。

## <a name="see-also"></a>関連項目

[チュートリアル: コード スニペットを作成する](../ide/walkthrough-creating-a-code-snippet.md)  
[方法: コード スニペットを配布する](../ide/how-to-distribute-code-snippets.md)  
[コード スニペットを使用するためのベスト プラクティス](../ide/best-practices-for-using-code-snippets.md)  
[スニペットのトラブルシューティング](../ide/troubleshooting-snippets.md)  
[C# コード スニペット](../ide/visual-csharp-code-snippets.md)  
[Visual C++ のコード スニペット](../ide/visual-cpp-code-snippets.md)  
[コード スニペット スキーマ リファレンス](../ide/code-snippets-schema-reference.md)