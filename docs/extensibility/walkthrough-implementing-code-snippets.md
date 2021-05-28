---
title: 'チュートリアル: コード スニペットの実装 | Microsoft Docs'
description: コード スニペットを作成して、エディター拡張機能に含めることができます。 このチュートリアルでは、コード スニペットを作成および登録する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: adbc5382-d170-441c-9fd0-80faa1816478
author: leslierichardson95
ms.author: lerich
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- vssdk
ms.openlocfilehash: b21a7515f7ad4bad74088b6b580a4a3122a2e12a
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216983"
---
# <a name="walkthrough-implement-code-snippets"></a>チュートリアル: コード スニペットを実装する
コード スニペットを作成してエディター拡張機能に含めると、拡張機能のユーザーがそれらを自分のコードに追加できるようになります。

 コード スニペットは、ファイルに組み込むことができるコードまたはその他のテキストの断片です。 特定のプログラミング言語用に登録されているすべてのスニペットを表示するには、 **[ツール]** メニューの **[コード スニペット マネージャー]** をクリックします。 スニペットをファイルに挿入するには、スニペットを配置する場所を右クリックし、[スニペットの挿入] または **[ブロックの挿入]** をクリックして、目的のスニペットを見つけてダブルクリックします。 **Tab** キーまたは **Shift**+**Tab** キーを押して、スニペットの関連部分を変更した後、**Enter** キーまたは **Esc** キーを押して変更を受け入れます。 詳しくは、「[コード スニペット](../ide/code-snippets.md)」をご覧ください。

 コード スニペットは、.snippet* というファイル名拡張子を持つ XML ファイルに格納されます。 スニペットには、スニペットの挿入後に強調表示されるフィールドを含めることができます。これにより、ユーザーはそれらを見つけて変更できるようになります。 スニペット ファイルでは、**コード スニペット マネージャー** 用の情報も提供されます。これにより、スニペット名が正しいカテゴリに表示されるようになります。 スニペット スキーマについて詳しくは、「[コード スニペット スキーマ リファレンス](../ide/code-snippets-schema-reference.md)」をご覧ください。

 このチュートリアルでは、次のタスクを実行する方法を説明します。

1. 特定の言語用のコード スニペットを作成して登録します。

2. **[スニペットの挿入]** コマンドをショートカット メニューに追加します。

3. スニペット拡張を実装します。

   このチュートリアルは、[「チュートリアル: 入力候補の表示](../extensibility/walkthrough-displaying-statement-completion.md)」に基づいています。

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-and-register-code-snippets"></a>コードスニペットを作成して登録する
 通常、コード スニペットは、登録されている言語サービスに関連付けられます。 ただし、コード スニペットを登録するために <xref:Microsoft.VisualStudio.Package.LanguageService> を実装する必要はありません。 代わりに、スニペットのインデックス ファイルで GUID を指定し、プロジェクトに追加する <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute> で同じ GUID を使用します。

 次の手順では、コード スニペットを作成し、特定の GUID に関連付ける方法を示します。

1. 次のディレクトリ構造を作成します。

    **%InstallDir%\TestSnippets\Snippets\1033\\**

    ここで、 *%InstallDir%* は Visual Studio のインストール フォルダーです (通常は、このパスがコード スニペットのインストールに使用されますが、任意のパスを指定することもできます)。

2. \1033\ フォルダーで、 *.xml* ファイルを作成し、名前を **TestSnippets.xml** と指定します。 (通常は、この名前がスニペットのインデックス ファイルに使用されますが、ファイル名拡張子が *.xml* であれば、任意の名前を指定することもできます)。次のテキストを追加し、プレースホルダー GUID を削除して、独自の GUID を追加します。

   ```xml
   <?xml version="1.0" encoding="utf-8" ?>
   <SnippetCollection>
       <Language Lang="TestSnippets" Guid="{00000000-0000-0000-0000-000000000000}">
           <SnippetDir>
               <OnOff>On</OnOff>
               <Installed>true</Installed>
               <Locale>1033</Locale>
               <DirPath>%InstallRoot%\TestSnippets\Snippets\%LCID%\</DirPath>
               <LocalizedName>Snippets</LocalizedName>
           </SnippetDir>
       </Language>
   </SnippetCollection>
   ```

3. スニペット フォルダー内にファイルを作成し、名前を **test**`.snippet` と指定して、次のテキストを追加します。

   ```xml
   <?xml version="1.0" encoding="utf-8" ?>
   <CodeSnippets  xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
       <CodeSnippet Format="1.0.0">
           <Header>
               <Title>Test replacement fields</Title>
               <Shortcut>test</Shortcut>
               <Description>Code snippet for testing replacement fields</Description>
               <Author>MSIT</Author>
               <SnippetTypes>
                   <SnippetType>Expansion</SnippetType>
               </SnippetTypes>
           </Header>
           <Snippet>
               <Declarations>
                   <Literal>
                     <ID>param1</ID>
                       <ToolTip>First field</ToolTip>
                       <Default>first</Default>
                   </Literal>
                   <Literal>
                       <ID>param2</ID>
                       <ToolTip>Second field</ToolTip>
                       <Default>second</Default>
                   </Literal>
               </Declarations>
               <References>
                  <Reference>
                      <Assembly>System.Windows.Forms.dll</Assembly>
                  </Reference>
               </References>
               <Code Language="TestSnippets">
                   <![CDATA[MessageBox.Show("$param1$");
        MessageBox.Show("$param2$");]]>
               </Code>
           </Snippet>
       </CodeSnippet>
   </CodeSnippets>
   ```

   次の手順は、コード スニペットの登録方法を示しています。

### <a name="to-register-code-snippets-for-a-specific-guid"></a>特定の GUID のコード スニペットを登録するには

1. **CompletionTest** プロジェクトを開きます。 このプロジェクトの作成方法について詳しくは、「[チュートリアル: 入力候補の表示](../extensibility/walkthrough-displaying-statement-completion.md)」をご覧ください。

2. プロジェクトで、次のアセンブリへの参照を追加します。

    - Microsoft.VisualStudio.TextManager.Interop

    - Microsoft.VisualStudio.TextManager.Interop.8.0

    - microsoft.msxml

3. プロジェクトで、**source.extension.vsixmanifest** ファイルを開きます。

4. **[アセット]** タブに **VsPackage** コンテンツ タイプが含まれていて、その **[プロジェクト]** がプロジェクトの名前に設定されていることを確認します。

5. CompletionTest プロジェクトを選択し、プロパティ ウィンドウで **[Pkgdef ファイルの生成]** を **true** に設定します。 プロジェクトを保存します。

6. 静的 `SnippetUtilities` クラスをプロジェクトに追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet22":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet22":::

7. SnippetUtilities クラスで、GUID を定義し、*SnippetsIndex.xml* ファイルで使用した値を指定します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet23":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet23":::

8. <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute> を `TestCompletionHandler` クラスに追加します。 この属性は、プロジェクト内の任意のパブリックまたは内部 (非静的) クラスに追加できます (場合によっては、Microsoft.VisualStudio.Shell 名前空間用の `using` ディレクティブを追加する必要があります)。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet24":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet24":::

9. プロジェクトをビルドして実行します。 プロジェクトの実行時に起動される Visual Studio の実験用インスタンスで、先ほど登録したスニペットが **TestSnippets** 言語の下の **コード スニペット マネージャー** に表示されます。

## <a name="add-the-insert-snippet-command-to-the-shortcut-menu"></a>[スニペットの挿入] コマンドをショートカット メニューに追加する
 **[スニペットの挿入]** コマンドは、テキスト ファイル用のショートカット メニューには含まれません。 そのため、コマンドを有効にする必要があります。

#### <a name="to-add-the-insert-snippet-command-to-the-shortcut-menu"></a>[スニペットの挿入] コマンドをショートカット メニューに追加するには

1. `TestCompletionCommandHandler` クラス ファイルを開きます。

     このクラスは <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> を実装しているため、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メソッドで **[スニペットの挿入]** コマンドをアクティブにすることができます。 コマンドを有効にする前に、このメソッドがオートメーション関数の内部で呼び出されないことを確認してください。これは、 **[スニペットの挿入]** コマンドをクリックしたときに、スニペット ピッカー ユーザー インターフェイス (UI) が表示されるためです。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet25":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet25":::

2. プロジェクトをビルドして実行します。 実験用インスタンスで、ファイル名拡張子が *.zzz* のファイルを開き、その中の任意の場所を右クリックします。 ショートカット メニューに **[スニペットの挿入]** コマンドが表示されます。

## <a name="implement-snippet-expansion-in-the-snippet-picker-ui"></a>スニペット ピッカー UI でスニペット拡張を実装する
 このセクションでは、コード スニペット拡張を実装して、ショートカット メニューの **[スニペットの挿入]** をクリックしたときに、スニペット ピッカー UI が表示されるようにする方法について説明します。 コード スニペットは、ユーザーがコード スニペットのショートカットを入力し、**Tab** キーを押したときにも展開されます。

 スニペット ピッカー UI を表示し、ナビゲーションと挿入後のスニペットの受け入れを有効にするには、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> メソッドを使用します。 挿入自体は、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> メソッドによって処理されます。

 コード スニペット拡張の実装では、レガシの <xref:Microsoft.VisualStudio.TextManager.Interop> インターフェイスが使用されます。 現在のエディター クラスからレガシ コードに変換する場合、レガシ インターフェイスでは、行番号と列番号の組み合わせを使用してテキスト バッファー内の場所が指定されますが、現在のクラスでは、1 つのインデックスが使用されることに注意してください。 したがって、バッファー内に、それぞれ 10 文字 (および 1 文字としてカウントされる改行) を含む 3 つの行がある場合、3 行目の 4 番目の文字は、現在の実装では 27 の位置になりますが、以前の実装では、2 行目の 3 の位置になります。

#### <a name="to-implement-snippet-expansion"></a>スニペット拡張を実装するには

1. `TestCompletionCommandHandler` クラスを含むファイルに、次の `using` ディレクティブを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet26":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet26":::

2. `TestCompletionCommandHandler` クラスに <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient> インターフェイスを実装させます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet27":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet27":::

3. `TestCompletionCommandHandlerProvider` クラスで、<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> をインポートします。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet28":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet28":::

4. コード拡張インターフェイスと <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 用のプライベート フィールドを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet29":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet29":::

5. `TestCompletionCommandHandler` クラスのコンストラクターで、次のフィールドを設定します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet30":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet30":::

6. ユーザーが **[スニペットの挿入]** コマンドをクリックしたときにスニペット ピッカーを表示するには、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> メソッドに次のコードを追加します (ここでは、説明を読みやすくするために、ステートメント入力候補に使用される `Exec()` コードは表示しません。代わりに、既存のメソッドにコードのブロックが追加されます)。文字をチェックするコードの後に、次のコード ブロックを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet31":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet31":::

7. 移動できるフィールドがスニペットにある場合、拡張が明示的に許可されるまで、拡張セッションは開いたままになります。スニペットにフィールドがない場合、セッションは閉じられ、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionManager.InvokeInsertionUI%2A> メソッドによって `null` として返されます。 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> メソッドで、前の手順で追加したスニペット ピッカー UI コードの後に、スニペット ナビゲーションを処理する次のコードを追加します (ユーザーがスニペットの挿入後に **Tab** または **Shift**+**Tab** キーを押した場合)。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet32":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet32":::

8. ユーザーが対応するショートカットを入力し、**Tab** キーを押したときにコード スニペットを挿入するには、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> メソッドにコードを追加します。 スニペットを挿入するプライベート メソッドは、後の手順で示します。 前の手順で追加したナビゲーション コードの後に、次のコードを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet33":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet33":::

9. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient> インターフェイスのメソッドを実装します。 この実装では、目的のメソッドは <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.EndExpansion%2A> と <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> だけです。 他のメソッドは <xref:Microsoft.VisualStudio.VSConstants.S_OK> を返すだけです。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet34":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet34":::

10. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> メソッドを実装します。 拡張を実際に挿入するヘルパー メソッドについては、後の手順で説明します。 <xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan> は行と列の情報を提供します。この情報は <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> から取得できます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet35":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet35":::

11. 次のプライベート メソッドでは、ショートカットまたはタイトルとパスに基づいて、コード スニペットが挿入されます。 その後、スニペットを使って <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansion.InsertNamedExpansion%2A> メソッドが呼び出されます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet36":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet36":::

## <a name="build-and-test-code-snippet-expansion"></a>コード スニペット拡張をビルドしてテストする
 プロジェクトでスニペット拡張が機能するかどうかをテストできます。

1. ソリューションをビルドします。 デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 つ目のインスタンスが起動されます。

2. テキスト ファイルを開き、いくつかのテキストを入力します。

3. テキスト内の任意の場所を右クリックし、 **[スニペットの挿入]** をクリックします。

4. スニペット ピッカー UI が表示され、「**Test replacement fields**」という文字列ポップアップが表示されます。 ポップアップをダブルクリックします。

     次のスニペットが挿入されます。

    ```
    MessageBox.Show("first");
    MessageBox.Show("second");
    ```

     **Enter** キーや **Esc** キーは押さないでください。

5. **Tab** キーまたは **Shift**+**Tab** キーを押して、"first" と "second" を切り替えます。

6. **Enter** キーまたは **Esc** キーを押して、挿入を受け入れます。

7. テキストの別の部分に「test」と入力し、**Tab** キーを押します。"test" はコード スニペットのショートカットなので、スニペットが再び挿入されます。

## <a name="next-steps"></a>次のステップ
