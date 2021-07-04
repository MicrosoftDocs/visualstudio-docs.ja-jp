---
title: VSIX 拡張機能スキーマ 2.0 リファレンス | Microsoft Docs
description: VSIX 拡張機能スキーマ 2.0 では、VSIX パッケージのコンテンツを記述する VSIX 配置マニフェスト ファイルのファイル形式を定義します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- vsix
- extension schema
ms.assetid: 0da81b98-f5e3-40d3-ba9a-94551378d0b4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 66393bbe6383fcc6cae942a3d7e86f1d701a9634
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905242"
---
# <a name="vsix-extension-schema-20-reference"></a>VSIX 拡張機能スキーマ 2.0 リファレンス
VSIX 配置マニフェスト ファイルには、VSIX パッケージのコンテンツが記述されます。 ファイル形式は、スキーマによって管理されます。 このスキーマのバージョン 2.0 では、カスタム型および属性の追加がサポートされています。  マニフェストのスキーマは拡張可能です。 マニフェスト ローダーでは、認識されない XML 要素および属性は無視されます。

> [!IMPORTANT]
> Visual Studio 2015 では、Visual Studio 2010、Visual Studio 2012、Visual Studio 2013 形式の VSIX ファイルを読み込むことができます。

## <a name="package-manifest-schema"></a>パッケージ マニフェスト スキーマ
 マニフェスト XML ファイルのルート要素は、`<PackageManifest>` です。 これには、マニフェスト形式のバージョンを示す単一の属性 `Version` が含まれています。 形式に大きな変更が加えられた場合は、バージョンの形式が変更されます。 この記事では、マニフェスト形式のバージョン 2.0 について説明します。これは、マニフェストで `Version` 属性を値 Version="2.0" に設定することで指定されます。

### <a name="packagemanifest-element"></a>PackageManifest 要素
 `<PackageManifest>` ルート要素内では、次の要素を使用できます。

- `<Metadata>` - パッケージ自体に関するメタデータと広告情報。 マニフェストに含めることができる `Metadata` 要素は 1 つだけです。

- `<Installation>` - このセクションでは、この拡張機能パッケージをインストールする方法を定義します。これには、インストール先のアプリケーション SKU も含まれます。 マニフェストに含めることができる `Installation` 要素は 1 つだけです。 マニフェストには `Installation` 要素が必要です。これがない場合、このパッケージはどの SKU にもインストールされません。

- `<Dependencies>` - ここでは、このパッケージの依存関係の省略可能なリストを定義します。

- `<Assets>` - このセクションには、このパッケージに含まれるすべての資産が含まれています。 このセクションを使用しない場合、このパッケージではコンテンツが提示されません。

- `<AnyElement>*` - マニフェスト スキーマは、他の任意の要素を使用できる十分な柔軟性を備えています。 マニフェスト ローダーで認識されない子要素は、拡張機能マネージャー API で追加の XmlElement オブジェクトとして公開されます。 VSIX 拡張機能では、これらの子要素を使用してマニフェスト ファイルに追加のデータを定義し、Visual Studio で実行されるコードから実行時にアクセスできます。 「[Microsoft.VisualStudio.ExtensionManager.IExtension.AdditionalElements](/previous-versions/visualstudio/visual-studio-2013/hh265266(v=vs.120))」を参照してください。

### <a name="metadata-element"></a>Metadata 要素
 このセクションは、パッケージ、その ID、広告情報に関するメタデータです。 `<Metadata>` には、次の要素があります。

- `<Identity>` - このパッケージの識別情報を定義し、次の属性を含んでいます。

  - `Id` - この属性は、作成者によって選択されたパッケージの一意の ID である必要があります。 この名前は、CLR 型を名前空間として使用する場合と同じ方法 (Company.Product.Feature.Name) で修飾する必要があります。 `Id` 属性は 100 文字までに制限されています。

  - `Version` - このパッケージとそのコンテンツのバージョンを定義します。 この属性は、CLR アセンブリのバージョン管理形式 (Major.Minor.Build.Revision) に従います (1.2.40308.00)。 バージョン番号が大きいパッケージは、パッケージの更新プログラムと見なされ、インストールされている既存のバージョンに上書きインストールできます。

  - `Language` - この属性は、パッケージの既定の言語であり、このマニフェストのテキスト データに対応します。 この属性は、リソース アセンブリの CLR ロケール コード規則 (en-us、en、fr-fr など) に従います。 `neutral` を指定すると、任意のバージョンの Visual Studio で実行される言語に依存しない拡張機能を宣言できます。 既定値は `neutral` です。

  - `Publisher` - この属性では、このパッケージの発行元 (会社または個人名のいずれか) を識別します。 `Publisher` 属性は 100 文字までに制限されています。

- `<DisplayName>` - この要素では、拡張機能マネージャーの UI に表示されるパッケージのユーザーフレンドリ名を指定します。 `DisplayName` の内容は 50 文字までに制限されています。

- `<Description>` - この省略可能な要素は、拡張機能マネージャーの UI に表示されるパッケージとそのコンテンツの簡単な説明です。 `Description` の内容には任意のテキストを含めることができますが、使用できる文字数は最大 1000 文字です。

- `<MoreInfo>` - この省略可能な要素は、このパッケージの詳しい説明を含むオンライン ページの URL です。 プロトコルは http として指定する必要があります。

- `<License>` - この省略可能な要素は、パッケージに含まれているライセンス ファイル (.txt、.rtf) への相対パスです。

- `<ReleaseNotes>` - この省略可能な要素は、パッケージ (.txt、.rtf) に含まれているリリース ノート ファイルへの相対パスまたはリリース ノートを表示する Web サイトの URL のいずれかです。

- `<Icon>` - この省略可能な要素は、パッケージに含まれているイメージ ファイル (png、bmp、jpeg、ico) への相対パスです。 アイコン イメージは、32 x 32 ピクセルである必要があり (そうでない場合は、そのサイズに縮小されます)、リスト ビュー UI に表示されます。 `Icon` 要素が指定されていない場合、UI では既定値が使用されます。

- `<PreviewImage>` - この省略可能な要素は、パッケージに含まれているイメージ ファイル (png、bmp、jpeg) への相対パスです。 プレビュー イメージは、200 x 200 ピクセルである必要があり、詳細 UI に表示されます。 `PreviewImage` 要素が指定されていない場合、UI では既定値が使用されます。

- `<Tags>` - この省略可能な要素では、検索ヒントに使用される、セミコロンで区切られた追加のテキスト タグをリストします。 `Tags` 要素は 100 文字までに制限されています。

- `<GettingStartedGuide>` - この省略可能な要素は、このパッケージ内の拡張機能またはコンテンツの使用方法に関する情報を含む HTML ファイルへの相対パスまたは Web サイトの URL のいずれかです。 このガイドはインストールの一部として起動されます。

- `<AnyElement>*` - マニフェスト スキーマは、他の任意の要素を使用できる十分な柔軟性を備えています。 マニフェスト ローダーで認識されない子要素は、XmlElement オブジェクトのリストとして公開されます。 VSIX 拡張機能では、マニフェスト ファイルでこれらの子要素を使用して追加のデータを定義し、実行時にそれらを列挙できます。

### <a name="installation-element"></a>Installation 要素
 このセクションでは、この拡張機能パッケージをインストールする方法とインストール先のアプリケーション SKU を定義します。 このセクションには、次の属性があります。

- `Experimental` - 現在すべてのユーザーに対して拡張機能がインストールされているが、同じコンピューターで更新されたバージョンを開発する場合は、この属性を true に設定します。 たとえば、すべてのユーザーに対して MyExtension 1.0 がインストールされているが、同じコンピューターで MyExtension 2.0 をデバッグする場合は、Experimental="true" に設定します。 この属性は、Visual Studio 2015 Update 1 以降で使用できます。

- `Scope` - この属性には、値 "Global" または "ProductExtension" を指定できます。

  - "Global" では、インストールの範囲が特定の SKU に限定されないことを指定します。 たとえば、この値は拡張機能 SDK をインストールするときに使用されます。

  - "ProductExtension" では、従来の VSIX 拡張機能 (バージョン 1.0) を個別の Visual Studio SKU に範囲を限定してインストールすることを指定します。 これが既定値です。

- `AllUsers` - この省略可能な属性では、このパッケージをすべてのユーザーに対してインストールするかどうかを指定します。 既定では、この属性はパッケージがユーザー単位であることを指定する false です。 (この値を true に設定した場合、インストールするユーザーは、結果として得られる VSIX をインストールするために管理特権レベルに昇格する必要があります。

- `InstalledByMsi` - この省略可能な属性では、このパッケージが MSI によってインストールされるかどうかを指定します。 MSI によってインストールされるパッケージは、Visual Studio 拡張機能マネージャーではなく、MSI ([プログラムと機能]) によってインストールおよび管理されます。  既定では、この属性はパッケージが MSI によってインストールされないことを指定する false です。

- `SystemComponent` - この省略可能な属性では、このパッケージをシステム コンポーネントと見なす必要があるかどうかを指定します。 システム コンポーネントは、拡張機能マネージャーの UI に表示されないため、更新できません。 既定では、この属性はパッケージがシステム コンポーネントではないことを指定する false です。

- `AnyAttribute*` - `Installation` 要素では、名前と値のペアのディクショナリとして実行時に公開される無制限の属性セットを受け入れます。

- `<InstallationTarget>` - この要素では、VSIX インストーラーでパッケージをインストールする場所を制御します。 `Scope` 属性の値が "ProductExtension" の場合、パッケージのターゲットは、その可用性を拡張機能に提供するためにそのコンテンツの一部としてマニフェスト ファイルがインストールされている SKU である必要があります。 `Scope` 属性の値が明示的な (または既定の) "ProductExtension" である場合、`<InstallationTarget>` 要素には次の属性が含まれます。

  - `Id` - この属性では、パッケージを識別します。  この属性は、名前空間規則 (Company.Product.Feature.Name) に従います。 `Id` 属性に使用できるのは英数字のみで、100 文字までに制限されています。 期待される値:

    - Microsoft.VisualStudio.IntegratedShell

    - Microsoft.VisualStudio.Pro

    - Microsoft.VisualStudio.Premium

    - Microsoft.VisualStudio.Ultimate

    - Microsoft.VisualStudio.VWDExpress

    - Microsoft.VisualStudio.VPDExpress

    - Microsoft.VisualStudio.VSWinExpress

    - Microsoft.VisualStudio.VSLS

    - My.Shell.App

  - `Version` - この属性では、この SKU のサポートされる最小および最大バージョンを含むバージョン範囲を指定します。 パッケージでは、サポートされる SKU のバージョンの詳細を示すことができます。 バージョン範囲の表記は [10.0-11.0] です。ここで

    - [ - 最小バージョン (その値を含む)。

    - ] - 最大バージョン (その値を含む)。

    - ( - 最小バージョン (その値を含まない)。

    - ) - 最大バージョン (その値を含まない)。

    - 単一のバージョン番号 - 指定されたバージョンのみ。

    > [!IMPORTANT]
    > Visual Studio 2012 で VSIX スキーマのバージョン 2.0 が導入されました。 このスキーマを使用するには、コンピューターに Visual Studio 2012 以降がインストールされていて、その製品の一部である VSIXInstaller.exe を使用する必要があります。 Visual Studio 2012 以降の VSIXInstaller では以前のバージョンの Visual Studio をターゲットにできますが、新しいバージョンのインストーラーを使用する必要があります。

    Visual Studio 2017 のバージョン番号については、「[Visual Studio のビルド番号とリリース日](../install/visual-studio-build-numbers-and-release-dates.md)」を参照してください。

    Visual Studio 2017 リリースのバージョンを表現する場合、マイナー バージョンは常に **0** にする必要があります。 たとえば、Visual Studio 2017 バージョン 15.3.26730.0 は、[15.0.26730.0,16.0) と表現する必要があります。 これは、Visual Studio 2017 以降のバージョン番号にのみ必要です。

  - `AnyAttribute*` - `<InstallationTarget>` 要素では、名前と値のペアのディクショナリとして実行時に公開される無制限の属性セットを使用できます。

### <a name="dependencies-element"></a>Dependencies 要素
 この要素には、このパッケージで宣言する依存関係のリストが含まれています。 依存関係が指定されている場合は、(`Id` によって識別される) それらのパッケージが先にインストールされている必要があります。

- `<Dependency>` 要素 - この子要素には、次の属性があります。

  - `Id` - この属性は、依存パッケージの一意の ID である必要があります。 この ID 値は、このパッケージが依存しているパッケージの `<Metadata><Identity>Id` 属性と一致している必要があります。 `Id` 属性は、名前空間規則 (Company.Product.Feature.Name) に従います。 この属性に使用できるのは英数字のみで、100 文字までに制限されています。

  - `Version` - この属性では、この SKU のサポートされる最小および最大バージョンを含むバージョン範囲を指定します。 パッケージでは、サポートされる SKU のバージョンの詳細を示すことができます。 バージョン範囲の表記は [12.0, 13.0] です。ここで:

    - [ - 最小バージョン (その値を含む)。

    - ] - 最大バージョン (その値を含む)。

    - ( - 最小バージョン (その値を含まない)。

    - ) - 最大バージョン (その値を含まない)。

    - 単一のバージョン番号 - 指定されたバージョンのみ。

  - `DisplayName` - この属性は、ダイアログ ボックスやエラーメッセージなどの UI 要素で使用される依存パッケージの表示名です。 依存パッケージが MSI によってインストールされる場合を除き、この属性は省略可能です。

  - `Location` - この省略可能な属性では、この VSIX 内で入れ子になった VSIX パッケージへの相対パスまたは依存関係のダウンロード先の URL のいずれかを指定します。 この属性は、ユーザーが前提条件となるパッケージを見つけやすくするために使用されます。

  - `AnyAttribute*` - `Dependency` 要素では、名前と値のペアのディクショナリとして実行時に公開される無制限の属性セットを受け入れます。

### <a name="assets-element"></a>Assets 要素
 この要素には、このパッケージによって提示される各拡張機能またはコンテンツ要素の `<Asset>` タグのリストが含まれています。

- `<Asset>` - この要素には、次の属性と要素が含まれています。

  - `Type` - この要素によって表される拡張機能またはコンテンツの種類。 各 `<Asset>` 要素に 1 つの `Type` を含める必要がありますが、複数の `<Asset>` 要素に同じ `Type` を含めることもできます。 この属性は、名前空間規則に従って完全修飾名として表す必要があります。 既知の種類は次のとおりです。

    1. Microsoft.VisualStudio.VsPackage

    2. Microsoft.VisualStudio.MefComponent

    3. Microsoft.VisualStudio.ToolboxControl

    4. Microsoft.VisualStudio.Samples

    5. Microsoft.VisualStudio.ProjectTemplate

    6. Microsoft.VisualStudio.ItemTemplate

    7. Microsoft.VisualStudio.Assembly

       独自の種類を作成し、一意の名前を指定できます。 Visual Studio 内での実行時に、コードで拡張機能マネージャー API を使用して、これらのカスタムの種類を列挙し、それらにアクセスできます。

  - `Path` - この資産を含むパッケージ内のファイルまたはフォルダーへの相対パス。

  - `TargetVersion` - 指定された資産が適用されるバージョン範囲。 複数のバージョンの資産を異なるバージョンの Visual Studio に配布するために使用されます。 Visual Studio 2017.3 以降が有効になっている必要があります。

  - `AnyAttribute*` - 名前と値のペアのディクショナリとして実行時に公開される無制限の属性セット。

    `<AnyElement>*` - `<Asset>` の開始および終了タグの間には、任意の構造化されたコンテンツを含めることができます。 すべての要素は、XmlElement オブジェクトのリストとして公開されます。 VSIX 拡張機能では、マニフェスト ファイルで構造化された種類固有のメタデータを定義し、実行時にそれらを列挙できます。

### <a name="sample-manifest"></a>サンプル マニフェスト

```xml
<?xml version="1.0" encoding="utf-8"?>
<PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011" xmlns:d="http://schemas.microsoft.com/developer/vsx-schema-design/2011">
  <Metadata>
    <Identity Id="0000000-0000-0000-0000-000000000000" Version="1.0" Language="en-US" Publisher="Company" />
    <DisplayName>Test Package</DisplayName>
    <Description>Information about my package</Description>
    <MoreInfo>http://www.fabrikam.com/Extension1/</MoreInfo>
    <License>eula.rtf</License>
    <ReleaseNotes>notes.txt</ReleaseNotes>
    <Icon>Images\icon.png</Icon>
    <PreviewImage>Images\preview.png</PreviewImage>
  </Metadata>
  <Installation InstalledByMsi="false" AllUsers="false" SystemComponent="false" Scope="ProductExtension">
    <InstallationTarget Id="Microsoft.VisualStudio.Pro" Version="[11.0, 12.0]" />
  </Installation>
  <Dependencies>
    <Dependency Id="Microsoft.Framework.NDP" DisplayName="Microsoft .NET Framework" d:Source="Manual" Version="[4.5,)" />
    <Dependency Id="Microsoft.VisualStudio.MPF.12.0" DisplayName="Visual Studio MPF 12.0" d:Source="Installed" Version="[12.0]" />
  </Dependencies>
  <Assets>
    <Asset Type="Microsoft.VisualStudio.VsPackage" d:Source="Project" d:ProjectName="%CurrentProject%" Path="|%CurrentProject%;PkgdefProjectOutputGroup|" />
  </Assets>
</PackageManifest>
```

## <a name="see-also"></a>関連項目

- [Visual Studio 拡張機能を配布する](../extensibility/shipping-visual-studio-extensions.md)
