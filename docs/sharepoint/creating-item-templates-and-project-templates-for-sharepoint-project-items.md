---
title: SharePoint プロジェクト項目の項目テンプレート/プロジェクト テンプレート
description: SharePoint プロジェクト項目の項目テンプレートとプロジェクト テンプレートを作成します。 項目テンプレートとプロジェクト テンプレートのウィザードを作成します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, creating custom templates
- .spdata files
- projects [SharePoint development in Visual Studio], creating custom templates
- SharePoint projects, creating custom templates
- SharePoint development in Visual Studio, creating custom project and item templates
- project items [SharePoint development in Visual Studio], creating custom templates
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 538bc709ed3af1c7b1424b56c1bd843b127c6ab7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99949156"
---
# <a name="create-item-templates-and-project-templates-for-sharepoint-project-items"></a>SharePoint プロジェクト項目の項目テンプレートとプロジェクト テンプレートを作成する

カスタムの SharePoint プロジェクト項目の種類を定義すると、それを項目テンプレートまたはプロジェクト テンプレートに関連付けることができます。 この関連付けにより、他の開発者が Visual Studio でプロジェクト項目を使用できるようになります。 テンプレートのウィザードを作成することもできます。

たとえば、Visual Studio には、SharePoint サイトにフィールドを追加するためのプロジェクト テンプレートまたは項目テンプレートは含まれていません。 フィールドを表す SharePoint プロジェクト項目の種類を定義してから、他の開発者がフィールド項目を SharePoint プロジェクトに追加するために使用できる項目テンプレートを構築することができます。 または、プロジェクト テンプレートを構築して、開発者がフィールド項目を含む新しい SharePoint プロジェクトを作成できるようにすることもできます。 どちらの場合も、開発者がテンプレートを使用するときに表示されるウィザードを提供できます。 このウィザードでは、新しい項目やプロジェクトを構成するために開発者からの情報を収集することができます。

項目テンプレートとプロジェクト テンプレートは、プロジェクト項目またはプロジェクトを作成するために Visual Studio で使用されるファイルが含まれている *.zip* ファイルです。 項目テンプレートとプロジェクト テンプレートの基礎の詳細については、「[プロジェクトと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)」を参照してください。

## <a name="create-item-templates"></a>項目テンプレートを作成する
 SharePoint プロジェクト項目の項目テンプレートを作成する場合は、常に必要なファイルと、特定の種類のプロジェクト項目で使用される可能性がある省略可能なファイルがあります。 SharePoint プロジェクト項目の種類を定義し、その項目テンプレートを作成する方法を示すチュートリアルについては、「[チュートリアル: 項目テンプレートを使ってカスタム アクション プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)」を参照してください。

 次の表に、SharePoint プロジェクト項目の項目テンプレートを作成するために必要なファイルを示します。

|必要なファイル|説明|
|-------------------|-----------------|
|*.spdata* ファイル|この XML ファイルには、プロジェクト項目の内容と既定の動作が指定されています。 このファイルは、項目テンプレートに含める必要があります。 *.spdata* ファイルの内容の詳細については、[SharePoint プロジェクト項目スキーマのリファレンス](../sharepoint/sharepoint-project-item-schema-reference.md)に関するページを参照してください。|
|*.vstemplate* ファイル。|このファイルは、 **[新しい項目の追加]** ダイアログ ボックスにテンプレートを表示したり、テンプレートからプロジェクト項目を作成したりするために必要な情報を Visual Studio に提供します。 このファイルは、項目テンプレートに含める必要があります。 詳細については、[Visual Studio テンプレートのメタデータ ファイル](/previous-versions/visualstudio/visual-studio-2010/xsxc3ete\(v\=vs.100\))に関するページを参照してください。|
|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> インターフェイスを実装する Visual Studio 拡張機能アセンブリ。|このアセンブリは、プロジェクト項目の実行時の動作を定義します。 このアセンブリは、項目テンプレートと共に VSIX パッケージに含める必要があります。 詳細については、「[カスタム SharePoint プロジェクト項目の種類を定義する](../sharepoint/defining-custom-sharepoint-project-item-types.md)」および「[Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。|

 次の表に、項目テンプレートに含めることができる最も一般的な省略可能ファイルを示します。 一部の種類のプロジェクト項目には、ここに記載されていない他のファイルが必要な場合があります。

| 省略可能なファイル | 説明 |
|----------------------| - |
| *Elements.xml* | "*Feature 要素*" ファイル。 このファイルには、プロジェクト項目によって作成されたカスタマイズの UI と動作が定義されています。 リスト インスタンス、コンテンツ タイプ、カスタム アクションなどのそれぞれの種類のカスタマイズには、このファイルの内容を定義する別のスキーマがあります。 詳細については、「[構成要素: フィーチャー](/previous-versions/office/developer/sharepoint-2010/ee537350(v=office.14))」および「[Feature スキーマ](/previous-versions/office/developer/sharepoint-2010/ms414322(v=office.14))」を参照してください。 |
| *Schema.xml* | リスト定義のスキーマ ファイル。 詳細については、「[構成要素: リストとドキュメント ライブラリ](/previous-versions/office/developer/sharepoint-2010/ee534985(v=office.14))」および [Schema.xml](/previous-versions/office/developer/sharepoint-2010/ms459356(v=office.14)) に関するページを参照してください。 |
| *.webpart* | "*Web パーツ定義*" ファイル。 このファイルには、Web パーツのプロパティ設定が含まれています。 詳細については、「[構成要素: Web パーツ](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))」を参照してください。 |
| *.ascx* | ASP.NET UserControl ファイル。 このファイルには、視覚的 Web パーツの UI が定義されています。 |
| *.aspx* | ASP.NET ページ ファイル。 このファイルには、アプリケーション ページを定義する XML マークアップが含まれています。 |
| *.cs* または *.vb* ファイル | これらのコード ファイルには、アプリケーション ページ、Web パーツ、ワークフローなど、Visual C# または Visual Basic コードからアクセスできるプログラミング モデルを含む SharePoint カスタマイズの動作が定義されています。 |

## <a name="create-project-templates"></a>プロジェクト テンプレートを作成する
 SharePoint プロジェクト テンプレートを作成する場合は、常に必要なファイルと、特定の種類のプロジェクトで使用される可能性がある省略可能なファイルがあります。 通常、SharePoint プロジェクトには、SharePoint プロジェクト項目が少なくとも 1 つ含まれています。 ただし、これは必須ではありません。 たとえば、他のプロジェクトで作成された SharePoint ソリューションを配置するためにのみ使用することを目的とした SharePoint プロジェクト テンプレートを定義できます。

 SharePoint プロジェクト項目の種類を定義し、そのプロジェクト テンプレートを作成する方法を示すチュートリアルについては、「[チュートリアル: プロジェクト テンプレートを使ってサイト列プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)」を参照してください。

 次の表に、SharePoint プロジェクト テンプレートに含める必要があるファイルを示します。

|必要なファイル|説明|
|-------------------|-----------------|
|*.vstemplate* ファイル|このファイルは、 **[新しいプロジェクト]** ダイアログ ボックスにテンプレートを表示したり、テンプレートからプロジェクトを作成したりするために必要な情報を Visual Studio に提供します。 詳細については、[Visual Studio テンプレートのメタデータ ファイル](/previous-versions/visualstudio/visual-studio-2010/xsxc3ete\(v\=vs.100\))に関するページを参照してください。|
|*.csproj* または *.vbproj* ファイル|これはプロジェクト ファイルです。 これには、プロジェクトの内容と構成設定が定義されています。|
|*Package.package*|このファイルには、プロジェクトの配置パッケージが定義されています。 パッケージ デザイナーを使用してプロジェクトのソリューション パッケージをカスタマイズすると、Visual Studio によりソリューション パッケージに関するデータがこのファイルに格納されます。<br /><br /> カスタムの SharePoint プロジェクト テンプレートを作成するときは、最低限必要なコンテンツのみを *Package.package* ファイルに含めることと、プロジェクト テンプレートに関連付けられている拡張機能で、<xref:Microsoft.VisualStudio.SharePoint.Packages> 名前空間の API を使用してソリューション パッケージを構成することをお勧めします。 この場合、プロジェクト テンプレートは、*Package.package* ファイルの構造に対する将来の変更から保護されます。 最低限必要なコンテンツのみを含む *Package.package* ファイルを作成する方法を示す例については、「[チュートリアル: プロジェクト テンプレートを使ってサイト列プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)」を参照してください。<br /><br /> *Package.package* ファイルを直接変更する場合は、 *%Program Files (x86)%\Microsoft Visual Studio 11.0\Xml\Schemas\PackageModelSchema.xsd* にあるスキーマを使用して内容を確認できます。|
|*Package.Template.xml*|このファイルは、プロジェクトから生成される SharePoint ソリューション パッケージ ( *.wsp*) のソリューション マニフェスト ファイル (*manifest.xml*) の基礎となります。 プロジェクトの種類のユーザーによる変更を意図していない動作を指定する場合は、このファイルにコンテンツを追加できます。 詳細については、「[構成要素: ソリューション](/previous-versions/office/developer/sharepoint-2010/ee537008(v=office.14))」および[ソリューションのスキーマ](/sharepoint/dev/schema/solution-schema)に関するページを参照してください。<br /><br /> プロジェクトからソリューション パッケージをビルドすると、Visual Studio により、*Package.package* および *Package.Template.xml* ファイルの内容がソリューション マニフェスト ファイルにマージされます。 ソリューション パッケージのビルドの詳細については、「[方法: MSBuild タスクを使用して SharePoint ソリューション パッケージを作成する](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)」を参照してください。|

 次の表に、プロジェクト テンプレートに含めることができる省略可能なファイルを示します。

|省略可能なファイル|説明|
|-------------------|-----------------|
|SharePoint プロジェクト項目|SharePoint プロジェクト項目の種類を定義する 1 つ以上の .spdata ファイルを含めることができます。 各 *.spdata* ファイルには、プロジェクト テンプレートと共に VSIX パッケージに含まれている拡張機能アセンブリに対応する <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 実装が必要です。 詳細については、「[項目テンプレートを作成する](#create-item-templates)」を参照してください。<br /><br /> 通常、SharePoint プロジェクトには、SharePoint プロジェクト項目が少なくとも 1 つ含まれています。 ただし、これは必須ではありません。|
|*\<featureName>.feature*|このファイルには、配置のために複数のプロジェクト項目をグループ化するために使用される SharePoint フィーチャーが定義されています。 フィーチャー デザイナーを使用してプロジェクトのフィーチャーをカスタマイズすると、Visual Studio により、そのフィーチャーに関するデータがこのファイルに格納されます。 プロジェクト項目を異なるフィーチャーにグループ化する場合は、複数の *.feature* ファイルを含めることができます。<br /><br /> カスタムの SharePoint プロジェクト テンプレートを作成するときは、最低限必要なコンテンツのみを *.feature* ファイルに含めることと、プロジェクト テンプレートに関連付けられている拡張機能で、<xref:Microsoft.VisualStudio.SharePoint.Features> 名前空間の API を使用してフィーチャーを構成することをお勧めします。 この場合、プロジェクト テンプレートは、 *.feature* ファイルの構造に対する将来の変更から保護されます。 最低限必要なコンテンツのみを含む *.feature* ファイルを作成する方法を示す例については、「[チュートリアル: プロジェクト テンプレートを使ってサイト列プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)」を参照してください。<br /><br /> *.feature* ファイルを直接変更する場合は、 *%Program Files (x86)%\Microsoft Visual Studio 11.0\Xml\Schemas\FeatureModelSchema.xsd* にあるスキーマを使用して内容を確認できます。|
|*\<featureName>.Template.xml*|このファイルは、プロジェクトから生成された各フィーチャーのフィーチャー マニフェスト ファイル (*Feature.xml*) の基礎となります。 プロジェクトの種類のユーザーによる変更を意図していない動作を指定する場合は、このファイルにコンテンツを追加できます。 詳細については、「[構成要素: フィーチャー](/previous-versions/office/developer/sharepoint-2010/ee537350(v=office.14))」および [Feature.xml ファイル](/sharepoint/dev/schema/feature-xml-files)に関するページを参照してください。<br /><br /> プロジェクトからソリューション パッケージをビルドすると、Visual Studio により、 *\<featureName>.feature* ファイルと *\<featureName>.Template.xml* ファイルの各ペアの内容がフィーチャー マニフェスト ファイルにマージされます。 ソリューション パッケージのビルドの詳細については、「[方法: MSBuild タスクを使用して SharePoint ソリューション パッケージを作成する](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)」を参照してください。|

## <a name="create-wizards-for-item-templates-and-project-templates"></a>項目テンプレートとプロジェクト テンプレートのウィザードを作成する
 SharePoint プロジェクト項目の種類を定義して、項目またはプロジェクト テンプレートに関連付けた後は、ウィザードを作成することもできます。 このウィザードは、開発者が項目テンプレートを使用して SharePoint プロジェクト項目をプロジェクトに追加するとき、または開発者がプロジェクト テンプレートを使用して、SharePoint プロジェクト項目が含まれている新しいプロジェクトを作成するときに表示されます。 このウィザードを使用して、開発者から情報を収集したり、新しい SharePoint プロジェクト項目を初期化したりすることができます。

 項目テンプレートとプロジェクト テンプレート用のウィザードを作成する方法を示すチュートリアルについては、「[チュートリアル: 項目テンプレートを使ってカスタム アクション プロジェクト項目を作成する (パート 2)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)」および「[チュートリアル: プロジェクト テンプレートを使ってサイト列プロジェクト項目を作成する (パート 2)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [カスタムの SharePoint プロジェクト項目の種類を定義する](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [チュートリアル: 項目テンプレートを使ってカスタム アクション プロジェクト項目を作成する (パート 2)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)
- [チュートリアル: プロジェクト テンプレートを使ってサイト列プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [チュートリアル: プロジェクト テンプレートを使用してサイト列プロジェクト項目を作成する (パート 2)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
