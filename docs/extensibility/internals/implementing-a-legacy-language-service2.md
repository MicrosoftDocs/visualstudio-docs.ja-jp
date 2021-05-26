---
title: 従来の言語サービスの実装 2 | Microsoft Docs
description: マネージド パッケージ フレームワーク (MPF) を使用して、拡張言語サービス機能をサポートする従来の言語サービスを実装する方法について説明します。 パート 2/2。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], implementing
ms.assetid: 5bcafdc5-f922-48f6-a12e-6c8507a79a05
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9bdb0d05faaa139b808d8d117125c5208da470e9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085820"
---
# <a name="implementing-a-legacy-language-service-2"></a>従来の言語サービスの実装 2
Managed Package Framework (MPF) を使用して言語サービスを実装するには、<xref:Microsoft.VisualStudio.Package.LanguageService> クラスからクラスを派生させ、次の抽象メソッドとプロパティを実装する必要があります。

- <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A> メソッド

- <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> メソッド

- <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッド

- <xref:Microsoft.VisualStudio.Package.LanguageService.Name%2A> プロパティ

  これらのメソッドとプロパティの実装の詳細については、後述の該当するセクションを参照してください。

  その他の機能をサポートするために、言語サービスでは、MPF 言語サービスのいずれかのクラスからクラスを派生させる必要がある場合があります。たとえば、追加のメニュー コマンドをサポートするには、<xref:Microsoft.VisualStudio.Package.ViewFilter> クラスからクラスを派生させ、いくつかのコマンド処理メソッドをオーバーライドする必要があります (詳細については、<xref:Microsoft.VisualStudio.Package.ViewFilter> を参照してください)。 <xref:Microsoft.VisualStudio.Package.LanguageService> クラスには、さまざまなクラスの新しいインスタンスを作成するために呼び出されるいくつかのメソッドが用意されています。また、独自のクラスのインスタンスを提供するには、該当する作成メソッドをオーバーライドします。 たとえば、独自の <xref:Microsoft.VisualStudio.Package.ViewFilter> クラスのインスタンスを取得するには、<xref:Microsoft.VisualStudio.Package.LanguageService> クラスの <xref:Microsoft.VisualStudio.Package.LanguageService.CreateViewFilter%2A> メソッドをオーバーライドする必要があります。 詳細については、「カスタム クラスのインスタンス化」セクションを参照してください。

  言語サービスでは、さまざまな場所で使用される独自のアイコンを提供することもできます。 たとえば、IntelliSense の入力候補一覧が表示される場合に、リスト内の各項目にアイコンを関連付けることができ、メソッド、クラス、名前空間、プロパティなど、言語に必要な任意のものとして項目をマークできます。 これらのアイコンは、すべての IntelliSense リスト、**ナビゲーション バー**、および **[エラー一覧]** タスク ウィンドウで使用されます。 詳細については、後述の「言語サービスのイメージ」セクションを参照してください。

## <a name="getlanguagepreferences-method"></a>GetLanguagePreferences メソッド
 <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A> メソッドは、常に同じ <xref:Microsoft.VisualStudio.Package.LanguagePreferences> クラスのインスタンスを返します。 言語サービスに対して追加の設定が不要な場合は、<xref:Microsoft.VisualStudio.Package.LanguagePreferences> 基本クラスを使用できます。 MPF 言語サービスのクラスでは、少なくとも <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 基本クラスが存在することを前提としています。

### <a name="example"></a>例
 <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A> メソッドの一般的な実装の例を次に示します。 この例では、<xref:Microsoft.VisualStudio.Package.LanguagePreferences> 基本クラスを使用します。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        private LanguagePreferences m_preferences;

        public override LanguagePreferences GetLanguagePreferences()
        {
            if (m_preferences == null)
            {
                m_preferences = new LanguagePreferences(this.Site,
                                                        typeof(TestLanguageService).GUID,
                                                        this.Name );
                m_preferences.Init();
            }
            return m_preferences;
        }
    }
}
```

## <a name="getscanner-method"></a>GetScanner メソッド
 このメソッドは、トークンとその型およびトリガーの取得に使用される行指向型のパーサーまたはスキャナーを実装する、<xref:Microsoft.VisualStudio.Package.IScanner> オブジェクトのインスタンスを返します。 このスキャナーは、<xref:Microsoft.VisualStudio.Package.Colorizer> クラスでは色分けのために使用されますが、より複雑な解析操作の準備としてトークンの型とトリガーを取得するためにも使用できます。 <xref:Microsoft.VisualStudio.Package.IScanner> インターフェイスを実装したこのクラスを提供する必要があります。また、<xref:Microsoft.VisualStudio.Package.IScanner> インターフェイスのすべてのメソッドを実装する必要があります。

### <a name="example"></a>例
 <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> メソッドの一般的な実装の例を次に示します。 `TestScanner` クラスは、<xref:Microsoft.VisualStudio.Package.IScanner> インターフェイスを実装しています (表示されていません)。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        private TestScanner m_scanner;

        public override IScanner GetScanner(IVsTextLines buffer)
        {
            if (m_scanner == null)
            {
                m_scanner = new TestScanner(buffer);
            }
            return m_scanner;
        }
    }
}
    internal class TestScanner : IScanner
    {
        private IVsTextBuffer m_buffer;
        string m_source;

        public TestScanner(IVsTextBuffer buffer)
        {
            m_buffer = buffer;
        }

        bool IScanner.ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo, ref int state)
        {
            tokenInfo.Type = TokenType.Unknown;
            tokenInfo.Color = TokenColor.Text;
            return true;
        }

        void IScanner.SetSource(string source, int offset)
        {
            m_source = source.Substring(offset);
        }
    }

```

## <a name="parsesource-method"></a>ParseSource メソッド
 さまざまな理由に基づいてソース ファイルを解析します。 このメソッドには、特定の解析操作から期待されるものを記述する <xref:Microsoft.VisualStudio.Package.ParseRequest> オブジェクトが渡されます。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドは、トークンの機能とスコープを特定するより複雑なパーサーを呼び出します。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドは、IntelliSense 操作のサポートと、中かっこの照合に使用されます。 このような高度な操作をサポートしていない場合でも、有効な <xref:Microsoft.VisualStudio.Package.AuthoringScope> オブジェクトを返す必要があります。そのため、<xref:Microsoft.VisualStudio.Package.AuthoringScope> インターフェイスを実装するクラスを作成し、そのインターフェイスのすべてのメソッドを実装する必要があります。 すべてのメソッドから null 値を返すことができますが、<xref:Microsoft.VisualStudio.Package.AuthoringScope> オブジェクト自体を null 値にすることはできません。

### <a name="example"></a>例
 この例は、<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドと <xref:Microsoft.VisualStudio.Package.AuthoringScope> クラスの最小限の実装を示しています。これにより、言語サービスをコンパイルして機能させることができますが、より高度な機能は実際にサポートされません。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        public override AuthoringScope ParseSource(ParseRequest req)
        {
            return new TestAuthoringScope();
        }
    }

    internal class TestAuthoringScope : AuthoringScope
    {
        public override string GetDataTipText(int line, int col, out TextSpan span)
        {
            span = new TextSpan();
            return null;
        }

        public override Declarations GetDeclarations(IVsTextView view,
                                                     int line,
                                                     int col,
                                                     TokenInfo info,
                                                     ParseReason reason)
        {
            return null;
        }

        public override string Goto(VSConstants.VSStd97CmdID cmd, IVsTextView textView, int line, int col, out TextSpan span)
        {
            span = new TextSpan();
            return null;
        }

        public override Methods GetMethods(int line, int col, string name)
        {
            return null;
        }
}
```

## <a name="name-property"></a>Name プロパティ
 このプロパティは、言語サービスの名前を返します。 これは、言語サービスの登録時に指定された名前と同じである必要があります。 この名前は、さまざまな場所で使用されます。そのうちで最も目立つ <xref:Microsoft.VisualStudio.Package.LanguagePreferences> クラスでは、レジストリへのアクセスに使用されます。 このプロパティによって返される名前は、レジストリでレジストリ エントリおよびキーの名前として使用されるため、ローカライズすることはできません。

### <a name="example"></a>例
 この例は、<xref:Microsoft.VisualStudio.Package.LanguageService.Name%2A> プロパティの考えられる実装の 1 つを示しています。 ここでは名前がハード コーディングされていることに注意してください。実際の名前は、言語サービスの登録に使用できるように、リソース ファイルから取得する必要があります (「[従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)」を参照してください)。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        public override string Name
        {
            get { return "Test Language"; }
        }
    }
}
```

## <a name="instantiating-custom-classes"></a>カスタム クラスのインスタンス化
 次に示すクラスのメソッドをオーバーライドして、各クラスの独自バージョンのインスタンスを提供することができます。

### <a name="in-the-languageservice-class"></a>LanguageService クラス内

|メソッド|返されるクラス|説明|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateCodeWindowManager%2A>|<xref:Microsoft.VisualStudio.Package.CodeWindowManager>|テキスト ビューへのカスタムの追加をサポートします。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDocumentProperties%2A>|<xref:Microsoft.VisualStudio.Package.DocumentProperties>|カスタム ドキュメントのプロパティをサポートします。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A>|<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>|**ナビゲーション バー** をサポートします。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionFunction%2A>|<xref:Microsoft.VisualStudio.Package.ExpansionFunction>|コード スニペット テンプレート内の関数をサポートします。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionProvider%2A>|<xref:Microsoft.VisualStudio.Package.ExpansionProvider>|コード スニペットをサポートします (通常、このメソッドはオーバーライドされません)。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateParseRequest%2A>|<xref:Microsoft.VisualStudio.Package.ParseRequest>|<xref:Microsoft.VisualStudio.Package.ParseRequest> 構造体のカスタマイズをサポートします (通常、このメソッドはオーバーライドされません)。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateSource%2A>|<xref:Microsoft.VisualStudio.Package.Source>|ソース コードの書式設定、コメント文字の指定、およびメソッド シグネチャのカスタマイズをサポートします。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateViewFilter%2A>|<xref:Microsoft.VisualStudio.Package.ViewFilter>|追加のメニュー コマンドをサポートします。|
|<xref:Microsoft.VisualStudio.Package.Source.GetColorizer%2A>|<xref:Microsoft.VisualStudio.Package.Colorizer>|構文の強調表示をサポートします (通常、このメソッドはオーバーライドされません)。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A>|<xref:Microsoft.VisualStudio.Package.LanguagePreferences>|言語設定へのアクセスをサポートします。 このメソッドは実装する必要がありますが、基本クラスのインスタンスを返すことができます。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>|<xref:Microsoft.VisualStudio.Package.IScanner>|行のトークンの型を特定するために使用されるパーサーを提供します。 このメソッドは実装する必要があり、<xref:Microsoft.VisualStudio.Package.IScanner> が派生される必要があります。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>|<xref:Microsoft.VisualStudio.Package.AuthoringScope>|ソース ファイル全体を通じて機能とスコープを特定するために使用されるパーサーを提供します。 このメソッドは実装する必要があり、<xref:Microsoft.VisualStudio.Package.AuthoringScope> クラスの独自バージョンのインスタンスを返す必要があります。 構文の強調表示をサポートするだけでよい場合は (<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> メソッドから返された <xref:Microsoft.VisualStudio.Package.IScanner> パーサーが必要です)、このメソッドでは何も行わず、<xref:Microsoft.VisualStudio.Package.AuthoringScope> クラス (すべてのメソッドで null 値を返すバージョン) を返すだけで済みます。|

### <a name="in-the-source-class"></a>Source クラス内

|メソッド|返されるクラス|説明|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.Source.CreateCompletionSet%2A>|<xref:Microsoft.VisualStudio.Package.CompletionSet>|IntelliSense の入力候補一覧の表示をカスタマイズします (通常、このメソッドはオーバーライドされません)。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateErrorTaskItem%2A>|<xref:Microsoft.VisualStudio.Package.DocumentTask>|[エラー一覧] タスク一覧のマーカーをサポートします。具体的には、ファイルを開いてエラーの原因となった行にジャンプする以外にも機能をサポートします。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateMethodData%2A>|<xref:Microsoft.VisualStudio.Package.MethodData>|IntelliSense の [パラメーター ヒント] ツールヒントの表示をカスタマイズします。|
|<xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A>|<xref:Microsoft.VisualStudio.Package.CommentInfo>|コードのコメント付けをサポートします。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateAuthoringSink%2A>|<xref:Microsoft.VisualStudio.Package.AuthoringSink>|解析操作中に情報を収集します。|

### <a name="in-the-authoringscope-class"></a>AuthoringScope クラス内

|メソッド|返されるクラス|説明|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A>|<xref:Microsoft.VisualStudio.Package.Declarations>|メンバーや型などの宣言の一覧を提供します。 このメソッドは実装する必要がありますが、null 値を返すことができます。 このメソッドが有効なオブジェクトを返す場合、そのオブジェクトは <xref:Microsoft.VisualStudio.Package.Declarations> クラスの独自バージョンのインスタンスでなければなりません。|
|<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetMethods%2A>|<xref:Microsoft.VisualStudio.Package.Methods>|指定されたコンテキストのメソッド シグネチャの一覧を提供します。 このメソッドは実装する必要がありますが、null 値を返すことができます。 このメソッドが有効なオブジェクトを返す場合、そのオブジェクトは <xref:Microsoft.VisualStudio.Package.Methods> クラスの独自バージョンのインスタンスでなければなりません。|

## <a name="language-service-images"></a>言語サービスのイメージ
 言語サービス全体で使用されるアイコンの一覧を提供するには、<xref:Microsoft.VisualStudio.Package.LanguageService> クラスの <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> メソッドをオーバーライドして、アイコンを含む <xref:System.Windows.Forms.ImageList> を返します。 <xref:Microsoft.VisualStudio.Package.LanguageService> 基本クラスでは、アイコンの既定のセットが読み込まれます。 アイコンが必要な場所に正確なイメージ インデックスを指定するので、独自のイメージ リストをどのように並べ替えるかは、ユーザー次第です。

### <a name="images-used-in-intellisense-completion-lists"></a>IntelliSense の入力候補一覧で使用されるイメージ
 IntelliSense の入力候補一覧の場合、イメージ インデックスは <xref:Microsoft.VisualStudio.Package.Declarations> クラスの <xref:Microsoft.VisualStudio.Package.Declarations.GetGlyph%2A> メソッドの各項目に対して指定されます。イメージ インデックスを指定する場合は、これをオーバーライドする必要があります。 <xref:Microsoft.VisualStudio.Package.Declarations.GetGlyph%2A> メソッドから返される値は、<xref:Microsoft.VisualStudio.Package.CompletionSet> クラスのコンストラクターに渡されるイメージ リストのインデックスであり、<xref:Microsoft.VisualStudio.Package.LanguageService> クラスの <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> メソッドから返されるイメージ リストと同じです (<xref:Microsoft.VisualStudio.Package.Source> クラスの <xref:Microsoft.VisualStudio.Package.Source.CreateCompletionSet%2A> メソッドをオーバーライドして別のイメージ リストを指定する場合は、<xref:Microsoft.VisualStudio.Package.CompletionSet> に使用するイメージ リストを変更できます)。

### <a name="images-used-in-the-navigation-bar"></a>ナビゲーション バーで使用されるイメージ
 **ナビゲーション バー** には、型とメンバーの一覧が表示されます。クイック ナビゲーションでのアイコンの表示を可能にするために使用されます。 これらのアイコンは <xref:Microsoft.VisualStudio.Package.LanguageService> クラスの <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> メソッドから取得されます。**ナビゲーション バー** 専用にオーバーライドすることはできません。 コンボ ボックス内の各項目に使用されるインデックスは、コンボ ボックスを表すリストが <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> クラスの <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> メソッドで入力されるときに指定されます (「[従来の言語サービスでのナビゲーション バーのサポート](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)」を参照してください)。 これらのイメージ インデックスは、通常は <xref:Microsoft.VisualStudio.Package.Declarations> クラスの独自バージョンを使用して、パーサーから取得されます。 インデックスがどのように取得されるかは、ユーザー次第です。

### <a name="images-used-in-the-error-list-task-window"></a>[エラー一覧] タスク ウィンドウで使用されるイメージ
 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッド パーサー (「[従来の言語サービスのパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)」を参照) がエラーを検出し、そのエラーを <xref:Microsoft.VisualStudio.Package.AuthoringSink> クラスの <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddError%2A> メソッドに渡すたびに、 **[エラー一覧]** タスク ウィンドウにエラーが報告されます。 タスク ウィンドウに表示される各項目にアイコンを関連付けることができ、そのアイコンは、<xref:Microsoft.VisualStudio.Package.LanguageService> クラスの <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> メソッドから返されるものと同じイメージ リストから取得されます。 MPF クラスの既定の動作では、エラー メッセージにイメージは表示されません。 ただし、<xref:Microsoft.VisualStudio.Package.Source> クラスからクラスを派生させ、<xref:Microsoft.VisualStudio.Package.Source.CreateErrorTaskItem%2A> メソッドをオーバーライドすることによって、この動作をオーバーライドできます。 このメソッドで、新しい <xref:Microsoft.VisualStudio.Package.DocumentTask> オブジェクトを作成します。 オブジェクトを返す前に、<xref:Microsoft.VisualStudio.Package.DocumentTask> オブジェクトの <xref:Microsoft.VisualStudio.Shell.Task.ImageIndex%2A> プロパティを使用してイメージ インデックスを設定できます。 これは、次の例のようになります。 `TestIconImageIndex` は、すべてのアイコンを一覧する列挙体であり、この例に固有のものです。 お使いの言語サービスでは、アイコンを識別する方法が異なる場合があります。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    class TestSource : Source
    {
        public override DocumentTask CreateErrorTaskItem(
            TextSpan          span,
            string            filename,
            string            message,
            TaskPriority      priority,
            TaskCategory      category,
            MARKERTYPE        markerType,
            TaskErrorCategory errorCategory)
        {
            DocumentTask taskItem = base.CreateErrorTaskItem(
                                           span,
                                           filename,
                                           message,
                                           priority,
                                           category,
                                           markerType,
                                           errorCategory);
            if (errorCategory == TaskErrorCategory.Error)
            {
                taskItem.ImageIndex = TestIconImageIndex.Error;
            }
            return taskItem;
        }
    }
}
```

## <a name="the-default-image-list-for-a-language-service"></a>言語サービスの既定のイメージ リスト
 MPF 言語サービスの基本クラスに用意されている既定のイメージ リストには、より一般的な言語要素に関連付けられている多数のアイコンが含まれています。 これらのアイコンの大部分は、public、internal、friend、protected、private、shortcut というアクセス概念に対応する 6 つのバリエーションのセットにまとめられています。 たとえば、メソッドが public、protected、private のいずれであるかに応じて、異なるアイコンを使用できます。

 次の列挙体では、各アイコン セットの一般的な名前を指定し、関連付けられているインデックスを指定します。 たとえば、この列挙体に基づいて、protected メソッドのイメージ インデックスを `(int)IconImageIndex.Method + (int)IconImageIndex.AccessProtected` として指定できます。 この列挙体内の名前は、必要に応じて変更できます。

```csharp
public enum IconImageIndex
        {
            // access types
            AccessPublic = 0,
            AccessInternal = 1,
            AccessFriend = 2,
            AccessProtected = 3,
            AccessPrivate = 4,
            AccessShortcut = 5,

            Base = 6,
            // Each of the following icon type has 6 versions,
            //corresponding to the access types
            Class = Base + 0,
            Constant = Base + 1,
            Delegate = Base + 2,
            Enumeration = Base + 3,
            EnumMember = Base + 4,
            Event = Base + 5,
            Exception = Base + 6,
            Field = Base + 7,
            Interface = Base + 8,
            Macro = Base + 9,
            Map = Base + 10,
            MapItem = Base + 11,
            Method = Base + 12,
            OverloadedMethod = Base + 13,
            Module = Base + 14,
            Namespace = Base + 15,
            Operator = Base + 16,
            Property = Base + 17,
            Struct = Base + 18,
            Template = Base + 19,
            Typedef = Base + 20,
            Type = Base + 21,
            Union = Base + 22,
            Variable = Base + 23,
            ValueType = Base + 24,
            Intrinsic = Base + 25,
            JavaMethod = Base + 26,
            JavaField = Base + 27,
            JavaClass = Base + 28,
            JavaNamespace = Base + 29,
            JavaInterface = Base + 30,
            // Miscellaneous icons with one icon for each type.
            Error = 187,
            GreyedClass = 188,
            GreyedPrivateMethod = 189,
            GreyedProtectedMethod = 190,
            GreyedPublicMethod = 191,
            BrowseResourceFile = 192,
            Reference = 193,
            Library = 194,
            VBProject = 195,
            VBWebProject = 196,
            CSProject = 197,
            CSWebProject = 198,
            VB6Project = 199,
            CPlusProject = 200,
            Form = 201,
            OpenFolder = 202,
            ClosedFolder = 203,
            Arrow = 204,
            CSClass = 205,
            Snippet = 206,
            Keyword = 207,
            Info = 208,
            CallBrowserCall = 209,
            CallBrowserCallRecursive = 210,
            XMLEditor = 211,
            VJProject = 212,
            VJClass = 213,
            ForwardedType = 214,
            CallsTo = 215,
            CallsFrom = 216,
            Warning = 217,
        }
```

## <a name="see-also"></a>関連項目
- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service1.md)
- [従来の言語サービスの概要](../../extensibility/internals/legacy-language-service-overview.md)
- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)
- [従来の言語サービスのパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
