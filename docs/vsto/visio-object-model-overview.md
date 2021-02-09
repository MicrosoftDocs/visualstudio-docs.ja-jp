---
title: Visio オブジェクトモデルの概要
description: Visio オブジェクトモデルを操作して Microsoft Visio 用の Office ソリューションを開発する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visio [Office development in Visual Studio], object model
- object models [Office development in Visual Studio], Office
- object models [Office development in Visual Studio], Visio
- objects [Office development in Visual Studio], Office object models
- Office object models
- Visio object model
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 8d7a83b5a900defb63ceffe4f63d57e2b200c47b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99921781"
---
# <a name="visio-object-model-overview"></a>Visio オブジェクトモデルの概要
  Visio オブジェクト モデルと対話することにより、Microsoft Office Visio 用の Office ソリューションを開発できます。 このオブジェクト モデルは、Visio のプライマリ相互運用機能アセンブリで提供されるクラスとインターフェイスで構成されています。それらは `Microsoft.Office.Interop.Visio` 名前空間の中で定義されています。

 ここでは、Visio オブジェクト モデルの概要を簡単に説明します。 Office プロジェクトでタスクを実行するために Visio オブジェクト モデルを使用する方法については、次のトピックを参照してください。

- [Visio 図面を操作する](../vsto/working-with-visio-documents.md)

- [Visio 図形を操作する](../vsto/working-with-visio-shapes.md)

## <a name="understand-the-visio-object-model"></a>Visio オブジェクトモデルについて
 Visio では、多くのオブジェクトが操作対象になります。 これらのオブジェクトは、ユーザー インターフェイスとほぼ同様の階層形式で編成されています。 階層の最上位にあるのは、 [Microsoft.Office.Interop.Visio.Application](/office/vba/api/Visio.Application) オブジェクトです。 このオブジェクトは、Visio の現在のインスタンスを表します。 オブジェクトには、 `Microsoft.Office.Interop.Visio.Application` オブジェクトとオブジェクト、およびコレクションとコレクションが含まれてい `Microsoft.Office.Interop.Visio.Document` `Microsoft.Office.Interop.Visio.Page` `Microsoft.Office.Interop.Visio.Documents` `Microsoft.Office.Interop.Visio.Pages` ます。 これらのオブジェクトとコレクションにはそれぞれ数多くのメソッドとプロパティがあり、それらにアクセスしてオブジェクトを処理したり、オブジェクトと対話したりできます。

 詳細については、 [Microsoft.Office.Interop.Visio.Application](/office/vba/api/Visio.Application)、 [Microsoft.Office.Interop.Visio.Document](/office/vba/api/Visio.Document)、および [Microsoft.Office.Interop.Visio.Page](/office/vba/api/Visio.Page) の各オブジェクト、 [Microsoft.Office.Interop.Visio.Documents](/office/vba/api/Visio.Documents) および [Microsoft.Office.Interop.Visio.Pages](/office/vba/api/Visio.Pages) の各コレクションの VBA リファレンス ドキュメントを参照してください。

 この後のセクションでは、最上位レベルのオブジェクトとそれらの相互関係について、簡単に説明します。 このようなオブジェクトには次の 4 つがあります。

- アプリケーション オブジェクト

- Document オブジェクト

- Page オブジェクト

### <a name="application-object"></a>アプリケーション オブジェクト
 Microsoft. Interop. Visio アプリケーションは Visio アプリケーションを表し、他のすべてのオブジェクトの親となります。 そのメンバーは、通常、Visio 全体に適用されます。 `Microsoft.Office.Interop.Visio.ApplicationSettings`Visio 環境を制御するには、Microsoft のアプリケーションおよびオブジェクトのプロパティとメソッドを使用します。

 VSTO アドインプロジェクトでは、 `Application` クラスのフィールドを使用することによって、アプリケーションオブジェクトにアクセスできます。 `ThisAddIn` 詳細については、「 [Programming VSTO Add-Ins](../vsto/programming-vsto-add-ins.md)」を参照してください。

### <a name="document-object"></a>Document オブジェクト
 Microsoft.Office.Interop.Visio.Document オブジェクトは、Visio をプログラミングするための中心的なオブジェクトです。 これは、図面、ステンシル、またはテンプレート ファイルを表します。 Visio 図面を開くか、新しいドキュメントを作成すると、新しい Microsoft.Office.Interop.Visio.Document オブジェクトが作成されます。このオブジェクトは、Microsoft.Office.Interop.Visio.Documents のコレクションに追加されます。

 フォーカスがある文書は、作業中のドキュメントと呼ばれます。 これは `Microsoft.Office.Interop.Visio.Application.ActiveDocument` 、Microsoft. Interop. Visio. Application オブジェクトのプロパティによって表されます。

### <a name="page-object"></a>Page オブジェクト
 Microsoft. Interop. Visio オブジェクトは、前景ページまたは背景ページの描画領域を表します。 `Microsoft.Office.Interop.Visio.Page.Background` プロパティを使用すると、ページが前景ページと背景ページのどちらであるかを判定できます。

 図形を作成するには、`Microsoft.Office.Interop.Visio.Page.DrawSpline` メソッドや `Microsoft.Office.Interop.Visio.Page.DrawOval` メソッドなどのメソッドを使用できます。 さらに、ステンシルからマスターを取得し、`Microsoft.Office.Interop.Visio.Page.Drop` メソッドまたは `Microsoft.Office.Interop.Visio.Page.DropMany` メソッドを使用することにより図形をページに配置できます。

## <a name="use-the-visio-object-model-documentation"></a>Visio オブジェクトモデルのドキュメントを使用する
 Visio オブジェクト モデルの詳細については、Visio の VBA オブジェクト モデルのリファレンスを参照してください。 VBA オブジェクト モデルのリファレンス ドキュメントでは、Visual Basic for Applications (VBA) コードに公開される Visio オブジェクト モデルについて説明しています。 詳細については、「 [Visio オブジェクトモデルのリファレンス](/office/vba/api/overview/visio/object-model)」を参照してください。

 VBA オブジェクト モデルのリファレンス内のオブジェクトとメンバーはすべて、Visio プライマリ相互運用機能アセンブリ (PIA) の型とメンバーに対応します。 たとえば、 `Document` VBA オブジェクトモデルのリファレンス内のオブジェクトは、VISIO PIA の Microsoft.Office.Interop.Visio.Document 型に対応しています。 VBA オブジェクト モデルのリファレンスでは、ほとんどのプロパティ、メソッド、およびイベントのコード例を紹介しています。ただし、Visual Studio を使用して作成した Visio VSTO アドイン プロジェクトでこのリファレンス内の VBA コードを使用するには、それらを Visual Basic または Visual C# に変換する必要があります。

> [!NOTE]
> 現在のところ、Visio プライマリ相互運用機能アセンブリに関するリファレンス ドキュメントは提供されていません。

 関連するコードサンプルと Visio ソリューションを作成するためのその他のツールについては、「 [visio 2010 software development kit](https://www.microsoft.com/download/details.aspx?id=12365)」を参照してください。

### <a name="additional-types-in-primary-interop-assemblies"></a>プライマリ相互運用機能アセンブリの追加の型
 実装の違いにより VBA には表示されないプライマリ相互運用機能アセンブリの型があります。 VBA では、直接使用できるオブジェクトとメンバーだけを含む Visio オブジェクト モデルのビューが提供されます。 プライマリ相互運用機能アセンブリは同じオブジェクト モデルを公開しますが、それには、COM オブジェクト モデルのオブジェクトをマネージド コードに変換する、その他のインターフェイス、クラス、およびメンバーも含まれています。 これらの追加の項目は、コードで直接使用するためのものではありません。

 詳細については、「 [office プライマリ相互運用機能](/previous-versions/office/office-12/ms247299(v=office.12)) アセンブリと [office プライマリ相互運用機能アセンブリ](../vsto/office-primary-interop-assemblies.md)のクラスとインターフェイスの概要」を参照してください。

## <a name="see-also"></a>関連項目
- [Visio ソリューション](../vsto/visio-solutions.md)
- [Visio 図面を操作する](../vsto/working-with-visio-documents.md)
- [Visio 図形を操作する](../vsto/working-with-visio-shapes.md)
