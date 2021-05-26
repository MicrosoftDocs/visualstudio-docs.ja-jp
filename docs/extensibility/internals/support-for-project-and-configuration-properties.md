---
title: プロジェクトおよび構成プロパティのサポート | Microsoft Docs
description: プロジェクトと構成の拡張プロパティを表示できる独自のプロジェクト タイプのプロパティ ページを、Visual Studio IDE で提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project properties, supporting with Visual Studio SDK
- configuration properties, supporting with Visual Studio SDK
ms.assetid: 9fcfaa0f-7b41-4b68-82ec-7a151dca5d7e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6f3932658442774ad6f54bd5e6243fe73679b38f
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106214032"
---
# <a name="support-for-project-and-configuration-properties"></a>プロジェクトおよび構成プロパティのサポート
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) の **[プロパティ]** ウィンドウでは、プロジェクトと構成のプロパティを表示できます。 ユーザーがアプリケーションのプロパティを設定できるように、独自のプロジェクト タイプのプロパティ ページを提供できます。

 **ソリューション エクスプローラー** でプロジェクト ノードを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックすると、プロジェクトと構成のプロパティが含まれるダイアログ ボックスを開くことができます。 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] や [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]、およびこれらの言語から派生したプロジェクト タイプでは、このダイアログ ボックスは、[[全般]、[環境]、[オプション]](../../ide/reference/general-environment-options-dialog-box.md) ダイアログ ボックスのタブ付きページとして表示されます。 詳細については、[Not in Build の「チュートリアル: プロジェクトと構成のプロパティの公開 (C#)」](/previous-versions/bb166517(v=vs.100))を参照してください。

 プロジェクト用 Managed Package Framework (MPFProj) には、新しいプロジェクト システムを作成および管理するためのヘルパー クラスが用意されています。 ソース コードとコンパイルの手順については、[Visual Studio 2013 のプロジェクト用 MPF](https://github.com/tunnelvisionlabs/MPFProj10) に関する記事を参照してください。

## <a name="persistence-of-project-and-configuration-properties"></a>プロジェクトと構成のプロパティの永続性
 プロジェクトと構成のプロパティは、そのプロジェクト タイプに関連付けられたファイル名拡張子を持つプロジェクト ファイルで永続化されます (.csproj、.vbproj、myproj など)。 言語プロジェクトでは、通常、テンプレート ファイルを使用してプロジェクト ファイルを生成します。 ただし実際には、プロジェクト タイプとテンプレートを関連付ける方法はいくつかあります。 詳細については、「[テンプレート ディレクトリの説明 (.Vsdir) ファイル](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)」を参照してください。

 プロジェクトと構成のプロパティは、テンプレート ファイルに項目を追加することによって作成されます。 これらのプロパティは、その後、このテンプレートを使用するプロジェクト タイプを使用して作成されるすべてのプロジェクトで使用できます。 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] プロジェクトと MPFProj はどちらも、テンプレート ファイルについての [Not in Build の「MSBuild の概要」](/previous-versions/visualstudio/visual-studio-2008/ms171452(v=vs.90))のスキーマを使用します。 これらのファイルには、構成ごとに PropertyGroup セクションがあります。 プロジェクトのプロパティは、通常、Configuration 引数が null 文字列に設定されている最初の PropertyGroup セクションで永続化されます。

 次のコードは、基本的な MSBuild プロジェクト ファイルの始めの部分を示しています。

```
<Project MSBuildVersion="2.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
    <Name>SomeProjectSix</Name>
    <SchemaVersion>2.0</SchemaVersion>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">
    <Optimize>false</Optimize>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)' == 'Release' ">
    <Optimize>true</Optimize>
```

 このプロジェクト ファイルでは、`<Name>` と `<SchemaVersion>` がプロジェクト プロパティで、`<Optimize>` が構成プロパティです。

 プロジェクト ファイルのプロジェクトと構成のプロパティの永続化は、プロジェクトで行う必要があります。

> [!NOTE]
> プロジェクトでは、既定値とは異なるプロパティ値のみを永続化することで、永続化を最適化できます。

## <a name="support-for-project-and-configuration-properties"></a>プロジェクトおよび構成プロパティのサポート
 `Microsoft.VisualStudio.Package.SettingsPage` クラスでは、プロジェクトと構成のプロパティ ページを実装します。 `SettingsPage` の既定の実装では、汎用プロパティ グリッド内のユーザーに、パブリック プロパティが提供されます。 `Microsoft.VisualStudio.Package.HierarchyNode.GetPropertyPageGuids` メソッドでは、プロジェクトのプロパティ グリッドの `SettingsPage` から派生したクラスを選択します。 `Microsoft.VisualStudio.Package.ProjectNode.GetConfigPropertyPageGuids` メソッドでは、構成のプロパティ グリッドの `SettingsPage` から派生したクラスを選択します。 プロジェクト タイプでこれらのメソッドをオーバーライドして、適切なプロパティ ページを選択する必要があります。

 `SettingsPage` クラスと `Microsoft.VisualStudio.Package.ProjectNode` クラスでは、プロジェクトと構成のプロパティを永続化するために以下のメソッドが提供されています。

- `Microsoft.VisualStudio.Package.ProjectNode.GetProjectProperty` と `Microsoft.VisualStudio.Package.ProjectNode.SetProjectProperty` ではプロジェクトのプロパティを永続化します。

- `Microsoft.VisualStudio.Package.SettingsPage.GetConfigProperty` と `Microsoft.VisualStudio.Package.SettingsPage.SetConfigProperty` では構成のプロパティを永続化します。

  > [!NOTE]
  > `Microsoft.VisualStudio.Package.SettingsPage` クラスと `Microsoft.VisualStudio.Package.ProjectNode` クラスの実装では、`Microsoft.Build.BuildEngine` (MSBuild) メソッドを使用して、プロジェクト ファイルからプロジェクトと構成のプロパティを取得し、設定します。

  `SettingsPage` から派生させるクラスでは、プロジェクト ファイルのプロジェクトまたは構成のプロパティを永続化するため、`Microsoft.VisualStudio.Package.SettingsPage.ApplyChanges` と `Microsoft.VisualStudio.Package.SettingsPage.BindProperties` を実装する必要があります。

## <a name="provideobjectattribute-and-registry-path"></a>ProvideObjectAttribute とレジストリ パス
 `SettingsPage` から派生したクラスは、VSPackage 間で共有されるように設計されています。 VSPackage で `SettingsPage` から派生したクラスを作成できるようにするには、`Microsoft.VisualStudio.Shell.Package` から派生したクラスに `Microsoft.VisualStudio.Shell.ProvideObjectAttribute` を追加します。

 :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportprojectconfigurationproperties/cs/vssdksupportprojectconfigurationpropertiespackage.cs" id="Snippet1":::
 :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportprojectconfigurationproperties/vb/vssdksupportprojectconfigurationpropertiespackage.vb" id="Snippet1":::

 属性がどの VSPackage アタッチされているかは重要ではありません。 VSPackage が [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に登録されると、<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry.CreateInstance%2A> への呼び出しによってそれを作成できるように、作成できる任意のオブジェクトのクラス ID (CLSID) が登録され ます。

 作成可能なオブジェクトのレジストリ パスは、そのオブジェクト型の <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A>、ワード、CLSID、GUID を組み合わせて決定されます。 `MyProjectPropertyPage` クラスの GUID が {3c693da2-5bca-49b3-bd95-ffe0a39dd723} で、UserRegistryRoot が HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp である場合、レジストリ パスは HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp\CLSID\\{3c693da2-5bca-49b3-bd95-ffe0a39dd723} になります。

## <a name="project-and-configuration-property-attributes-and-layout"></a>プロジェクトと構成のプロパティの属性とレイアウト
 <xref:System.ComponentModel.CategoryAttribute>、<xref:System.ComponentModel.DisplayNameAttribute>、<xref:System.ComponentModel.DescriptionAttribute> の各属性では、汎用プロパティ ページのプロジェクトと構成のプロパティのレイアウト、ラベル付け、説明を指定します。 これらの属性によって、オプションのカテゴリ、表示名、説明がそれぞれ決定されます。

> [!NOTE]
> 同等の属性である SRCategory、LocDisplayName、SRDescription では、ローカライズ用の文字列リソースが使用されます。これらは、[Visual Studio 2013 のプロジェクト用 MPF](https://github.com/tunnelvisionlabs/MPFProj10) で定義されています。

 次のコードがあるとします。

 :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportprojectconfigurationproperties/vb/myprojectpropertypage.vb" id="Snippet2":::
 :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportprojectconfigurationproperties/cs/myprojectpropertypage.cs" id="Snippet2":::

 `MyConfigProp` 構成プロパティは、 **[My Category]** というカテゴリの **[My Config Property]** という構成プロパティ ページに表示されます。 このオプションが選択された場合は、説明パネルに「**My Description**」という説明が表示されます。

## <a name="see-also"></a>関連項目
- [プロパティ ページの追加と削除](../../extensibility/adding-and-removing-property-pages.md)
- [プロジェクト](../../extensibility/internals/projects.md)
- [テンプレート ディレクトリの説明 (.Vsdir) ファイル](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)