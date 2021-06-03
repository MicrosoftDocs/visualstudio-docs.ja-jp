---
title: プロジェクト項目でのパッケージ化と配置の情報
description: フィーチャー プロパティ、フィーチャー レシーバー、プロジェクト出力参照、安全なコントロール エンティティを使用して、SharePoint プロジェクト項目にパッケージ化および配置データを追加します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.SafeControlEntries
- VS.SharePointTools.Project.ProjectOutputReference
- VS.SharePointTools.Project.FeatureProperties
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, safe controls
- project output references [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, feature properties
- SharePoint development in Visual Studio, project output references
- SharePoint development in Visual Studio, advanced packaging tools
- feature properties [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, feature receiver
- feature receiver [SharePoint development in Visual Studio]
- safe controls [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f05e2035338ea4c2d0e45bb9d135d618b938e4ca
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889539"
---
# <a name="provide-packaging-and-deployment-information-in-project-items"></a>プロジェクト項目でのパッケージ化と配置の情報を提供する
  [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のすべての SharePoint プロジェクト項目には、プロジェクトを SharePoint に配置するときに追加データを提供するために使用できるプロパティがあります。 選択できるプロパティは次のとおりです。

- 機能プロパティ

- フィーチャー レシーバー

- プロジェクト出力参照

- 安全なコントロール エントリ

  これらのプロパティは、 **[プロパティ]** ウィンドウに表示されます。

## <a name="feature-properties"></a>機能のプロパティ
 フィーチャーによって使用されるデータを指定するには、**フィーチャー プロパティ** プロパティを使用します。 フィーチャー プロパティのデータは、フィーチャーが SharePoint に配置されるときに一緒に含まれる (キー/値ペアとして格納される) 一連の値です。 フィーチャーが配置されると、そのプロパティ値にコードでアクセスできるようになります。

 フィーチャー プロパティの値をプロジェクト項目に追加すると、その値は項目のフィーチャーのマニフェストに要素として追加されます。 たとえば、Business Data Connectivity (BDC) モデル プロジェクトでは、ModelFileName フィーチャー プロパティが次のように表示されます。

```xml
<Property Key="ModelFileName" Value="BdcModel1\BdcModel1.bdcm" />
```

 フィーチャー プロパティの値を設定すると、それがプロジェクトの *.spdata* ファイルに FeatureProperty 要素として追加されます。 SharePoint でのプロパティへのアクセスの詳細については、「[SPFeaturePropertyCollection クラス](/previous-versions/office/sharepoint-server/ms461895(v=office.15))」を参照してください。

 すべてのプロジェクト項目の同じフィーチャー プロパティ値は、フィーチャー マニフェストにマージされます。 ただし、2 つの異なるプロジェクト項目で同じフィーチャー プロパティ キーが指定され、その値が一致しない場合は、検証エラーが発生します。

 フィーチャー プロパティをフィーチャー ファイル ( *.feature*) に直接追加するには、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint オブジェクト モデルの <xref:Microsoft.VisualStudio.SharePoint.Features.IPropertyCollection.Add%2A> メソッドを呼び出します。 この方法を使用する場合は、フィーチャー プロパティに同じフィーチャー プロパティ値を追加する場合と同じルールが、フィーチャー ファイルに直接追加されたプロパティにも適用されることにご注意ください。

## <a name="feature-receiver"></a>フィーチャー レシーバー
 フィーチャー レシーバーは、プロジェクト項目に含まれているフィーチャーで特定のイベントが発生した場合に実行されるコードです。 たとえば、フィーチャーをインストール、アクティブ化、またはアップグレードしたときに実行されるフィーチャー レシーバーを定義できます。 フィーチャー レシーバーを追加する方法の 1 つは、「[チュートリアル: フィーチャー イベント レシーバーを追加する](../sharepoint/walkthrough-add-feature-event-receivers.md)」の説明に従って、それをフィーチャーに直接追加することです。 もう 1 つの方法は、フィーチャー レシーバー クラスの名前とアセンブリを **フィーチャー レシーバー** プロパティで参照することです。

### <a name="direct-method"></a>ダイレクト メソッド
 フィーチャー レシーバーをフィーチャーに直接追加すると、ソリューション エクスプローラーの **[フィーチャー]** ノードの下にコード ファイルが配置されます。 SharePoint ソリューションをビルドすると、このコードがアセンブリにコンパイルされ、SharePoint に配置されます。 既定では、**レシーバー アセンブリ** および **レシーバー クラス** フィーチャー プロパティでクラス名とアセンブリが参照されます。

### <a name="reference-method"></a>Reference メソッド
 フィーチャー レシーバーを追加するもう 1 つの方法は、プロジェクト項目の **フィーチャー レシーバー** プロパティを使用してフィーチャー レシーバー アセンブリを参照することです。 フィーチャー レシーバー プロパティ値には、**アセンブリ** と **クラス名** という 2 つのサブプロパティがあります。 アセンブリには完全修飾された "厳密な" 名前を使用する必要があり、クラス名は完全な型名である必要があります。 詳細については、「[厳密な名前付きアセンブリ](/previous-versions/dotnet/netframework-4.0/wd40t7ad(v=vs.100))」を参照してください。 ソリューションを SharePoint に配置した後、このフィーチャーでは、参照されているフィーチャー レシーバーを使用してフィーチャー イベントを処理します。

 ソリューションのビルド時に、フィーチャーとそのプロジェクトのフィーチャー レシーバー プロパティの値が結合され、SharePoint ソリューション ( *.wsp*) ファイルのフィーチャー マニフェスト内の Feature 要素の ReceiverAssembly および ReceiverClass 属性が設定されます。 したがって、プロジェクト項目とフィーチャーの両方のアセンブリおよびクラス名プロパティの値が指定されている場合は、プロジェクト項目とフィーチャーのプロパティ値が一致する必要があります。 値が一致しない場合は、検証エラーが表示されます。 フィーチャーで使用されているものとは異なるフィーチャー レシーバー アセンブリをプロジェクト項目で参照する必要がある場合は、それを別のフィーチャーに移動します。

 サーバー上にまだ存在しないフィーチャー レシーバー アセンブリを参照する場合は、アセンブリ ファイル自体もパッケージに含める必要もあります。[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ではこれを自動的に追加しません。 このフィーチャーを配置すると、アセンブリ ファイルはシステムの [!INCLUDE[TLA#tla_gac](../sharepoint/includes/tlasharptla-gac-md.md)] または SharePoint 物理ディレクトリの Bin フォルダーにコピーされます。 詳細については、「[方法: アセンブリを追加および削除する](../sharepoint/how-to-add-and-remove-additional-assemblies.md)」を参照してください。

 フィーチャー レシーバーの詳細については、「[フィーチャー イベント レシーバー](/previous-versions/office/developer/sharepoint-2007/bb862634(v=office.12))」と「[フィーチャー イベント](/previous-versions/office/developer/sharepoint-2010/ms469501(v=office.14))」を参照してください。

## <a name="project-output-references"></a>プロジェクト出力参照
 プロジェクト出力参照プロパティでは、プロジェクト項目の実行に必要な依存関係 (アセンブリなど) を指定します。 たとえば、ソリューションに BDC プロジェクトとクラス プロジェクトがあるとします。 BDC プロジェクトに、クラス プロジェクトによって出力されるアセンブリに対する依存関係がある場合は、BDC プロジェクトのプロジェクト出力参照プロパティでアセンブリを参照できます。 BDC プロジェクトをパッケージ化すると、依存アセンブリがパッケージに含められます。

 通常、プロジェクト出力参照はアセンブリですが、場合によっては (Silverlight プロジェクトなど)、他の種類のファイルにすることもできます。

 詳細については、「[方法: プロジェクト出力参照を追加する](../sharepoint/how-to-add-a-project-output-reference.md)」を参照してください。

## <a name="safe-control-entries"></a>安全なコントロール エントリ
 SharePoint には、信頼されていないユーザーによる特定のコントロールへのアクセスを制限するため、安全なコントロール エントリと呼ばれるセキュリティ メカニズムが用意されています。 SharePoint では、設計上、信頼されていないユーザーが SharePoint サーバーに ASPX ページをアップロードして作成できます。 これらのユーザーがアンセーフ コードを ASPX ページに追加できないようにするため、SharePoint では "*安全なコントロール*" へのアクセスが制限されています。 安全なコントロールは、セキュリティで保護されるとして指定され、サイト上の任意のユーザーが使用できる ASPX コントロールと Web パーツです。 詳細については、「[手順 4: Web パーツを安全な コントロール リストに追加する](/previous-versions/office/developer/sharepoint-2007/ms581321(v=office.12))」を参照してください。

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のすべての SharePoint プロジェクト項目には、**安全** と **スクリプトに対して安全** の 2 つのブール値サブプロパティを持つ **安全なコントロール エントリ** というプロパティがあります。 安全プロパティでは、信頼されていないユーザーがコントロールにアクセスできるかどうかを指定します。 スクリプトに対して安全プロパティでは、信頼されていないユーザーがコントロールのプロパティを表示および変更できるかどうかを指定します。

 安全なコントロール エントリは、アセンブリごとに参照されます。 プロジェクトのアセンブリに安全なコントロール エントリを追加するには、プロジェクト項目の **安全なコントロール エントリ** プロパティにそれらを入力します。 ただし、パッケージにアセンブリを追加するときに、**パッケージ デザイナー** の **[詳細設定]** タブでプロジェクトのアセンブリに安全なコントロール エントリを追加することもできます。 詳細については、「[方法: コントロールを安全なコントロールとしてマークする](../sharepoint/how-to-mark-controls-as-safe-controls.md)」または「[Web パーツ アセンブリを安全なコントロールとして登録する](/previous-versions/office/developer/sharepoint2003/dd587360(v=office.11))」を参照してください。

### <a name="xml-entries-for-safe-controls"></a>安全なコントロールの XML エントリ
 安全なコントロール エントリをプロジェクト項目またはプロジェクトのアセンブリに追加すると、パッケージ マニフェストに次の形式で参照が書き込まれます。

```xml
<Assemblies>
    <Assembly Location="<assembly name>.dll"
      DeploymentTarget="<'GlobalAssemblyCache' or 'WebApplication'">>
        <SafeControls>
            <SafeControl Assembly="<assembly name>.dll" Namespace=
              "<SharePoint project name>" Safe="<true/false>"
                TypeName="<control name>"
                SafeAgainstScript="<true/false>" />
        </SafeControls>
    </Assembly>
</Assemblies>
```

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
- [モジュールを使用してソリューションにファイルを含める](../sharepoint/using-modules-to-include-files-in-the-solution.md)
- [SharePoint のパッケージ化と配置を拡張する](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
