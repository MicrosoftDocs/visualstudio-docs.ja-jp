---
title: VSIX 拡張機能スキーマ2.0 リファレンス |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- vsix
- extension schema
ms.assetid: 0da81b98-f5e3-40d3-ba9a-94551378d0b4
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9333f2fb1bff0fdb8a3f0dac8004f66156b8863d
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68870820"
---
# <a name="vsix-extension-schema-20-reference"></a>VSIX 拡張機能スキーマ2.0 リファレンス
Vsix 配置マニフェストファイルは、VSIX パッケージの内容を記述します。 ファイル形式は、スキーマによって管理されます。 このスキーマのバージョン2.0 では、カスタム型と属性の追加がサポートされています。  マニフェストのスキーマは拡張可能です。 マニフェストローダーは、認識されない XML 要素と属性を無視します。

> [!IMPORTANT]
> Visual Studio 2015 では、visual Studio 2010、Visual Studio 2012、Visual Studio 2013 形式で VSIX ファイルを読み込むことができます。

## <a name="package-manifest-schema"></a>パッケージマニフェストスキーマ
 マニフェスト XML ファイルのルート要素は`<PackageManifest>`です。 これには、マニフェスト`Version`形式の1つの属性があります。 形式に大きな変更が加えられた場合は、バージョンの形式が変更されます。 この記事では、マニフェストで指定されるマニフェスト形式バージョン2.0 について`Version`説明します。これは、属性を version = "2.0" の値に設定することによって行います。

### <a name="packagemanifest-element"></a>PackageManifest 要素
 `<PackageManifest>`ルート要素内では、次の要素を使用できます。

- `<Metadata>`-パッケージ自体に関するメタデータと広告情報。 マニフェストで`Metadata`許可される要素は1つだけです。

- `<Installation>`-このセクションでは、この拡張機能パッケージをインストールする方法を定義します。これには、インストール可能なアプリケーション Sku も含まれます。 マニフェストで許可`Installation`される要素は1つだけです。 マニフェストには`Installation`要素が必要です。または、このパッケージはどの SKU にもインストールされません。

- `<Dependencies>`-このパッケージの依存関係のオプションの一覧は、ここで定義されています。

- `<Assets>`-このセクションには、このパッケージに含まれるすべての資産が含まれています。 このセクションを使用しない場合、このパッケージはコンテンツを表示しません。

- `<AnyElement>*`-マニフェストスキーマは、他の要素を許可するのに十分な柔軟性を備えています。 マニフェストローダーによって認識されない子要素は、拡張機能マネージャー API で追加の XmlElement オブジェクトとして公開されます。 VSIX 拡張機能では、これらの子要素を使用して、Visual Studio で実行されるコードが実行時にアクセスできるマニフェストファイルに追加のデータを定義できます。 「 [VisualStudio](/previous-versions/visualstudio/visual-studio-2013/hh265266(v=vs.120))」を参照してください。

### <a name="metadata-element"></a>Metadata 要素
 このセクションは、パッケージ、その id、および広告情報に関するメタデータです。 `<Metadata>`には、次の要素が含まれています。

- `<Identity>`-このパッケージの識別情報を定義します。次の属性が含まれています。

  - `Id`-この属性は、作成者によって選択されたパッケージの一意の ID である必要があります。 CLR 型の名前空間と同じ方法で名前を修飾する必要があります。Company.Product.Feature.Name。 属性`Id`は、100文字までに制限されています。

  - `Version`-このパッケージのバージョンとそのコンテンツを定義します。 この属性は、CLR アセンブリのバージョン管理形式に従います。Major. Minor. Build. Revision (1.2.40308.00)。 バージョン番号が高いパッケージは、パッケージの更新プログラムと見なされ、インストールされている既存のバージョンを介してインストールできます。

  - `Language`-この属性はパッケージの既定の言語であり、このマニフェストのテキストデータに対応します。 この属性は、リソースアセンブリの CLR ロケールコード規則に従います。たとえば、en-us、en、fr-fr などです。 任意のバージョン`neutral`の Visual Studio で実行される言語に依存しない拡張機能を宣言するように、を指定できます。 既定値は `neutral` です。

  - `Publisher`-この属性は、このパッケージの発行元 (会社名または個人名) を識別します。 属性`Publisher`は、100文字までに制限されています。

- `<DisplayName>`-この要素は、拡張機能マネージャーの UI に表示されるユーザーフレンドリなパッケージ名を指定します。 コンテンツ`DisplayName`は50文字までに制限されています。

- `<Description>`-この省略可能な要素は、拡張機能マネージャーの UI に表示されるパッケージとその内容の簡単な説明です。 コンテンツ`Description`には任意のテキストを含めることができますが、1000文字までに制限されています。

- `<MoreInfo>`-この省略可能な要素は、このパッケージの完全な説明を含むページオンラインの URL です。 プロトコルは http として指定する必要があります。

- `<License>`-この省略可能な要素は、パッケージに含まれているライセンスファイル (.txt、.rtf) への相対パスです。

- `<ReleaseNotes>`-この省略可能な要素は、パッケージ (.txt、.rtf) に含まれているリリースノートファイルへの相対パスか、リリースノートを表示する web サイトの URL です。

- `<Icon>`-この省略可能な要素は、パッケージに含まれているイメージファイル (png、bmp、jpeg、ico) への相対パスです。 アイコンイメージは32x32 ピクセルである必要があります (またはそのサイズに縮小されます)。また、listview UI に表示されます。 要素が`Icon`指定されていない場合、UI は既定値を使用します。

- `<PreviewImage>`-この省略可能な要素は、パッケージに含まれているイメージファイル (png、bmp、jpeg) への相対パスです。 プレビューイメージは 200 x 200 ピクセルで、詳細 UI に表示されます。 要素が`PreviewImage`指定されていない場合、UI は既定値を使用します。

- `<Tags>`-この省略可能な要素は、検索ヒントに使用される、セミコロンで区切られた追加のテキストタグを一覧表示します。 要素`Tags`の文字数は100文字に制限されています。

- `<GettingStartedGuide>`-この省略可能な要素は、HTML ファイルへの相対パスか、このパッケージ内の拡張機能またはコンテンツの使用方法に関する情報を含む web サイトの URL です。 このガイドは、のインストールの一部として起動されます。

- `<AnyElement>*`-マニフェストスキーマは、他の要素を許可するのに十分な柔軟性を備えています。 マニフェストローダーによって認識されない子要素は、XmlElement オブジェクトのリストとして公開されます。 VSIX 拡張機能では、これらの子要素を使用して、マニフェストファイルに追加のデータを定義し、実行時にそれらを列挙できます。

### <a name="installation-element"></a>インストール要素
 このセクションでは、このパッケージをインストールする方法、およびインストール可能なアプリケーション Sku を定義します。 ここでは、次の属性について説明します。

- `Experimental`-すべてのユーザーに対して現在インストールされている拡張機能があり、同じコンピューターで更新されたバージョンを開発している場合は、この属性を true に設定します。 たとえば、すべてのユーザーに対して MyExtension 1.0 をインストールしていても、同じコンピューターで MyExtension 2.0 をデバッグする場合は、実験的 = "true" に設定します。 この属性は、Visual Studio 2015 Update 1 以降で使用できます。

- `Scope`-この属性には、"Global" または "ProductExtension" の値を指定できます。

  - "Global" は、インストールの範囲が特定の SKU に限定されないことを指定します。 たとえば、この値は拡張 SDK がインストールされているときに使用されます。

  - "ProductExtension" は、個別の Visual Studio Sku を対象とした従来の VSIX 拡張機能 (バージョン 1.0) がインストールされていることを指定します。 これが既定値です。

- `AllUsers`-この省略可能な属性は、このパッケージをすべてのユーザーにインストールするかどうかを指定します。 既定では、この属性は false です。これは、パッケージがユーザー単位であることを指定します。 (この値を true に設定すると、インストールするユーザーは、結果として得られる VSIX をインストールするために、管理特権レベルに昇格する必要があります。

- `InstalledByMsi`-このオプションの属性は、このパッケージが MSI によってインストールされるかどうかを指定します。 MSI によってインストールされたパッケージは、Visual Studio 拡張機能マネージャーではなく、MSI (プログラムおよび機能) によってインストールおよび管理されます。  既定では、この属性は false です。これは、パッケージが MSI によってインストールされないことを指定します。

- `SystemComponent`-この省略可能な属性は、このパッケージをシステムコンポーネントと見なす必要があるかどうかを指定します。 システムコンポーネントは、拡張機能マネージャーの UI に表示されないため、更新できません。 既定では、この属性は false です。これは、パッケージがシステムコンポーネントではないことを指定します。

- `AnyAttribute*`-要素`Installation`は、実行時に名前と値のペアのディクショナリとして公開される、オープンエンドの属性のセットを受け入れます。

- `<InstallationTarget>`-この要素は、VSIX インストーラーによってパッケージがインストールされる場所を制御します。 `Scope`属性の値が "productextension" の場合、パッケージは SKU をターゲットにする必要があります。これにより、マニフェストファイルがコンテンツの一部としてインストールされ、拡張機能への可用性が提供されます。 属性に明示的な値または既定値 "productextension" が指定されて`<InstallationTarget>`いる場合、要素には次の属性が`Scope`あります。

  - `Id`-この属性は、パッケージを識別します。  属性は、名前空間の規則に従います。Company.Product.Feature.Name。 属性`Id`に使用できるのは英数字のみで、100文字までに制限されています。 予期される値:

    - VisualStudio (Microsoft.)

    - Microsoft.VisualStudio.Pro

    - VisualStudio

    - VisualStudio

    - VisualStudio. VWDExpress

    - VisualStudio. VPDExpress

    - VisualStudio. VSWinExpress

    - VisualStudio. VSLS

    - App.xaml

  - `Version`-この属性は、この SKU のサポートされている最小バージョンと最大バージョンを含むバージョン範囲を指定します。 パッケージは、サポートされている Sku のバージョンを詳細に示すことができます。 バージョン範囲の表記は [10.0-11.0] で、ここでは

    - [-最小バージョンを含みます。

    - ]-最大バージョンを含みます。

    - (-最小バージョン排他。

    - )-最大バージョン排他。

    - 単一バージョン #-指定されたバージョンのみ。

    > [!IMPORTANT]
    > バージョン2.0 の VSIX スキーマは、Visual Studio 2012 で導入されました。 このスキーマを使用するには、コンピューターに Visual Studio 2012 以降がインストールされていて、その製品の一部である VSIXInstaller を使用している必要があります。 以前のバージョンの Visual Studio は、Visual Studio 2012 以降 VSIXInstaller を使用して対象にすることができますが、それ以降のバージョンのインストーラーでのみ使用できます。

    Visual Studio 2017 のバージョン番号につい[ては、「Visual studio のビルド番号とリリース日](../install/visual-studio-build-numbers-and-release-dates.md)」を参照してください。

    Visual Studio 2017 リリースのバージョンを表現する場合、マイナーバージョンは常に**0**にする必要があります。 たとえば、Visual Studio 2017 バージョン15.3.26730.0 は、[15.0.26730.0, 16.0) として表現する必要があります。 これは、Visual Studio 2017 以降のバージョン番号にのみ必要です。

  - `AnyAttribute*`-要素`<InstallationTarget>`は、実行時に名前と値のペアのディクショナリとして公開される属性のオープンエンドのセットを許可します。

### <a name="dependencies-element"></a>Dependencies 要素
 この要素には、このパッケージが宣言する依存関係の一覧が含まれています。 依存関係が指定されている場合は、その`Id`パッケージ (によって識別される) がの前にインストールされている必要があります。

- `<Dependency>`要素-この子要素には、次の属性があります。

  - `Id`-この属性は、依存パッケージの一意の ID である必要があります。 この id 値は、 `<Metadata><Identity>Id`このパッケージが依存しているパッケージの属性と一致している必要があります。 属性`Id`は、名前空間の規則に従います。Company.Product.Feature.Name。 属性に使用できるのは英数字のみで、100文字までに制限されています。

  - `Version`-この属性は、この SKU のサポートされている最小バージョンと最大バージョンを含むバージョン範囲を指定します。 パッケージは、サポートされている Sku のバージョンを詳細に示すことができます。 バージョン範囲の表記は [12.0, 13.0] で、次のようになります。

    - [-最小バージョンを含みます。

    - ]-最大バージョンを含みます。

    - (-最小バージョン排他。

    - )-最大バージョン排他。

    - 単一バージョン #-指定されたバージョンのみ。

  - `DisplayName`-この属性は、ダイアログボックスやエラーメッセージなどの UI 要素で使用される依存パッケージの表示名です。 依存パッケージが MSI によってインストールされている場合を除き、属性は省略可能です。

  - `Location`-この省略可能な属性は、この VSIX 内で入れ子になった VSIX パッケージへの相対パス、または依存関係のダウンロード先の URL を指定します。 この属性は、ユーザーが前提条件となるパッケージを見つけられるようにするために使用されます。

  - `AnyAttribute*`-要素`Dependency`は、実行時に名前と値のペアのディクショナリとして公開される、オープンエンドの属性のセットを受け入れます。

### <a name="assets-element"></a>Assets 要素
 この要素には、この`<Asset>`パッケージによって表示される各拡張機能またはコンテンツ要素のタグの一覧が含まれます。

- `<Asset>`-この要素には、次の属性と要素が含まれています。

  - `Type`-この要素によって表される拡張機能またはコンテンツの型。 各`<Asset>`要素には1つ`Type`のが必要`<Asset>`ですが、複数の`Type`要素が同じである場合があります。 この属性は、名前空間の規則に従って、完全修飾名として表す必要があります。 既知の型は次のとおりです。

    1. VisualStudio. VsPackage

    2. Microsoft.VisualStudio.MefComponent

    3. VisualStudio. ToolboxControl

    4. VisualStudio

    5. VisualStudio テンプレート

    6. VisualStudio

    7. VisualStudio

       独自の型を作成し、一意の名前を付けることができます。 Visual Studio 内の実行時に、コードは拡張機能マネージャー API を使用して、これらのカスタム型を列挙してアクセスできます。

  - `Path`-アセットを含むパッケージ内のファイルまたはフォルダーへの相対パス。

  - `TargetVersion`-指定された資産が適用されるバージョン範囲。 複数のバージョンのアセットを異なるバージョンの Visual Studio に配布するために使用されます。 Visual Studio 2017.3 以降が有効になっている必要があります。

  - `AnyAttribute*`-実行時に名前と値のペアのディクショナリとして公開される、オープンエンドの属性のセット。

    `<AnyElement>*`-開始タグと終了タグの間`<Asset>`には、構造化されたコンテンツを使用できます。 すべての要素は、XmlElement オブジェクトのリストとして公開されます。 VSIX 拡張機能は、マニフェストファイルで構造化型固有のメタデータを定義し、実行時にそれらを列挙できます。

### <a name="sample-manifest"></a>サンプルマニフェスト

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

- [Visual Studio 拡張機能を出荷する](../extensibility/shipping-visual-studio-extensions.md)
