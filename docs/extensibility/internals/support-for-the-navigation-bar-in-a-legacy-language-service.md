---
title: 従来の言語サービスでのナビゲーション バーのサポート
description: 従来の言語サービスでナビゲーション バーをサポートする方法について説明します。 エディター ビューのナビゲーション バーには、ファイル内の型とメンバーが表示されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Navigation bar, supporting in language services [managed package framework]
- language services [managed package framework], Navigation bar
ms.assetid: 2d301ee6-4523-4b82-aedb-be43f352978e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e75103d008e65c6d2060d598e442499f38a0e322
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080659"
---
# <a name="support-for-the-navigation-bar-in-a-legacy-language-service"></a>従来の言語サービスでのナビゲーション バーのサポート
エディター ビューの上部にあるナビゲーション バーには、ファイル内の型とメンバーが表示されます。 型は左のドロップダウンに表示され、メンバーは右のドロップダウンに表示されます。 ユーザーが型を選択すると、キャレットが型の最初の行に配置されます。 ユーザーがメンバーを選択すると、キャレットがそのメンバーの定義に配置されます。 ドロップダウン ボックスは、キャレットの現在位置を反映するように更新されます。

## <a name="displaying-and-updating-the-navigation-bar"></a>ナビゲーション バーの表示と更新
 ナビゲーション バーをサポートするには、<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> クラスからクラスを派生し、<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> メソッドを実装する必要があります。 言語サービスにコード ウィンドウが指定されている場合、基本 <xref:Microsoft.VisualStudio.Package.LanguageService> クラスでは <xref:Microsoft.VisualStudio.Package.CodeWindowManager> をインスタンス化します。これには、コード ウィンドウを表す <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> オブジェクトが含まれています。 次に、<xref:Microsoft.VisualStudio.Package.CodeWindowManager> オブジェクトに新しい <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> オブジェクトを指定します。 <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A> メソッドによって <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> オブジェクトを取得します。 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> クラスのインスタンスを返す場合、<xref:Microsoft.VisualStudio.Package.CodeWindowManager> では <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> メソッドを呼び出して内部リストに値を設定し、<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> オブジェクトを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ドロップダウン バー マネージャーに渡します。 次に、ドロップダウン バー マネージャーでは <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> オブジェクトに対して <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.SetDropdownBar%2A> メソッドを呼び出し、2 つのドロップダウン バーを保持する <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBar> オブジェクトを確立します。

 キャレットが移動すると、<xref:Microsoft.VisualStudio.Package.LanguageService.OnIdle%2A> メソッドでは <xref:Microsoft.VisualStudio.Package.LanguageService.OnCaretMoved%2A> メソッドを呼び出します。 基本 <xref:Microsoft.VisualStudio.Package.LanguageService.OnCaretMoved%2A> メソッドでは、<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> クラスの <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> メソッドを呼び出して、ナビゲーション バーの状態を更新します。 <xref:Microsoft.VisualStudio.Package.DropDownMember> オブジェクトのセットをこのメソッドに渡します。 各オブジェクトは、ドロップダウンのエントリを表します。

## <a name="the-contents-of-the-navigation-bar"></a>ナビゲーション バーの内容
 通常、ナビゲーション バーには、型の一覧とメンバーの一覧が含まれています。 型の一覧には、現在のソース ファイルで使用できるすべての型が含まれています。 型名には、完全な名前空間情報が含まれています。 2 つの型を持つ C# コードの例を次に示します。

```csharp
namespace TestLanguagePackage
{
    public class TestLanguageService
    {
        internal struct Token
        {
            int tokenID;
        }
        private Tokens[] tokens;
        private string serviceName;
    }
}
```

 型一覧に `TestLanguagePackage.TestLanguageService` と `TestLanguagePackage.TestLanguageService.Tokens` が表示されます。

 メンバー一覧には、型一覧で選択された型の使用可能なメンバーが表示されます。 上のコード例を使用して、選択されている型が `TestLanguagePackage.TestLanguageService` である場合は、メンバー一覧にプライベート メンバー `tokens` と `serviceName` が含まれます。 内部構造体 `Token` は表示されません。

 キャレットを内側に置いたときにメンバーの名前を太字にすることができるように、メンバー一覧を実装できます。 また、メンバーをグレーのテキストで表示することもできます。これは、キャレットが現在配置されているスコープ内にないことを示します。

## <a name="enabling-support-for-the-navigation-bar"></a>ナビゲーション バーのサポートを有効にする
 ナビゲーション バーのサポートを有効にするには、<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 属性の `ShowDropdownBarOption` パラメーターを `true` に設定する必要があります。 このパラメーターは、<xref:Microsoft.VisualStudio.Package.LanguagePreferences.ShowNavigationBar%2A> プロパティを設定します。 ナビゲーション バーをサポートするには、<xref:Microsoft.VisualStudio.Package.LanguageService> クラスの <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A> メソッドに <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> オブジェクトを実装する必要があります。

 <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A> メソッドの実装で、<xref:Microsoft.VisualStudio.Package.LanguagePreferences.ShowNavigationBar%2A> プロパティが `true` に設定されている場合は、<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> オブジェクトを返すことができます。 オブジェクトを返さない場合、ナビゲーション バーは表示されません。

 ナビゲーション バーを表示するオプションは、ユーザーが設定できます。このため、エディター ビューが開いている間に、このコントロールがリセットされる可能性があります。 ユーザーは、変更が行われる前にエディター ウィンドウを閉じ、再度開く必要があります。

## <a name="implementing-support-for-the-navigation-bar"></a>ナビゲーション バーのサポートの実装
 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> メソッドでは、2 つの一覧 (ドロップダウンごとに 1 つ) と、各一覧内の現在の選択を表す 2 つの値を受け取ります。 一覧と選択値は更新できます。この場合、<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> メソッドでは一覧が変更されたことを示すために `true` を返す必要があります。

 型ドロップダウンで選択が変更されると、メンバー一覧を更新して新しい型を反映する必要があります。 メンバー一覧に表示される内容は、次のいずれかになります。

- 現在の型のメンバーの一覧。

- ソース ファイルで使用できるすべてのメンバー。ただし、現在の型に含まれていないすべてのメンバーはグレーのテキストで表示されます。 グレー表示されたメンバーは引き続き選択できるため、クイック ナビゲーションに使用できますが、この色によって、現在選択されている型に含まれていないことを示しています。

  <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> メソッドの実装では、通常、次の手順を実行します。

1. ソース ファイルに対する現在の宣言の一覧を取得します。

     一覧を設定する方法はいくつかあります。 1 つの方法は、ご使用のバージョンの <xref:Microsoft.VisualStudio.Package.LanguageService> クラスで、すべての宣言の一覧を返すカスタムの解析理由を指定して <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドを呼び出すカスタム メソッドを作成することです。 別の方法は、カスタムの解析理由を指定して、<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> メソッドから <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドを直接呼び出すことです。 3 番目の方法は、<xref:Microsoft.VisualStudio.Package.LanguageService> クラスの最後の完全な解析操作によって返された <xref:Microsoft.VisualStudio.Package.AuthoringScope> クラスで宣言をキャッシュし、<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> メソッドからそれを取得することです。

2. 型の一覧を設定または更新します。

     型一覧の内容は、ソースが変更されたとき、または現在のキャレット位置に基づいて型のテキスト スタイルを変更するように選択した場合に、更新される可能性があります。 この位置は <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> メソッドに渡されることに注意してください。

3. 現在のキャレット位置に基づいて、型一覧で選択する型を決定します。

     手順 1 で取得した宣言を検索して、現在のキャレット位置を囲む型を探し、型一覧でその型を検索して、型一覧におけるインデックスを決定できます。

4. 選択した型に基づいてメンバーの一覧を作成または更新します。

     メンバー一覧には、 **[メンバー]** ドロップダウンに現在表示されている内容が反映されます。 ソースが変更された場合、または選択した型のメンバーだけを表示していて、選択した型が変更された場合は、メンバー一覧の内容の更新が必要になることがあります。 ソース ファイル内のすべてのメンバーを表示することを選択した場合は、現在選択されている型が変更されると、一覧内の各メンバーのテキスト スタイルを更新する必要があります。

5. 現在のキャレット位置に基づいて、メンバー一覧で選択するメンバーを決定します。

     手順 1 で取得した宣言で現在のキャレット位置を含むメンバーを検索し、メンバー一覧でそのメンバーを検索して、メンバー一覧におけるインデックスを決定します。

6. 一覧またはいずれかの一覧の選択に何らかの変更が加えられた場合は、`true` を返します。
