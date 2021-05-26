---
title: デザイナーの初期化とメタデータの構成 | Microsoft Docs
description: VSPackage によるデザイナーまたはデザイナー コンポーネントの初期化とそのメタデータの制御を、Visual Studio SDK で容易にする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- designers [Visual Studio SDK], initializing
- designers [Visual Studio SDK], configuring metadata
ms.assetid: f7fe9a7e-f669-4642-ad5d-186b2e6e6ec9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 13c65913fe54b9c22eb8fa374b7a16de84438e33
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091280"
---
# <a name="designer-initialization-and-metadata-configuration"></a>デザイナーの初期化とメタデータの構成

デザイナーまたはデザイナー コンポーネントに関連付けられているメタデータ属性およびフィルター属性を操作すると、さまざまな <xref:System.Type> オブジェクト (データ構造、クラス、グラフィカル エンティティなど) を扱うために特定のデザイナーで使用されるツール、デザイナーを利用できるタイミング、デザイナーをサポートするための Visual Studio IDE の構成 (使用可能な **ツールボックス** カテゴリまたはタブなど) を定義するためのメカニズムがアプリケーションにもたらされます。

[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] には、VSPackage によるデザイナーまたはデザイナー コンポーネントの初期化の制御とそのメタデータの操作を容易にする複数のメカニズムが用意されています。

## <a name="initialize-metadata-and-configuration-information"></a>メタデータと構成情報を初期化する
 これらはオンデマンドで読み込まれるので、デザイナーのインストール前に、Visual Studio 環境で VSPackage が読み込まれていない可能性があります。 このため、VSPackage では、作成時にデザイナーまたはデザイナー コンポーネントを構成するための標準的なメカニズム (<xref:System.ComponentModel.Design.IDesignerEventService.DesignerCreated> イベントを処理するためのもの) は使用できません。 代わりに、VSPackage では、<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> インスタンスのインスタンスを実装し、カスタマイズを提供するために自らを登録します。これをデザイン サーフェイス拡張機能と呼びます。

### <a name="customize-initialization"></a>初期化をカスタマイズする

デザイナー、コンポーネント、またはデザイナー サーフェイスのカスタマイズには次の操作が含まれます。

1. デザイナー メタデータの変更と、特定の <xref:System.Type> にアクセスしたり変換したりする方法の効果的な変更。

    これは通常は <xref:System.Drawing.Design.UITypeEditor> または <xref:System.ComponentModel.TypeConverter> のメカニズムを通じて行われます。

    たとえば、<xref:System.Windows.Forms> ベースのデザイナーが初期化されるときに、Visual Studio 環境では、ファイル システムではなくビットマップを取得するためにリソース マネージャーを使用するデザイナーで使用される <xref:System.Web.UI.WebControls.Image> オブジェクトの <xref:System.Drawing.Design.UITypeEditor> を変更します。

2. イベントのサブスクライブやプロジェクト構成情報の取得などによる環境との統合。 <xref:System.ComponentModel.Design.ITypeResolutionService> インターフェイスを取得すると、プロジェクト構成情報を取得し、イベントをサブスクライブできます。

3. 適切な **ツールボックス** カテゴリのアクティブ化や、<xref:System.ComponentModel.ToolboxItemFilterAttribute> クラスのインスタンスのデザイナーへの適用を通じたデザイナーの適用性の制限によるユーザー環境の変更。

### <a name="designer-initialization-by-a-vspackage"></a>VSPackage によるデザイナーの初期化

VSPackage では、次の操作を行って、デザイナーの初期化を処理する必要があります。

1. <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> クラスを実装するオブジェクトの作成。

   > [!NOTE]
   > <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> クラスは決して、<xref:Microsoft.VisualStudio.Shell.Package> クラスと同じオブジェクト上に実装しないでください。

2. VSPackage のデザイナー拡張機能のサポートの提供として <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> を実装するクラスの登録。 VSPackage による <xref:Microsoft.VisualStudio.Shell.Package> の実装を提供するクラスに、<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute>、<xref:Microsoft.VisualStudio.Shell.ProvideObjectAttribute>、<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> のインスタンスを適用して、クラスを登録します。

デザイナーまたはデザイナー コンポーネントを作成するたびに、Visual Studio 環境では次のように処理します。

- 登録したそれぞれのデザイン サーフェイス拡張機能プロバイダーにアクセスします。

- それぞれのデザイン サーフェイス拡張機能プロバイダーの <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> オブジェクトのインスタンスを作成し初期化します。

- 各デザイン サーフェイス拡張機能プロバイダーの <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnDesignerCreated%2A> メソッドまたは <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnComponentCreated%2A> メソッド (必要に応じて) を呼び出します。

<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> オブジェクトを VSPackage のメンバーとして実装するときに、次の点を把握することが重要です。

- Visual Studio 環境では、特定の `DesignSurfaceExtension` プロバイダーが変更したメタデータや他の構成設定について一切制御しません。 2 つ以上の `DesignSurfaceExtension` プロバイダーが同じデザイナー機能を相反する方法で変更し、最後の変更が決定版になるということはありえます。 どの変更が最後に適用されるかは、不確定です。

- <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> オブジェクトの実装を特定のデザイナーに明示的に制限するには、その実装に <xref:System.ComponentModel.ToolboxItemFilterAttribute> のインスタンスを適用します。 **ツールボックス** 項目のフィルター処理の詳細については、「<xref:System.ComponentModel.ToolboxItemFilterAttribute>」および「<xref:System.ComponentModel.ToolboxItemFilterType>」を参照してください。

## <a name="additional-metadata-provisioning"></a>追加メタデータのプロビジョニング

VSPackage では、デザイン時以外にデザイナーまたはデザイナー コンポーネントの構成を変更できます。

<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> クラスはプログラムで使用することも、デザイナーを提供する VSPackage に適用することもできます。

<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> クラスのインスタンスは、デザイン サーフェイスで作成されたコンポーネントのメタデータを変更するために使用されます。 たとえば、<xref:System.Windows.Forms.CommonDialog> オブジェクトで使用される既定のプロパティ ブラウザーは、カスタム プロパティ ブラウザーに置き換えることができます。

VSPackage による <xref:Microsoft.VisualStudio.Shell.Package> の実装に適用される <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> のインスタンスでもたらされる変更では、次の 2 つのスコープのどちらかを使用できます。

- グローバル -- 指定のコンポーネントのすべての新しいインスタンス用

- ローカル -- 現在の VSPackage で提供されるデザイン サーフェイス上に作成されたコンポーネントのインスタンスにのみ関連。

VSPackage による <xref:Microsoft.VisualStudio.Shell.Package> の実装に適用された <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> インスタンスの `IsGlobal` プロパティによって、このスコープが決定します。

次に示すように、`true` に設定されている <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> オブジェクトの <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute.IsGlobal%2A> プロパティを使用して <xref:Microsoft.VisualStudio.Shell.Package> の実装に属性を適用すると、Visual Studio 環境全体のブラウザーが変更されます。

`[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=true`  `)]`

`internal class MyPackage : Package {}`

グローバル フラグが `false` に設定されている場合、メタデータの変更は、現在の VSPackage でサポートされている現在のデザイナーに対してローカルになります。

`[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=false`  `)]`

`internal class MyPackage : Package {}`

> [!NOTE]
> デザイン サーフェイスはコンポーネントの作成のみをサポートするので、コンポーネントだけがローカル メタデータを保持できます。 上記の例では、オブジェクトの `Color` プロパティなど、プロパティの変更を試みました。 グローバル フラグについて `false` が渡された場合、実際にはデザイナーによって `Color` のインスタンスが作成されないので、`CustomBrowser` は決して表示されません。 グローバル フラグを `false` に設定すると、コントロール、タイマー、ダイアログ ボックスなどのコンポーネントに役立ちます。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>
- <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute>
- <xref:System.ComponentModel.ToolboxItemFilterType>
- [デザイン時サポートの拡張](/previous-versions/37899azc(v=vs.140))