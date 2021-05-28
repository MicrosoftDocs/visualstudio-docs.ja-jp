---
title: オプションとオプション ページ |Microsoft Docs
description: VSPackage の状態を決定するオプションの値を変更できる、オプション ページのサポートについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], managed package framework support
- managed package framework, Tools Options pages support
- support, Tools Options pages
- Tools Options pages [Visual Studio SDK], layouts
- Tools Options pages [Visual Studio SDK], attributes
ms.assetid: e6c0e636-5ec3-450e-b395-fc4bb9d75918
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 32bcb32c4fc80a5806c9007c3119a2ba3de62427
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106214513"
---
# <a name="options-and-options-pages"></a>オプションとオプション ページ
**[ツール]** メニューの **[オプション]** をクリックすると、 **[オプション]** ダイアログ ボックスが開きます。 このダイアログ ボックス内のオプションは、総称してオプション ページと呼ばれます。 ナビゲーション ウィンドウのツリー コントロールにはオプション カテゴリが含まれていて、すべてのカテゴリにオプション ページがあります。 ページを選択すると、そのオプションが右側のウィンドウに表示されます。 これらのページでは、VSPackage の状態を決定するオプションの値を変更できます。

## <a name="support-for-options-pages"></a>オプション ページのサポート
 オプション ページとオプション カテゴリの作成は、<xref:Microsoft.VisualStudio.Shell.Package> クラスによってサポートされます。 オプション ページは、<xref:Microsoft.VisualStudio.Shell.DialogPage> クラスによって実装されます。

 <xref:Microsoft.VisualStudio.Shell.DialogPage> の既定の実装では、プロパティの汎用グリッド内のユーザーに対して、パブリック プロパティが提供されます。 この動作をカスタマイズするには、ページのさまざまなメソッドをオーバーライドして、独自のユーザー インターフェイス (UI) を使ったカスタム オプション ページを作成します。 詳しくは、「[オプション ページの作成](../../extensibility/creating-an-options-page.md)」をご覧ください。

 <xref:Microsoft.VisualStudio.Shell.DialogPage> クラスでは、<xref:Microsoft.VisualStudio.Shell.IProfileManager> が実装されます。これにより、オプション ページとユーザー設定に対する保持機能が提供されます。 <xref:Microsoft.VisualStudio.Shell.IProfileManager.LoadSettingsFromStorage%2A> メソッドと <xref:Microsoft.VisualStudio.Shell.IProfileManager.SaveSettingsToStorage%2A> メソッドの既定の実装では、プロパティと文字列との間での変換が可能な場合、プロパティの変更がレジストリのユーザー セクションに保持されます。

## <a name="options-page-registry-path"></a>オプション ページのレジストリ パス
 既定では、オプション ページによって管理されるプロパティのレジストリ パスは、<xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A>、DialogPage という文字列、およびオプション ページ クラスの型名を組み合わせることで決定されます。 たとえば、オプション ページ クラスは次のように定義できます。

 :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs" id="Snippet1":::
 :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb" id="Snippet1":::

 <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A> が HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp の場合、プロパティ名と値のペアは、HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp\DialogPage\Company.OptionsPage.OptionsPageGeneral のサブキーになります。

 オプション ページ自体のレジストリ パスは、<xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>、ToolsOptionsPages という文字列、およびオプション ページのカテゴリと名前を組み合わせることで決定されます。 たとえば、Custom オプション ページのカテゴリが My Option Pages、<xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> が HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp である場合、そのオプション ページのレジストリ キーは、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\ToolsOptionsPages\My Option Pages\Custom になります。

## <a name="toolsoptions-page-attributes-and-layout"></a>ツール/オプション ページの属性とレイアウト
 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> 属性を使用すると、 **[オプション]** ダイアログ ボックスのナビゲーション ツリーで、カスタム オプション ページをカテゴリ別にグループ化できます。 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> 属性を使用すると、オプション ページに、インターフェイスを提供する VSPackage を関連付けることができます。 次のコードがあるとします。

:::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs" id="Snippet2":::
:::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb" id="Snippet2":::

 このコードでは、MyPackage で 2 つのオプション ページ (OptionsPageGeneral と OptionsPageCustom) を提供することを宣言しています。 これらのオプション ページは、 **[オプション]** ダイアログ ボックスの **[My Option Pages]** カテゴリに、 **[General]** および **[Custom]** という名前でそれぞれ表示されます。

## <a name="option-attributes-and-layout"></a>オプションの属性とレイアウト
 カスタム オプション ページ内のオプションの外観は、ページに表示されるユーザー インターフェイス (UI) によって決まります。 汎用オプション ページのオプションのレイアウト、ラベル付け、および説明は、次の属性によって決定されます。

- <xref:System.ComponentModel.CategoryAttribute> では、オプションのカテゴリを決定します。

- <xref:System.ComponentModel.DisplayNameAttribute> では、オプションの表示名を決定します。

- <xref:System.ComponentModel.DescriptionAttribute> では、オプションの説明を決定します。

  > [!NOTE]
  > 同等の属性、SRCategory、LocDisplayName、および SRDescription では、ローカライズ用の文字列リソースを使用します。これらは、[マネージド プロジェクトのサンプル](/azure/devops/integrate/index)で定義されています。

  次のコードがあるとします。

  :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/optionspagecustom.cs" id="Snippet3":::
  :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/optionspagegeneral.vb" id="Snippet3":::

  OptionInteger オプションは、オプション ページで、 **[My Options]** カテゴリの **[Integer Option]** として表示されます。 このオプションが選択されると、説明ボックスに「**My integer option**」という説明が表示されます。

## <a name="accessing-options-pages-from-another-vspackage"></a>別の VSPackage からオプション ページにアクセスする
 オプション ページをホストおよび管理する VSPackage には、オートメーション モデルを使って、別の VSPackage からプログラムでアクセスすることもできます。 たとえば、次のコードでは、VSPackage がオプション ページのホストとして登録されています。

 :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs" id="Snippet4":::
 :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb" id="Snippet4":::

 次のコード フラグメントでは、MyOptionPage から OptionInteger の値を取得しています。

 :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs" id="Snippet5":::
 :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb" id="Snippet5":::

 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> 属性でオプション ページが登録されるとき、属性の `SupportsAutomation` 引数が `true` であれば、そのページは AutomationProperties キーの下に登録されます。 オートメーションは、このレジストリ エントリを調べて、関連する VSPackage を見つけます。その後、ホストされているオプション ページ (この場合は My Grid Page) を通じてプロパティにアクセスします。

 オートメーション プロパティのレジストリ パスは、<xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>、AutomationProperties という文字列、およびオプション ページのカテゴリと名前を組み合わせることで決定されます。 たとえば、オプション ページのカテゴリが My Category、名前が My Grid Page、<xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> が HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp である場合、オートメーション プロパティのレジストリ キーは、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\AutomationProperties\My Category\My Grid Page になります。

> [!NOTE]
> 正規名である My Category.My Grid Page は、このキーの Name サブキーの値です。
