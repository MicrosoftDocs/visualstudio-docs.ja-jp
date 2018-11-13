---
title: '[オプション]、[テキスト エディター]、[C#]、[詳細]'
ms.date: 10/29/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.CSharp.Outlining
- VS.ToolsOptionsPages.Text_Editor.CSharp.Advanced
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 7cfbc6d57e5bfd3c6a8f317967448039a9b3f5e4
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2018
ms.locfileid: "50670716"
---
# <a name="options-text-editor-c-advanced"></a>[オプション]、[テキスト エディター]、[C#]、[詳細]

**[詳細]** オプションを使って、C# のエディターの書式設定、コードのリファクタリング、および XML ドキュメントのコメントの設定を変更します。 このオプション ページにアクセスするには、**[ツール]** > **[オプション]** を選び、さらに **[テキスト エディター]** > **[C#]** > **[詳細]** の順に選びます。

> [!NOTE]
> ここには、すべてのオプションが一覧されていない可能性があります。

## <a name="analysis"></a>分析

- 完全ソリューション解析を有効にする

   開いているコード ファイルだけでなく、ソリューションのすべてのファイルでコード分析を有効にします。 詳細については、[完全ソリューション解析](../../code-quality/how-to-enable-and-disable-full-solution-analysis-for-managed-code.md)に関するページを参照してください。

## <a name="using-directives"></a>Using ディレクティブ

- using を並べ替える際に、'System' ディレクティブを先頭に配置する

   選択した場合、右クリック メニューの **[using の削除と並べ替え]** コマンドによって `using` ディレクティブが並べ替えられ、'System' 名前空間が一覧の先頭に置かれます。

   並べ替える前:

   ```csharp
   using AutoMapper;
   using FluentValidation;
   using System.Collections.Generic;
   using System.Linq;
   using Newtonsoft.Json;
   using System;
   ```
   
   並べ替えた後:

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using AutoMapper;
   using FluentValidation;
   using Newtonsoft.Json;
   ```
   
- ディレクティブ グループを使用して分離します

   選択した場合、右クリック メニューの **[using の削除と並べ替え]** コマンドによって、同じルート名前空間を持つディレクティブのグループの間に空の行を挿入することで、`using` ディレクティブが分離されます。

   並べ替える前:

   ```csharp
   using AutoMapper;
   using FluentValidation;
   using System.Collections.Generic;
   using System.Linq;
   using Newtonsoft.Json;
   using System;
   ```
   
   並べ替えた後:
   
   ```csharp
   using AutoMapper;
   
   using FluentValidation;
   
   using Newtonsoft.Json;
   
   using System;
   using System.Collections.Generic;
   using System.Linq;
   ```
   
- 参照アセンブリの型に using を提案する 
- NuGet パッケージの型に using を提案する 

   これらのオプションを選択した場合、[クイック アクション](../quick-actions.md)を使用して NuGet パッケージをインストールし、参照されていない型の `using` ディレクティブを追加できます。

   ![Visual Studio に NuGet パッケージをインストールするためのクイック アクション](media/nuget-lightbulb.png)
  
## <a name="highlighting"></a>強調表示

- カーソルの下にあるシンボルへの参照をハイライトする

   シンボル内にカーソルを置いたり、シンボルをクリックしたりすると、コード ファイル内のそのシンボルのすべてのインスタンスが強調表示されます。

## <a name="outlining"></a>アウトライン

- ファイルが開かれたときにアウトライン モードを実行する

   選択すると、コードの折りたたみ可能なブロックを作成するコード ファイルが自動的にアウトラインになります。 初めてファイルが開かれると、#regions ブロックとアクティブでないコード ブロックが折りたたまれます。

- プロシージャ行の区切り記号を表示する

   テキスト エディターに、プロシージャのスコープが表示されます。 プロジェクトの *.vb* ソース ファイルで、次の表に示す場所に線が表示されます。

   |.vb ソース ファイル内の場所|線が表示される場所の例|
   |---------------------------------|------------------------------|
   |ブロック宣言構造の後|-   クラス、構造体、モジュール、インターフェイス、または列挙型の最後<br />-   プロパティ、関数、または sub の後<br />-   プロパティの get 句と set 句の間は対象外|
   |一連の単一行構造|-   import ステートメントの後、クラス ファイルの型定義の前<br />-   クラスで宣言されている変数の後、プロシージャの前|
   |単一行宣言|-   Import ステートメント、Inherits ステートメント、変数宣言、イベント宣言、デリゲート宣言、および DLL の Declare ステートメントの後|

## <a name="editor-help"></a>エディターのヘルプ

- /// が入力されたとき、XML ドキュメントのコメントを生成する

   オンにすると、`///` コメント イントロダクションを入力した後に、XML ドキュメント コメントの XML 要素が挿入されます。 XML ドキュメントの詳細については、「[XXML ドキュメント コメント (C# プログラミング ガイド)](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments)」を参照してください。

## <a name="see-also"></a>関連項目

- [方法: ドキュメント生成のための XML コメントを挿入する](../../ide/reference/generate-xml-documentation-comments.md)
- [XML ドキュメント コメント (C# プログラミング ガイド)](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments)
- [XML コメントによるコードの文書化 (C# ガイド)](/dotnet/csharp/codedoc)
- [言語固有のエディター オプションの設定](../../ide/reference/setting-language-specific-editor-options.md)
- [C# IntelliSense](../../ide/visual-csharp-intellisense.md)
