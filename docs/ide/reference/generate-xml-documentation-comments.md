---
title: "Visual Studio で XML ドキュメントのコメントを挿入する | Microsoft Docs"
ms.custom: 
ms.date: 01/26/2018
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-general
ms.topic: article
author: gewarren
ms.author: gewarren
manager: ghogen
ms.workload:
- dotnet
ms.openlocfilehash: a98373280aa789e3c2381c5afc7d6c60c53dd171
ms.sourcegitcommit: 205d15f4558315e585c67f33d5335d5b41d0fcea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2018
---
# <a name="how-to-insert-xml-comments-for-documentation-generation"></a>方法: ドキュメント生成のための XML コメントを挿入する

Visual Studio では、クラスやメソッドなどのコード要素を文書化しやすいように、標準的な XML ドキュメント コメント構造を自動的に生成できます。 コンパイル時に、ドキュメントのコメントを含む XML ファイルを生成できます。 コンパイラによって生成された XML ファイルは、.NET アセンブリと共に配布できます。これにより、Visual Studio や他の IDE で、IntelliSense を使って型やメンバーに関する概要情報を表示できます。 さらに、[DocFX](https://dotnet.github.io/docfx/) や [Sandcastle](https://www.microsoft.com/download/details.aspx?id=10526) のようなツールを使用して XML ファイルを実行し、API リファレンスの Web サイトを生成することができます。

> [!NOTE]
> XML ドキュメントのコメントを自動的に挿入する **[コメントの挿入]** コマンドは、[C#](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments) と [Visual Basic](/dotnet/visual-basic/programming-guide/program-structure/how-to-create-xml-documentation) で使うことができます。 ただし、[C++ ファイルに XML ドキュメントのコメント](/cpp/ide/xml-documentation-visual-cpp)を手動で挿入し、コンパイル時に XML ドキュメント ファイルを生成することもできます。

## <a name="to-insert-xml-comments-for-a-code-element"></a>コード要素の XML コメントを挿入するには

1. メソッドなど、ドキュメント化する要素の上にテキスト カーソルを置きます。

1. 次のいずれかの操作を行います。

   - C# では「`///`」と入力し、Visual Basic では「`'''`」と入力します

   - **[編集]** メニューから、**[IntelliSense]** > **[コメントの挿入]** の順に選択します

   - コード要素の前面またはすぐ上に表示される右クリック メニューまたはコンテキスト メニューから、**[スニペット]** > **[コメントの挿入]** の順に選択します

   すぐに、XML テンプレートがコード要素の上に生成されます。 たとえば、メソッドのコメントを生成すると、**\<summary\>** 要素、各パラメーターの **\<param\>** 要素、および戻り値を文書化するための **\<returns\>** 要素が生成されます。

   ![XML コメント テンプレート - C#](media/doc-preview-cs.png)

   ![XML コメント テンプレート - Visual Basic](media/doc-preview-vb.png)

1. 各 XML 要素の説明を入力し、コード要素を完全に文書化します。

   ![完了したコメント](media/doc-result-cs.png)

> [!NOTE]
> `///` (C#) または `'''` (Visual Basic) を入力した後で XML ドキュメントのコメントを切り替えるための[オプション](../../ide/reference/options-text-editor-csharp-advanced.md)があります。 メニュー バーから **[ツール]** > **[オプション]** の順に選択して、**[オプション]** ダイアログ ボックスを開きます。 次に、**[テキスト エディター]** > **[C#]** または **[Basic]** > **[詳細]** の順に移動します。 **[エディターのヘルプ]** セクションで、**[XML ドキュメントを生成する]** オプションを探します。

## <a name="see-also"></a>関連項目

[XML ドキュメント コメント (C# プログラミング ガイド)](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments)  
[XML コメントによるコードの文書化 (C# ガイド)](/dotnet/csharp/codedoc)  
[方法: XML ドキュメントを作成する (Visual Basic)](/dotnet/visual-basic/programming-guide/program-structure/how-to-create-xml-documentation)  
[C++ のコメント](/cpp/cpp/comments-cpp)  
[XML ドキュメント (C++)](/cpp/ide/xml-documentation-visual-cpp)  
[コード生成](../code-generation-in-visual-studio.md)
