---
title: 従来の言語サービスでのコードスニペットのサポート |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- snippets, supporting in language services
- code snippets, supporting in language services [managed package framework]
- language services [managed package framework], supporting code snippets
ms.assetid: 7490325b-acee-4c2d-ac56-1cd5db1a1083
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2d771db166baa66426c7a6d03b344c4bc7b74b27
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72723105"
---
# <a name="support-for-code-snippets-in-a-legacy-language-service"></a>従来の言語サービスでのコード スニペットのサポート
コードスニペットは、ソースファイルに挿入されるコードの一部です。 スニペット自体は、一連のフィールドを持つ XML ベースのテンプレートです。 これらのフィールドは、スニペットが挿入された後に強調表示され、スニペットが挿入されたコンテキストによって異なる値を持つことができます。 スニペットが挿入されるとすぐに、言語サービスはスニペットの書式を設定できます。

 スニペットは、TAB キーを使用してスニペットのフィールドに移動できる特殊な編集モードで挿入されます。 フィールドでは、IntelliSense スタイルのドロップダウンメニューをサポートできます。 ユーザーは、ENTER キーまたは ESC キーを入力して、スニペットをソースファイルにコミットします。 スニペットの詳細については、「[コードスニペット](../../ide/code-snippets.md)」を参照してください。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能を実装するための新しい方法として、MEF 拡張機能を使用することをお勧めします。 詳細については、「[チュートリアル: コードスニペットの実装](../../extensibility/walkthrough-implementing-code-snippets.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、エディターの新機能を利用できるようになります。

## <a name="managed-package-framework-support-for-code-snippets"></a>マネージパッケージフレームワークによるコードスニペットのサポート
 Managed package framework (MPF) では、テンプレートを読み取ってスニペットを挿入し、特殊な編集モードを有効にするなど、ほとんどのスニペット機能がサポートされています。 サポートは <xref:Microsoft.VisualStudio.Package.ExpansionProvider> クラスによって管理されます。

 @No__t_0 クラスがインスタンス化されると、<xref:Microsoft.VisualStudio.Package.ExpansionProvider> オブジェクトを取得するために <xref:Microsoft.VisualStudio.Package.LanguageService> クラスの <xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionProvider%2A> メソッドが呼び出されます (基本 <xref:Microsoft.VisualStudio.Package.LanguageService> クラスは、常に各 <xref:Microsoft.VisualStudio.Package.ExpansionProvider> オブジェクトの新しい <xref:Microsoft.VisualStudio.Package.Source> オブジェクトを返します)。

 MPF は拡張機能をサポートしていません。 拡張関数は、スニペットテンプレートに埋め込まれている名前付き関数であり、フィールドに配置される1つ以上の値を返します。 値は、<xref:Microsoft.VisualStudio.Package.ExpansionFunction> オブジェクトを介して言語サービス自体によって返されます。 拡張機能をサポートするには、<xref:Microsoft.VisualStudio.Package.ExpansionFunction> オブジェクトが言語サービスによって実装されている必要があります。

## <a name="providing-support-for-code-snippets"></a>コードスニペットのサポートの提供
 コードスニペットのサポートを有効にするには、スニペットを指定またはインストールする必要があります。また、スニペットを挿入するための手段をユーザーに提供する必要があります。 コードスニペットのサポートを有効にするには、次の3つの手順を実行します。

1. スニペットファイルをインストールしています。

2. 言語サービスのコードスニペットを有効にします。

3. @No__t_0 オブジェクトを呼び出しています。

### <a name="installing-the-snippet-files"></a>スニペットファイルのインストール
 言語のすべてのスニペットは、テンプレートとして XML ファイルに格納されます。通常、ファイルごとに1つのスニペットテンプレートが使用されます。 コードスニペットテンプレートに使用される XML スキーマの詳細については、「[コードスニペットスキーマリファレンス](../../ide/code-snippets-schema-reference.md)」を参照してください。 各スニペットテンプレートには、言語 ID が指定されています。 この言語 ID はレジストリで指定され、テンプレート内の \<Code > タグの `Language` 属性に格納されます。

 通常、スニペットテンプレートファイルが格納されている場所は2つあります。 1) 言語がインストールされていて、2) ユーザーのフォルダーにあります。 これらの場所はレジストリに追加されるので、Visual Studio **Code スニペットマネージャー**はスニペットを見つけることができます。 ユーザーのフォルダーは、ユーザーが作成したスニペットが格納される場所です。

 インストールされているスニペットテンプレートファイルの一般的なフォルダーレイアウトは次のようになります。 *[Installroot]* \\ *[testlanguage]* \ スニペット \\ *[LCID]* \snippets

 *[Installroot]* は、言語がインストールされているフォルダーです。

 *[Testlanguage]* は、言語の名前をフォルダー名として指定します。

 *[LCID]* はロケール ID です。 これは、スニペットのローカライズバージョンが格納される方法です。 たとえば、英語のロケール ID は1033であるため、 *[LCID]* は1033に置き換えられます。

 追加のファイルを1つ指定する必要があります。これは通常、SnippetsIndex またはと呼ばれるインデックスファイルです (.xml で終わる任意の有効なファイル名を使用できます)。 通常、このファイルは *[Installroot]* \\ *[testlanguage]* フォルダーに格納され、スニペットフォルダーの正確な場所、およびスニペットを使用する言語サービスの言語 ID と GUID を指定します。 インデックスファイルの正確なパスは、後の「レジストリエントリのインストール」で説明されているように、レジストリに格納されます。 SnippetsIndex ファイルの例を次に示します。

```
<?xml version="1.0" encoding="utf-8" ?>
<SnippetCollection>
    <Language Lang="Testlanguage" Guid="{b614a40a-80d9-4fac-a6ad-fc2868fff7cd}">
        <SnippetDir>
            <OnOff>On</OnOff>
            <Installed>true</Installed>
            <Locale>1033</Locale>
            <DirPath>%InstallRoot%\TestLanguage\Snippets\%LCID%\Snippets\</DirPath>
            <LocalizedName>Snippets</LocalizedName>
        </SnippetDir>
    </Language>
</SnippetCollection>
```

 @No__t_0Language > タグは、言語 ID (`Lang` 属性) と言語サービス GUID を指定します。

 この例では、Visual Studio のインストールフォルダーに言語サービスがインストールされていることを前提としています。 % LCID% はユーザーの現在のロケール ID に置き換えられます。 複数の \<SnippetDir > タグを、それぞれ異なるディレクトリとロケールに1つずつ追加できます。 また、スニペットフォルダーにはサブフォルダーを含めることができます。各サブフォルダーには、\<SnippetDir > タグに埋め込まれている \<SnippetSubDir > タグがインデックスファイルで識別されます。

 ユーザーは、自分の言語に合わせて独自のスニペットを作成することもできます。 これらは通常、ユーザーの設定フォルダーに格納されます。たとえば、[ *Testdocs]* \ コードスニペット \\ *[testdocs]* \ テストコードスニペットです。ここで、 *[Testdocs]* は Visual Studio のユーザーの設定フォルダーの場所です。

 次の置換要素は、インデックスファイルの \<DirPath > タグに格納されているパスに配置できます。

|要素|説明|
|-------------|-----------------|
|LCID|ロケール ID。|
|InstallRoot|Visual Studio のルートインストールフォルダー (C:\Program て Visual Studio 8 など)。|
|% ProjDir%|現在のプロジェクトを格納しているフォルダー。|
|% ProjItem%|現在のプロジェクト項目を格納しているフォルダー。|
|% TestDocs%|ユーザーの settings フォルダー内のフォルダー (C:\documents and、Settings \\ *[username]* \My Documents\Visual Studio\8. など)。|

### <a name="enabling-code-snippets-for-your-language-service"></a>言語サービスのコードスニペットの有効化
 @No__t_0 属性を VSPackage に追加することによって、言語サービスのコードスニペットを有効にすることができます (詳細について[は、「従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)」を参照してください)。 @No__t_0 パラメーターと <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute.SearchPaths%2A> パラメーターは省略可能ですが、スニペットの場所を**コードスニペットマネージャー**に通知するために、`SearchPaths` 名前付きパラメーターを含める必要があります。

 この属性を使用する方法の例を次に示します。

```
[ProvideLanguageCodeExpansion(
         typeof(TestSnippetLanguageService),
         "Test Snippet Language",          // Name of language used as registry key
         0,                               // Resource ID of localized name of language service
         "Test Snippet Language",        // Name of Language attribute in snippet template
         @"%InstallRoot%\Test Snippet Language\Snippets\%LCID%\SnippetsIndex.xml",  // Path to snippets index
         SearchPaths = @"%InstallRoot%\Test Snippet Language\Snippets\%LCID%\")]    // Path to snippets
```

### <a name="calling-the-expansion-provider"></a>拡張プロバイダーの呼び出し
 言語サービスは、挿入の呼び出しと同様に、任意のコードスニペットの挿入を制御します。

## <a name="calling-the-expansion-provider-for-code-snippets"></a>コードスニペットの展開プロバイダーの呼び出し
 拡張プロバイダーを呼び出すには、メニューコマンドを使用する方法と、入力候補一覧からショートカットキーを使用する方法の2つがあります。

### <a name="inserting-a-code-snippet-by-using-a-menu-command"></a>メニューコマンドを使用したコードスニペットの挿入
 メニューコマンドを使用してスニペットブラウザーを表示するには、メニューコマンドを追加し、そのメニューコマンドに応答して、<xref:Microsoft.VisualStudio.Package.ExpansionProvider> インターフェイスで <xref:Microsoft.VisualStudio.Package.ExpansionProvider.DisplayExpansionBrowser%2A> メソッドを呼び出します。

1. Vsct ファイルにコマンドとボタンを追加します。 [メニューコマンドを使用して拡張機能を作成](../../extensibility/creating-an-extension-with-a-menu-command.md)する方法については、「」を参照してください。

2. @No__t_0 クラスからクラスを派生させ、<xref:Microsoft.VisualStudio.Package.ViewFilter.QueryCommandStatus%2A> メソッドをオーバーライドして、新しいメニューコマンドのサポートを示すようにします。 この例では、常にメニューコマンドを有効にします。

    ```csharp
    using Microsoft.VisualStudio.Package;

    namespace TestLanguagePackage
    {
        class TestViewFilter : ViewFilter
        {
            public TestViewFilter(CodeWindowManager mgr, IVsTextView view)
                : base(mgr, view)
            {
            }

            protected override int QueryCommandStatus(ref Guid guidCmdGroup,
                                                      uint nCmdId)
            {
                int hr = base.QueryCommandStatus(ref guidCmdGroup, nCmdId);
                // If the base class did not recognize the command then
                // see if we can handle the command.
                if (hr == (int)Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_UNKNOWNGROUP)
                {
                    if (guidCmdGroup == GuidList.guidTestLanguagePackageCmdSet)
                    {
                        if (nCmdId == PkgCmdIDList.InvokeCodeSnippetsBrowser)
                        {
                            hr = (int)(OLECMDF.OLECMDF_SUPPORTED | OLECMDF.OLECMDF_ENABLED);
                        }
                    }
                }
                return hr;
            }
        }
    }
    ```

3. @No__t_1 クラスの <xref:Microsoft.VisualStudio.Package.ViewFilter.HandlePreExec%2A> メソッドをオーバーライドして <xref:Microsoft.VisualStudio.Package.ExpansionProvider> オブジェクトを取得し、そのオブジェクトに対して <xref:Microsoft.VisualStudio.Package.ExpansionProvider.DisplayExpansionBrowser%2A> メソッドを呼び出します。

    ```csharp
    using Microsoft.VisualStudio.Package;

    namespace TestLanguagePackage
    {
        class TestViewFilter : ViewFilter
        {
            public override bool HandlePreExec(ref Guid guidCmdGroup,
                                               uint nCmdId,
                                               uint nCmdexecopt,
                                               IntPtr pvaIn,
                                               IntPtr pvaOut)
            {
                if (base.HandlePreExec(ref guidCmdGroup,
                                       nCmdId,
                                       nCmdexecopt,
                                       pvaIn,
                                       pvaOut))
                {
                    // Base class handled the command.  Do nothing more here.
                    return true;
                }

                if (guidCmdGroup == GuidList.guidTestLanguagePackageCmdSet)
                {
                    if (nCmdId == PkgCmdIDList.InvokeCodeSnippetsBrowser)
                    {
                        ExpansionProvider ep = this.GetExpansionProvider();
                        if (this.TextView != null && ep != null)
                        {
                            bool bDisplayed = ep.DisplayExpansionBrowser(
                                this.TextView,
                                "TestLanguagePackage Snippet:",
                                null,
                                false,
                                null,
                                false);
                        }
                        return true;   // Handled the command.
                    }
                }
                return false;   // Did not handle the command.
            }
        }
    }

    ```

     @No__t_0 クラスの次のメソッドは、スニペットを挿入する処理中に Visual Studio によって指定された順序で呼び出されます。

4. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnItemChosen%2A>

5. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.IsValidKind%2A>

6. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnBeforeInsertion%2A>

7. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FormatSpan%2A>

8. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A>

     @No__t_0 メソッドが呼び出されると、スニペットが挿入され、<xref:Microsoft.VisualStudio.Package.ExpansionProvider> オブジェクトは、挿入されたばかりのスニペットを変更するために使用される特殊な編集モードになります。

### <a name="inserting-a-code-snippet-by-using-a-shortcut"></a>ショートカットを使用したコードスニペットの挿入
 入力候補一覧からのショートカットの実装は、メニューコマンドの実装よりもはるかに複雑です。 最初にスニペットのショートカットを IntelliSense の単語入力候補一覧に追加する必要があります。 次に、完了の結果としてスニペットのショートカット名が挿入されたことを検出する必要があります。 最後に、ショートカット名を使用してスニペットのタイトルとパスを取得し、その情報を <xref:Microsoft.VisualStudio.Package.ExpansionProvider> メソッドの <xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A> メソッドに渡す必要があります。

 単語の入力候補一覧にスニペットのショートカットを追加するには、<xref:Microsoft.VisualStudio.Package.AuthoringScope> クラスの <xref:Microsoft.VisualStudio.Package.Declarations> オブジェクトに追加します。 ショートカットをスニペット名として識別できることを確認する必要があります。 例については、「[チュートリアル: インストールされているコードスニペットの一覧を取得する (レガシ実装)](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)」を参照してください。

 @No__t_1 クラスの <xref:Microsoft.VisualStudio.Package.Declarations.OnAutoComplete%2A> メソッドにコードスニペットのショートカットを挿入することを検出できます。 スニペット名は既にソースファイルに挿入されているため、展開を挿入するときに削除する必要があります。 @No__t_0 メソッドは、スニペットの挿入ポイントを説明するスパンを受け取ります。スパンにソースファイル内のスニペット名全体が含まれている場合、その名前はスニペットに置き換えられます。

 ここでは、ショートカット名を指定してスニペットの挿入を処理する <xref:Microsoft.VisualStudio.Package.Declarations> クラスのバージョンを示します。 @No__t_0 クラスのその他のメソッドは、わかりやすくするために省略されています。 このクラスのコンストラクターは、<xref:Microsoft.VisualStudio.Package.LanguageService> オブジェクトを受け取ることに注意してください。 これは、<xref:Microsoft.VisualStudio.Package.AuthoringScope> オブジェクトのバージョンから渡すことができます (たとえば、<xref:Microsoft.VisualStudio.Package.AuthoringScope> クラスの実装では、コンストラクターの <xref:Microsoft.VisualStudio.Package.LanguageService> オブジェクトを受け取り、そのオブジェクトを `TestDeclarations` クラスコンストラクターに渡すことがあります)。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    internal class TestDeclarations : Declarations
    {
        private ArrayList       declarations;
        private LanguageService languageService;
        private TextSpan        commitSpan;

        public TestDeclarations(LanguageService langService)
            : base()
        {
            languageService = langService;
            declarations = new ArrayList();
        }

        // This method is used to add declarations to the internal list.
        public void AddDeclaration(TestDeclaration declaration)
        {
            declarations.Add(declaration);
        }

        // This method is called to get the string to commit to the source buffer.
        // Note that the initial extent is only what the user has typed so far.
        public override string OnCommit(IVsTextView textView,
                                        string textSoFar,
                                        char commitCharacter,
                                        int index,
                                        ref TextSpan initialExtent)
        {
            // We intercept this call only to get the initial extent
            // of what was committed to the source buffer.
            commitSpan = initialExtent;

            return base.OnCommit(textView,
                                 textSoFar,
                                 commitCharacter,
                                 index,
                                 ref initialExtent);
        }

        // This method is called after the string has been committed to the source buffer.
        public override char OnAutoComplete(IVsTextView textView,
                                            string committedText,
                                            char commitCharacter,
                                            int index)
        {
            TestDeclaration item = declarations[index] as TestDeclaration;
            if (item != null)
            {
                // In this example, TestDeclaration identifies types with a string.
                // You can choose a different approach.
                if (item.Type == "snippet")
                {
                    Source src = languageService.GetSource(textView);
                    if (src != null)
                    {
                        ExpansionProvider ep = src.GetExpansionProvider();
                        if (ep != null)
                        {
                            string title;
                            string path;
                            int commitLength = commitSpan.iEndIndex - commitSpan.iStartIndex;
                            if (commitLength < committedText.Length)
                            {
                                // Replace everything that was inserted
                                // so calculate the span of the full
                                // insertion, taking into account what
                                // was inserted when the commitSpan
                                // was obtained in the first place.
                                commitSpan.iEndIndex += (committedText.Length - commitLength);
                            }

                            if (ep.FindExpansionByShortcut(textView,
                                                           committedText,
                                                           commitSpan,
                                                           true,
                                                           out title,
                                                           out path))
                            {
                                ep.InsertNamedExpansion(textView,
                                                        title,
                                                        path,
                                                        commitSpan,
                                                        false);
                            }
                        }
                    }
                }
            }
            return '\0';
        }
    }
}
```

 言語サービスがショートカット名を取得すると、<xref:Microsoft.VisualStudio.Package.ExpansionProvider.FindExpansionByShortcut%2A> メソッドを呼び出して、ファイル名とコードスニペットのタイトルを取得します。 次に、言語サービスは、<xref:Microsoft.VisualStudio.Package.ExpansionProvider> クラスの <xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A> メソッドを呼び出して、コードスニペットを挿入します。 次のメソッドは、スニペットの挿入処理中に、<xref:Microsoft.VisualStudio.Package.ExpansionProvider> クラスの指定された順序で Visual Studio によって呼び出されます。

1. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.IsValidKind%2A>

2. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnBeforeInsertion%2A>

3. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FormatSpan%2A>

4. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A>

   言語サービスに対してインストールされているコードスニペットの一覧を取得する方法の詳細については、「[チュートリアル: インストールされているコードスニペットの一覧を取得する (レガシ実装)](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)」を参照してください。

## <a name="implementing-the-expansionfunction-class"></a>すべての関数クラスの実装
 拡張関数は、スニペットテンプレートに埋め込まれている名前付き関数であり、フィールドに配置される1つ以上の値を返します。 言語サービスで拡張関数をサポートするには、<xref:Microsoft.VisualStudio.Package.ExpansionFunction> クラスからクラスを派生させ、<xref:Microsoft.VisualStudio.Package.ExpansionFunction.GetCurrentValue%2A> メソッドを実装する必要があります。 次に、<xref:Microsoft.VisualStudio.Package.LanguageService> クラスの <xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionFunction%2A> メソッドをオーバーライドして、サポートする各拡張関数について、使用しているバージョンの <xref:Microsoft.VisualStudio.Package.ExpansionFunction> クラスの新しいインスタンス化を返す必要があります。 拡張関数から有効な値の一覧をサポートする場合は、その値の一覧を返すために、<xref:Microsoft.VisualStudio.Package.ExpansionFunction> クラスの <xref:Microsoft.VisualStudio.Package.ExpansionFunction.GetIntellisenseList%2A> メソッドもオーバーライドする必要があります。

 拡張機能が呼び出されたときに拡張プロバイダーが完全に初期化されない可能性があるため、引数を受け取るか、他のフィールドにアクセスする必要がある拡張関数は、編集可能なフィールドに関連付けないでください。 その結果、展開関数は引数またはその他のフィールドの値を取得できません。

### <a name="example"></a>例
 @No__t_0 と呼ばれる単純な展開関数の実装例を次に示します。 この展開関数は、拡張関数がインスタンス化されるたびに、基底クラス名に数値を追加します (関連付けられているコードスニペットが挿入されるたびに対応します)。

```csharp
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        private int classNameCounter = 0;

        public override ExpansionFunction CreateExpansionFunction(
            ExpansionProvider provider,
            string functionName)
        {
            ExpansionFunction function = null;
            if (functionName == "GetName")
            {
                ++classNameCounter;
                function = new TestGetNameExpansionFunction(provider, classNameCounter);
            }
            return function;
        }
    }

    internal class TestGetNameExpansionFunction : ExpansionFunction
    {
        private int nameCount;

        TestGetNameExpansionFunction(ExpansionProvider provider, int counter)
            : base(provider)
        {
            nameCount = counter;
        }

        public override string GetCurrentValue()
        {
            string name = "TestClass";
            name += nameCount.ToString();
            return name;
        }
    }
}
```

## <a name="see-also"></a>関連項目
- [従来の言語サービスの特徴](../../extensibility/internals/legacy-language-service-features1.md)
- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)
- [コード スニペット](../../ide/code-snippets.md)
- [チュートリアル: インストールされているコード スニペットの一覧の取得 (従来の実装)](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)