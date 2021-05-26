---
title: オプション ページの作成 |Microsoft Docs
description: マネージド パッケージ フレームワークの DialogPage クラスを実装することで、Visual Studio の [ツール] メニューの下に [オプション] ページを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed package framework, creating Tools Options pages
- Tools Options pages [Visual Studio SDK], creating using managed package framework
ms.assetid: 1bf11fec-dece-4943-8053-6de1483c43eb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f7b1b8b92f978739bfa4e540013347e216781cd4
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217243"
---
# <a name="create-options-pages"></a>オプションページを作成する
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] マネージド パッケージ フレームワークでは、<xref:Microsoft.VisualStudio.Shell.DialogPage> から派生したクラスを使用して、 **[ツール]** メニューの下に **[オプション]** ページを追加することで、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE を拡張します。

 特定の **[ツール オプション]** ページを実装するオブジェクトは、<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> オブジェクトによって、特定の VSPackage に関連付けられます。

 IDE によって特定の **[ツール オプション]** ページが表示されるときに、環境によって、その特定のページを実装しているオブジェクトがインスタンス化されます。

- **[ツール オプション]** ページは、VSPackage を実装しているオブジェクトではなく、独自のオブジェクトに実装する必要があります。

- 1 つのオブジェクトで複数の **[ツール オプション]** ページを実装することはできません。

## <a name="register-as-a-tools-options-page-provider"></a>[ツール オプション] ページ プロバイダーとして登録する
 **[ツール オプション]** ページを通してユーザー構成をサポートする VSPackage では、<xref:Microsoft.VisualStudio.Shell.Package> 実装に適用される <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> のインスタンスを適用することによって、これらの **[ツール オプション]** ページを提供するオブジェクトを示します。

 **[ツール オプション]** ページを実装するすべての <xref:Microsoft.VisualStudio.Shell.DialogPage> 派生型に対して、<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> のインスタンスが 1 つ存在する必要があります。

 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> の各インスタンスでは、 **[ツール オプション]** ページを実装する型、 **[ツール オプション]** ページを識別するために使用されるカテゴリとサブカテゴリを含む文字列、 **[ツール オプション]** ページを提供するものとしてその型を登録するためのリソース情報が使用されます。

## <a name="persist-tools-options-page-state"></a>[ツール オプション] ページの状態を永続化する
 **[ツール オプション]** ページの実装が、有効になっているオートメーション サポートに登録されると、IDE では、その他すべての **[ツール オプション]** ページと共に、そのページの状態が永続化されます。

 VSPackage では、<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> を使用して、独自の永続化を管理できます。 永続化の方法は、1 種類のみを使用する必要があります。

## <a name="implement-dialogpage-class"></a>DialogPage クラスを実装する
 <xref:Microsoft.VisualStudio.Shell.DialogPage> 派生型の VSPackage の実装を提供するオブジェクトでは、継承された以下の機能を利用できます。

- 既定のユーザー インターフェイス ウィンドウ。

- <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> がこのクラスに適用されている場合や、クラスに適用されている <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> の <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute.SupportsProfiles%2A> プロパティが `true` に設定されている場合は、既定の永続化メカニズムを使用できます。

- オートメーションのサポート。

  <xref:Microsoft.VisualStudio.Shell.DialogPage> を使用して **[ツール オプション]** ページを実装するオブジェクトの最小要件は、パブリック プロパティの追加です。

  クラスが **[ツール オプション]** ページ プロバイダーとして正しく登録されている場合は、プロパティ グリッドの形式で、 **[ツール]** メニューの **[オプション]** セクションからそのパブリック プロパティを使用できます。

  これらの既定の機能はすべて、オーバーライドできます。 たとえば、より洗練されたユーザー インターフェイスを作成するには、<xref:Microsoft.VisualStudio.Shell.DialogPage.Window%2A> の既定の実装をオーバーライドするだけで済みます。

## <a name="example"></a>例
 次に示すのは、オプション ページの単純な "Hello world" 実装です。 **[メニュー コマンド]** オプションを選択した Visual Studio パッケージ テンプレートによって作成された既定のプロジェクトに、次のコードを追加すると、オプション ページの機能の適切な実例となります。

### <a name="description"></a>説明
 次のクラスでは、最小限の "Hello world" オプション ページを定義しています。 開かれたときには、ユーザーがプロパティ グリッドで、パブリック `HelloWorld` プロパティを設定できます。

### <a name="code"></a>コード
:::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/cs/class1.cs" id="Snippet11":::
:::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/vb/class1.vb" id="Snippet11":::

### <a name="description"></a>説明
 パッケージ クラスに次の属性を適用すると、パッケージの読み込み時にオプション ページが使用できるようになります。 数値は、カテゴリとページを表す任意のリソース ID であり、最後にあるブール値では、そのページがオートメーションをサポートするかどうかを指定しています。

### <a name="code"></a>コード
:::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/cs/uiusersettingstoolsoptionspagespackage.cs" id="Snippet07":::
:::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/vb/uiusersettingstoolsoptionspagespackage.vb" id="Snippet07":::

### <a name="description"></a>説明
 次のイベント ハンドラーは、オプション ページで設定されたプロパティの値に応じて結果を表示します。 これは、結果がカスタム オプション ページの型に明示的にキャストされる <xref:Microsoft.VisualStudio.Shell.Package.GetDialogPage%2A> メソッドを使用して、そのページによって公開されるプロパティにアクセスします。

 パッケージ テンプレートによって生成されたプロジェクトの場合は、`MenuItemCallback` 関数からこの関数を呼び出して、それを **[ツール]** メニューに追加された既定のコマンドにアタッチします。

### <a name="code"></a>コード
:::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/cs/uiusersettingstoolsoptionspagespackage.cs" id="Snippet08":::
:::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/vb/uiusersettingstoolsoptionspagespackage.vb" id="Snippet08":::

## <a name="see-also"></a>関連項目
- [ユーザー設定とオプションを拡張する](../../extensibility/extending-user-settings-and-options.md)
- [オプション ページのオートメーションのサポート](../../extensibility/internals/automation-support-for-options-pages.md)
