---
title: 従来の言語サービスでのコード スニペットのサポート | Microsoft Docs
description: 従来の言語サービスでコード スニペットをサポートする方法について説明します。 コード スニペットは、ソース ファイルに挿入されるコードの一部です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- snippets, supporting in language services
- code snippets, supporting in language services [managed package framework]
- language services [managed package framework], supporting code snippets
ms.assetid: 7490325b-acee-4c2d-ac56-1cd5db1a1083
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9578159554f77a9ad7553a56c054a863b3b63fd5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080763"
---
# <a name="support-for-code-snippets-in-a-legacy-language-service"></a>従来の言語サービスでのコード スニペットのサポート
コード スニペットは、ソース ファイルに挿入されるコードの一部です。 スニペット自体は、一連のフィールドを持つ XML ベースのテンプレートです。 これらのフィールドは、スニペットが挿入された後に強調表示され、スニペットが挿入されたコンテキストによって異なる値を指定できます。 スニペットが挿入されるとすぐに、言語サービスではスニペットを書式設定できます。

 スニペットは、TAB キーを使用してスニペットのフィールドをナビゲートできる特殊な編集モードで挿入されます。 フィールドでは、IntelliSense スタイルのドロップダウン メニューをサポートできます。 ユーザーは、ENTER または ESC キーのいずれかを入力して、スニペットをソース ファイルにコミットします。 スニペットの詳細については、「[コード スニペット](../../ide/code-snippets.md)」を参照してください。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能の新しい実装方法では MEF 拡張機能が使用されます。 詳細については、「[チュートリアル: コード スニペットの実装](../../extensibility/walkthrough-implementing-code-snippets.md)」を参照してください。

> [!NOTE]
> 新しいエディターの API をできるだけ早く使い始めることをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="managed-package-framework-support-for-code-snippets"></a>Managed Package Framework によるコード スニペットのサポート
 Managed Package Framework (MPF) では、テンプレートを読み取ってスニペットを挿入し、特殊な編集モードを有効にするなど、ほとんどのスニペット機能がサポートされています。 サポートは <xref:Microsoft.VisualStudio.Package.ExpansionProvider> クラスによって管理されます。

 <xref:Microsoft.VisualStudio.Package.Source> クラスがインスタンス化されると、<xref:Microsoft.VisualStudio.Package.LanguageService> クラスの <xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionProvider%2A> メソッドが呼び出されて <xref:Microsoft.VisualStudio.Package.ExpansionProvider> オブジェクトが取得されます (基底 <xref:Microsoft.VisualStudio.Package.LanguageService> クラスでは常に各 <xref:Microsoft.VisualStudio.Package.Source> オブジェクトの新しい <xref:Microsoft.VisualStudio.Package.ExpansionProvider> オブジェクトが返されることに注意してください)。

 MPF では拡張関数をサポートしていません。 拡張関数は、スニペット テンプレートに埋め込まれている名前付き関数であり、フィールドに配置される 1 つ以上の値を返します。 値は、言語サービス自体によって <xref:Microsoft.VisualStudio.Package.ExpansionFunction> オブジェクトを介して返されます。 拡張関数をサポートするには、<xref:Microsoft.VisualStudio.Package.ExpansionFunction> オブジェクトが言語サービスによって実装されている必要があります。

## <a name="providing-support-for-code-snippets"></a>コード スニペットのサポートの提供
 コード スニペットのサポートを有効にするには、スニペットを指定またはインストールする必要があります。また、ユーザーがスニペットを挿入するための手段を提供する必要があります。 コード スニペットのサポートを有効にするには、次の 3 つの手順があります。

1. スニペット ファイルをインストールします。

2. 言語サービスのコード スニペットを有効にします。

3. <xref:Microsoft.VisualStudio.Package.ExpansionProvider> オブジェクトを呼び出します。

### <a name="installing-the-snippet-files"></a>スニペット ファイルのインストール
 言語のすべてのスニペットは、テンプレートとして XML ファイルに格納されます。通常、ファイルごとに 1 つのスニペット テンプレートが使用されます。 コード スニペット テンプレートに使用される XML スキーマの詳細については、「[コード スニペット スキーマ リファレンス](../../ide/code-snippets-schema-reference.md)」を参照してください。 各スニペット テンプレートは、言語 ID で識別されます。 この言語 ID はレジストリで指定され、テンプレート内の \<Code> タグの `Language` 属性に格納されます。

 通常、スニペット テンプレート ファイルが格納されている場所は 2 つあります。1) 言語がインストールされている場所と、2) ユーザーのフォルダーです。 Visual Studio の **コード スニペット マネージャー** でスニペットを見つけることができるように、これらの場所はレジストリに追加されます。 ユーザーのフォルダーは、ユーザーが作成したスニペットが格納される場所です。

 インストールされているスニペット テンプレート ファイルの一般的なフォルダー レイアウトは、 *[InstallRoot]* \\ *[TestLanguage]* \Snippets\\ *[LCID]* \Snippets のようになります。

 *[InstallRoot]* は、言語がインストールされているフォルダーです。

 *[TestLanguage]* は、フォルダー名としての言語の名前です。

 *[LCID]* はロケール ID です。 これは、スニペットのローカライズされたバージョンが格納される方法です。 たとえば、英語のロケール ID は 1033 であるため、 *[LCID]* は 1033 に置き換えられます。

 追加のファイルを 1 つ指定する必要があります。これは通常 SnippetsIndex.xml または ExpansionsIndex.xml というインデックス ファイルです (.xml で終わる有効なファイル名を使用できます)。 通常、このファイルは *[InstallRoot]* \\ *[TestLanguage]* フォルダーに格納され、スニペット フォルダーの正確な場所と、スニペットを使用する言語サービスの言語 ID と GUID を指定します。 インデックス ファイルの正確なパスは、後のレジストリ エントリのインストールに関するトピックで説明されているように、レジストリに格納されます。 SnippetsIndex.xml ファイルの例を次に示します。

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

 \<Language> タグでは、言語 ID (`Lang` 属性) と言語サービスの GUID を指定します。

 この例では、Visual Studio のインストール フォルダーに言語サービスがインストールされていることを前提としています。 %LCID% はユーザーの現在のロケール ID に置き換えられます。 ディレクトリとロケールごとに 1 つずつ、複数の \<SnippetDir> タグを追加することができます。 また、スニペット フォルダーにはサブフォルダーを含めることができ、各サブフォルダーは \<SnippetDir> タグに埋め込まれた \<SnippetSubDir> タグを使用してインデックス ファイルで識別されます。

 ユーザーは、使用している言語に合わせて独自のスニペットを作成することもできます。 これらは通常、ユーザーの設定フォルダーに格納されます。たとえば、 *[TestDocs]* \Code Snippets\\ *[TestLanguage]* \Test Code Snippets では、 *[TestDocs]* は Visual Studio のユーザーの設定フォルダーの場所です。

 次の置換要素は、インデックス ファイルの \<DirPath> タグに格納されているパスに配置できます。

|要素|説明|
|-------------|-----------------|
|%LCID%|ロケール ID。|
|%InstallRoot%|Visual Studio のルート インストール フォルダー (たとえば、C:\Program Files\Microsoft Visual Studio 8)。|
|%ProjDir%|現在のプロジェクトを格納しているフォルダー。|
|%ProjItem%|現在のプロジェクト項目を格納しているフォルダー。|
|%TestDocs%|ユーザーの設定フォルダー内のフォルダー (たとえば、C:\Documents and Settings\\ *[username]* \My Documents\Visual Studio\8)。|

### <a name="enabling-code-snippets-for-your-language-service"></a>言語サービスのコード スニペットの有効化
 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute> 属性を VSPackage に追加することによって、言語サービスのコード スニペットを有効にすることができます (詳細については、「[従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)」を参照してください)。 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute.ShowRoots%2A> および <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute.SearchPaths%2A> パラメーターは省略可能ですが、スニペットの場所を **コード スニペット マネージャー** に通知するために、`SearchPaths` 名前付きパラメーターを含める必要があります。

 この属性を使う方法の例を次に示します。

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
 言語サービスでは、挿入の呼び出し方法と同様に、任意のコード スニペットの挿入を制御します。

## <a name="calling-the-expansion-provider-for-code-snippets"></a>コード スニペットの拡張プロバイダーの呼び出し
 拡張プロバイダーを呼び出すには、メニュー コマンドを使用する方法と、入力候補一覧からショートカットキーを使用する方法の 2 つがあります。

### <a name="inserting-a-code-snippet-by-using-a-menu-command"></a>メニュー コマンドを使用したコード スニペットの挿入
 メニュー コマンドを使用してスニペット ブラウザーを表示するには、メニュー コマンドを追加してから、そのメニュー コマンドに応答して <xref:Microsoft.VisualStudio.Package.ExpansionProvider> インターフェイスの <xref:Microsoft.VisualStudio.Package.ExpansionProvider.DisplayExpansionBrowser%2A> メソッドを呼び出します。

1. .vsct ファイルにコマンドとボタンを追加します。 「[メニュー コマンドを使用した拡張機能の作成](../../extensibility/creating-an-extension-with-a-menu-command.md)」でこれを行う手順を参照してください。

2. <xref:Microsoft.VisualStudio.Package.ViewFilter> クラスからクラスを派生させ、<xref:Microsoft.VisualStudio.Package.ViewFilter.QueryCommandStatus%2A> メソッドをオーバーライドして、新しいメニュー コマンドのサポートを示すようにします。 この例では、常にメニュー コマンドを有効にします。

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

3. <xref:Microsoft.VisualStudio.Package.ViewFilter> クラスの <xref:Microsoft.VisualStudio.Package.ViewFilter.HandlePreExec%2A> メソッドをオーバーライドして、<xref:Microsoft.VisualStudio.Package.ExpansionProvider> オブジェクトを取得し、そのオブジェクトに対して <xref:Microsoft.VisualStudio.Package.ExpansionProvider.DisplayExpansionBrowser%2A> メソッドを呼び出します。

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

     <xref:Microsoft.VisualStudio.Package.ExpansionProvider> クラスの次のメソッドは、スニペットの挿入中に、指定された順序で Visual Studio によって呼び出されます。

4. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnItemChosen%2A>

5. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.IsValidKind%2A>

6. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnBeforeInsertion%2A>

7. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FormatSpan%2A>

8. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A>

     <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A> メソッドが呼び出されると、スニペットが挿入され、<xref:Microsoft.VisualStudio.Package.ExpansionProvider> オブジェクトは、挿入されたばかりのスニペットを変更するために使用される特殊な編集モードになります。

### <a name="inserting-a-code-snippet-by-using-a-shortcut"></a>ショートカットを使用したコード スニペットの挿入
 入力候補一覧からのショートカットの実装は、メニュー コマンドの実装よりもはるかに複雑です。 最初にスニペットのショートカットを IntelliSense の単語入力候補一覧に追加する必要があります。 次に、完了の結果としてスニペットのショートカット名が挿入されたときに検出する必要があります。 最後に、ショートカット名を使用してスニペットのタイトルとパスを取得し、その情報を <xref:Microsoft.VisualStudio.Package.ExpansionProvider> メソッドの <xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A> メソッドに渡す必要があります。

 単語入力候補一覧にスニペットのショートカットを追加するには、それらを <xref:Microsoft.VisualStudio.Package.AuthoringScope> クラスの <xref:Microsoft.VisualStudio.Package.Declarations> オブジェクトに追加します。 ショートカットをスニペット名として識別できるようにする必要があります。 例については、「[チュートリアル: インストールされているコード スニペットの一覧の取得 (従来の実装)](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)」を参照してください。

 <xref:Microsoft.VisualStudio.Package.Declarations> クラスの <xref:Microsoft.VisualStudio.Package.Declarations.OnAutoComplete%2A> メソッドで、コード スニペットのショートカットの挿入を検出できます。 スニペット名は既にソース ファイルに挿入されているため、拡張を挿入するときに削除する必要があります。 <xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A> メソッドでは、スニペットの挿入ポイントを説明するスパンを受け取ります。スパンにソース ファイル内のスニペット名全体が含まれている場合、その名前はスニペットに置き換えられます。

 ここでは、ショートカット名を指定してスニペットの挿入を処理する <xref:Microsoft.VisualStudio.Package.Declarations> クラスのバージョンを示します。 <xref:Microsoft.VisualStudio.Package.Declarations> クラスの他のメソッドは、わかりやすくするために省略されています。 このクラスのコンストラクターでは <xref:Microsoft.VisualStudio.Package.LanguageService> オブジェクトを受け取ることに注意してください。 これは、使用しているバージョンの <xref:Microsoft.VisualStudio.Package.AuthoringScope> オブジェクトから渡すことができます (たとえば、<xref:Microsoft.VisualStudio.Package.AuthoringScope> クラスの実装では、コンストラクター内の <xref:Microsoft.VisualStudio.Package.LanguageService> オブジェクトを受け取り、そのオブジェクトを `TestDeclarations` クラス コンストラクターに渡すことがあります)。

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

 言語サービスではショートカット名を取得すると、<xref:Microsoft.VisualStudio.Package.ExpansionProvider.FindExpansionByShortcut%2A> メソッドを呼び出して、ファイル名とコード スニペットのタイトルを取得します。 次に、言語サービスでは <xref:Microsoft.VisualStudio.Package.ExpansionProvider> クラスの <xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A> メソッドを呼び出して、コード スニペットを挿入します。 次のメソッドは、スニペットの挿入中に、<xref:Microsoft.VisualStudio.Package.ExpansionProvider> クラスで指定された順序で Visual Studio によって呼び出されます。

1. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.IsValidKind%2A>

2. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnBeforeInsertion%2A>

3. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FormatSpan%2A>

4. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A>

   言語サービスに対してインストールされているコード スニペットの一覧を取得する方法の詳細については、「[チュートリアル: インストールされているコード スニペットの一覧の取得 (従来の実装)](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)」を参照してください。

## <a name="implementing-the-expansionfunction-class"></a>ExpansionFunction クラスの実装
 拡張関数は、スニペット テンプレートに埋め込まれている名前付き関数であり、フィールドに配置される 1 つ以上の値を返します。 言語サービスで拡張関数をサポートするには、<xref:Microsoft.VisualStudio.Package.ExpansionFunction> クラスからクラスを派生させ、<xref:Microsoft.VisualStudio.Package.ExpansionFunction.GetCurrentValue%2A> メソッドを実装する必要があります。 次に、<xref:Microsoft.VisualStudio.Package.LanguageService> クラスの <xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionFunction%2A> メソッドをオーバーライドして、サポートする拡張関数ごとに使用しているバージョンの <xref:Microsoft.VisualStudio.Package.ExpansionFunction> クラスの新しいインスタンス化を返す必要があります。 拡張関数から有効な値の一覧をサポートする場合は、<xref:Microsoft.VisualStudio.Package.ExpansionFunction> クラスの <xref:Microsoft.VisualStudio.Package.ExpansionFunction.GetIntellisenseList%2A> メソッドをオーバーライドして、それらの値の一覧を返す必要もあります。

 拡張関数が呼び出されるときまでに拡張プロバイダーは完全に初期化されていない可能性があるため、引数を指定するか、他のフィールドにアクセスする必要がある拡張関数は、編集可能なフィールドに関連付けないでください。 その結果、拡張関数では引数またはその他のフィールドの値を取得できません。

### <a name="example"></a>例
 `GetName` という単純な拡張関数を実装する方法の例を次に示します。 この拡張関数では、拡張関数がインスタンス化されるたびに、基底クラス名に数値を追加します (関連付けられているコード スニペットが挿入されるたびに対応します)。

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
- [従来の言語サービスの機能](../../extensibility/internals/legacy-language-service-features1.md)
- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)
- [コード スニペット](../../ide/code-snippets.md)
- [チュートリアル: インストールされているコード スニペットの一覧の取得 (従来の実装)](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)
