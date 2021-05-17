---
title: 従来の言語サービスでのメンバー補完 | Microsoft Docs
description: 従来の言語サービスにおける IntelliSense メンバー補完ツールヒントの動作、およびそれが Managed Package Framework (MPF) によってどのようにサポートされているかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense, Member Completion tool tip
- Member Completion, supporting in language services [managed package framework]
- language services [managed package framework], IntelliSense Member Completion
ms.assetid: 500f718d-9028-49a4-8615-ba95cf47fc52
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5279b3a96cb9658b968a5d51bbd8b1c2a41862b6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095135"
---
# <a name="member-completion-in-a-legacy-language-service"></a>従来の言語サービスでのメンバー補完

IntelliSense メンバー補完は、クラス、構造体、列挙型、名前空間など、特定のスコープの使用可能なメンバーのリストを表示するツールヒントです。 たとえば、C# では、ユーザーが "this" に続けてピリオドを入力すると、現在のスコープのクラスまたは構造体のすべてのメンバーのリストが、ユーザーが選択できるリストに表示されます。

Managed Package Framework (MPF) ではツールヒントがサポートされており、ツールヒントでリストを管理できます。ここでは、パーサーを使用して、リストに表示されるデータを提供するだけで済みます。

従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能の新しい実装方法では MEF 拡張機能が使用されます。 詳細については、「[エディターと言語サービスの拡張](../../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

> [!NOTE]
> 新しいエディターの API をできるだけ早く使い始めることをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="how-it-works"></a>動作のしくみ

MPF のクラスを使用してメンバー リストを表示するには、次の 2 つの方法があります。

- 識別子の上、またはメンバーの補完文字の後にキャレットを置いて、**IntelliSense** メニューの **[メンバーの一覧]** を選択します。

- <xref:Microsoft.VisualStudio.Package.IScanner> スキャナーではメンバー補完文字が検出され、その文字に対して [TokenTriggers.MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>) のトークン トリガーが設定されます。

メンバー補完文字は、クラス、構造体、または列挙型のメンバーが後に続くことを示しています。 たとえば、C# または Visual Basic ではメンバー補完文字は `.` です。また、C++ では、文字は `.` または `->` です。 トリガーの値は、メンバーの選択文字がスキャンされるときに設定されます。

### <a name="the-intellisense-member-list-command"></a>IntelliSense メンバー リスト コマンド

<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> コマンドを指定すると、<xref:Microsoft.VisualStudio.Package.Source> クラスの <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> メソッドの呼び出しが開始されます。その後、<xref:Microsoft.VisualStudio.Package.Source.Completion%2A> メソッドによって <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッド パーサーが [ParseReason.DisplayMemberList](<xref:Microsoft.VisualStudio.Package.ParseReason.DisplayMemberList>) という解析理由で呼び出されます。

パーサーにより、現在の位置のコンテキストと、現在の位置またはその直前のトークンが確認されます。 このトークンに基づいて、宣言のリストが表示されます。 たとえば、C# では、クラス メンバーの上にキャレットを配置し、 **[メンバーの一覧]** を選択すると、クラスのすべてのメンバーのリストが表示されます。 オブジェクト変数に続くピリオドの後にキャレットを配置すると、そのオブジェクトが表すクラスの全メンバーのリストが表示されます。 メンバー リストが表示されているときに、メンバーの上にキャレットを配置した場合、リストからメンバーを選択すると、キャレットが置かれているメンバーがリスト内のメンバーと置き換えられます。

### <a name="the-token-trigger"></a>トークン トリガー

[TokenTriggers.MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>) トリガーでは、<xref:Microsoft.VisualStudio.Package.Source> クラスの <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> メソッドの呼び出しが開始されます。その後、<xref:Microsoft.VisualStudio.Package.Source.Completion%2A> メソッドによってパーサーが [ParseReason.MemberSelect](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelect>) という解析理由で呼び出されます。 トークン トリガーにも [TokenTriggers.MatchBraces](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MatchBraces>) フラグが含まれている場合、解析理由は、メンバーの選択とかっこの強調表示を組み合わせた [ParseReason. MemberSelectAndHighlightBraces](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelectAndHighlightBraces>) になります。

パーサーにより、現在の位置のコンテキストと、メンバー選択文字の前に入力された文字が確認されます。 この情報から、要求されたスコープのすべてのメンバーのリストがパーサーによって作成されます。 この宣言の一覧は、<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドから返される <xref:Microsoft.VisualStudio.Package.AuthoringScope> オブジェクトに格納されます。 宣言が返された場合、メンバー補完ツールヒントが表示されます。 ツールヒントは、<xref:Microsoft.VisualStudio.Package.CompletionSet> クラスのインスタンスによって管理されます。

## <a name="enable-support-for-member-completion"></a>メンバー補完のサポートを有効にする

IntelliSense の操作をサポートするには、`CodeSense` レジストリ エントリを 1 に設定する必要があります。 このレジストリ エントリは、言語パッケージに関連付けられている <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> ユーザー属性に渡される名前付きパラメーターを使用して設定できます。 言語サービスのクラスでは、<xref:Microsoft.VisualStudio.Package.LanguagePreferences> クラスの <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> プロパティからこのレジストリ エントリの値が読み取られます。

スキャナーから [TokenTriggers.MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>) のトークン トリガーが返され、パーサーから宣言のリストが返された場合、メンバー入力候補一覧が表示されます。

## <a name="support-member-completion-in-the-scanner"></a>スキャナーでメンバー補完をサポートする

スキャナーでは、メンバー補完文字を検出し、その文字が解析されたときに [TokenTriggers.MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>) のトークン トリガーが設定されるようにする必要があります。

### <a name="scanner-example"></a>スキャナーの例

メンバー補完文字を検出し、適切な <xref:Microsoft.VisualStudio.Package.TokenTriggers> フラグを設定する簡単な例を次に示します。 この例は、説明のみを目的としています。 テキスト行でトークンを識別して返すメソッド `GetNextToken` がスキャナーに含まれていることを想定しています。 このコード例では、単純に、正しい種類の文字が確認されるたびにトリガーが設定されます。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestScanner : IScanner
    {
        private Lexer lex;
        private const char memberSelectChar = '.';

        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,
                                                   ref int state)
        {
            bool foundToken = false
            string token = lex.GetNextToken();
            if (token != null)
            {
                foundToken = true;
                char c = token[0];
                if (c == memberSelectChar)
                {
                        tokenInfo.Trigger |= TokenTriggers.MemberSelect;
                }
            }
            return foundToken;
        }
    }
}
```

## <a name="support-member-completion-in-the-parser"></a>パーサーでメンバー補完をサポートする

メンバー補完のためには、<xref:Microsoft.VisualStudio.Package.Source> クラスで <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A> メソッドを呼び出します。 <xref:Microsoft.VisualStudio.Package.Declarations> クラスから派生したクラスでこの一覧を実装する必要があります。 実装する必要があるメソッドの詳細については、<xref:Microsoft.VisualStudio.Package.Declarations> クラスを参照してください。

メンバー選択文字が入力されると、パーサーは [ParseReason.MemberSelect](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelect>) または [ParseReason.MemberSelectAndHighlightBraces](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelectAndHighlightBraces>) を使用して呼び出されます。 <xref:Microsoft.VisualStudio.Package.ParseRequest> オブジェクトで指定された場所は、メンバー選択文字の直後です。 パーサーでは、ソース コード内の特定の位置にある、メンバー リストに表示できるすべてのメンバーの名前を収集する必要があります。 次に、パーサーでは現在の行を解析して、ユーザーがメンバー選択文字に関連付けるスコープを確認する必要があります。

このスコープは、メンバー選択文字の前にある識別子の種類に基づいています。 たとえば、C# では、メンバー変数 `languageService` の型が `LanguageService` である場合、「**languageService.** 」と入力すると、 `LanguageService` クラスのすべてのメンバーのリストが生成されます。 また、C# では、「**this.** 」と入力すると、 現在のスコープ内のクラスの全メンバーを含むリストが生成されます。

### <a name="parser-example"></a>パーサーの例

次の例は、<xref:Microsoft.VisualStudio.Package.Declarations> リストに入力する方法の 1 つを示しています。 このコードでは、`TestAuthoringScope` クラスの `AddDeclaration` メソッドを呼び出すことによって、パーサーで宣言が作成され、それがリストに追加されることを前提としています。

```csharp
using System.Collections;
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    internal class TestDeclaration
    {
        public string Name;            // Name of declaration
        public int     TypeImageIndex; // Glyph index
        public string Description;     // Description of declaration

        public TestDeclaration(string name, int typeImageIndex, string description)
        {
            this.Name = name;
            this.TypeImageIndex = typeImageIndex;
            this.Description = description;
        }
    }

    //===================================================
    internal class TestDeclarations : Declarations
    {
        private ArrayList declarations;

        public TestDeclarations()
            : base()
        {
            declarations = new ArrayList();
        }

        public void AddDeclaration(TestDeclaration declaration)
        {
            declarations.Add(declaration);
        }

        //////////////////////////////////////////////////////////////////////
        // Declarations of class methods that must be implemented.
        public override int GetCount()
        {
            // Return the number of declarations to show.
            return declarations.Count;
        }

        public override string GetDescription(int index)
        {
            // Return the description of the specified item.
            string description = "";
            if (index >= 0 && index < declarations.Count)
            {
                description = ((TestDeclaration)declarations[index]).Description;
            }
            return description;
        }

        public override string GetDisplayText(int index)
        {
            // Determine what is displayed in the tool tip list.
            string text = null;
            if (index >= 0 && index < declarations.Count)
            {
                text = ((TestDeclaration)declarations[index]).Name;
            }
            return text;
        }

        public override int GetGlyph(int index)
        {
            // Return index of image to display next to the display text.
            int imageIndex = -1;
            if (index >= 0 && index < declarations.Count)
            {
                imageIndex = ((TestDeclaration)declarations[index]).TypeImageIndex;
            }
            return imageIndex;
        }

        public override string GetName(int index)
        {
            string name = null;
            if (index >= 0 && index < declarations.Count)
            {
                name = ((TestDeclaration)declarations[index]).Name;
            }
            return name;
        }
    }

    //===================================================
    public class TestAuthoringScope : AuthoringScope
    {
        private TestDeclarations declarationsList;

        public void AddDeclaration(TestDeclaration declaration)
        {
            if (declaration != null)
            {
                if (declarationsList == null)
                {
                    declarationsList = new TestDeclarations();
                }
                declarationsList.AddDeclaration(declaration);
            }
        }

        public override Declarations GetDeclarations(IVsTextView view,
                                                     int line,
                                                     int col,
                                                     TokenInfo info,
                                                     ParseReason reason)
        {
            return declarationsList;
        }

        /////////////////////////////////////////////////
        // Remainder of AuthoringScope methods not shown.
        /////////////////////////////////////////////////
    }

    //===================================================
    class TestLanguageService : LanguageService
    {
        public override AuthoringScope ParseSource(ParseRequest req)
        {
            TestAuthoringScope scope = new TestAuthoringScope();
            if (req.Reason == ParseReason.MemberSelect ||
                req.Reason == ParseReason.MemberSelectAndHighlightBraces)
            {
                // Gather list of declarations based on what the user
                // has typed so far. In this example, this list is an array of
                // MemberDeclaration objects (a helper class you might implement
                // to hold member declarations).
                // How this list is gathered is dependent on the parser
                // and is not shown here.
                MemberDeclarations memberDeclarations;
                memberDeclarations = GetDeclarationsForScope();

                // Now populate the Declarations list in the authoring scope.
                // GetImageIndexBasedOnType() is a helper method you
                // might implement to convert a member type to an index into
                // the image list returned from the language service.
                foreach (MemberDeclaration dec in memberDeclarations)
                {
                    scope.AddDeclaration(new TestDeclaration(
                                             dec.Name,
                                             GetImageIndexBasedOnType(dec.Type),
                                             dec.Description));
                }
            }
            return scope;
        }
    }
}
```
