---
title: Visio ソリューション
description: VSTO アドインを使用して、Visio の自動化、Visio 機能の拡張、または Visio ユーザー インターフェイス (UI) のカスタマイズを行う方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office projects [Office development in Visual Studio], Visio
- solutions [Office development in Visual Studio], Visio
- Visio [Office development in Visual Studio]
- templates [Office development in Visual Studio], Visio
- projects [Office development in Visual Studio], Visio
- Office solutions [Office development in Visual Studio], Visio
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9d888a27a8443b6500093a70416414bec453e77e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99838045"
---
# <a name="visio-solutions"></a>Visio ソリューション
  Visual Studio には、Microsoft Office Visio の VSTO アドインを作成するために使用できるプロジェクト テンプレートが用意されています。 VSTO アドインを使用して、Visio の自動化、Visio 機能の拡張、または Visio ユーザー インターフェイス (UI) のカスタマイズが可能です。

 VSTO アドインの詳細については、「[VSTO アドインのプログラミングの概要](../vsto/getting-started-programming-vsto-add-ins.md)」と「[VSTO アドインのアーキテクチャ](../vsto/architecture-of-vsto-add-ins.md)」を参照してください。Microsoft Office を使用したプログラミングを初めて行う場合は、[はじめに &#40;Visual Studio での Office 開発&#41;](../vsto/getting-started-office-development-in-visual-studio.md) に関するページを参照してください。

 **対象:** このトピックの情報は、Visio 2010 の VSTO アドインのプロジェクトに適用されます。 詳細については、「[Office アプリケーションおよびプロジェクトの種類別の使用可能な機能](../vsto/features-available-by-office-application-and-project-type.md)」を参照してください。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="automate-visio-by-using-the-visio-object-model"></a>Visio オブジェクト モデルを使用して Visio を自動化する
 Visio オブジェクト モデルでは、組織図、フローチャート、プロジェクト タイムライン、ネットワーク ダイアグラム、事務所スペースなどのダイアグラムを Visio で自動的に作成するために使用できる多数のクラスが公開されています。 この API を使用して、次のような一般的なタスクを実行するコードを作成できます。

- 図形やテキストを作成し、ダイアグラムに配置する。

- ビジネス ロジックやユーザー入力に基づいて図形の動作を管理する。

- ダイアグラムの視覚エフェクト (パン、ズームなど) を制御する。

- アプリケーション UI をカスタマイズする。

- 外部データを Visio にインポートし、図形にリンクしてページ上にグラフィカルに表示する。

  Visio のオブジェクト モデルを使用して図面および図形を操作する手順やコード例については、「[Visio 図面を操作する](../vsto/working-with-visio-documents.md)」および「[Visio 図形を操作する](../vsto/working-with-visio-shapes.md)」を参照してください。

  VSTO アドインから Visio オブジェクト モデルにアクセスするには、プロジェクト内の `Application` クラスの `ThisAddIn` フィールドを使用します。 `Application` フィールドは、Visio の現在のインスタンスを表す `Microsoft.Office.Interop.Visio.Application` オブジェクトを返します。 詳細については、「[VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)」を参照してください。

  Visio オブジェクト モデルを呼び出すときは、Visio のプライマリ相互運用機能アセンブリ (PIA) に用意された型を使用します。 PIA は、VSTO アドインのマネージド コードと Visio の COM オブジェクト モデルとの橋渡し役として機能します。 Visio PIA のすべての型は、`Microsoft.Office.Interop.Visio` 名前空間で定義されます。 プライマリ相互運用機能アセンブリの詳細については、「[Office ソリューションの開発の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)」および「[Office プライマリ相互運用機能アセンブリ](../vsto/office-primary-interop-assemblies.md)」を参照してください。

## <a name="visio-object-model-overview"></a>Visio オブジェクト モデルの概要
 Visio オブジェクト モデルの概要については、Visio オブジェクト モデルのリファレンスや SDK へのリンクを含む「[Visio オブジェクト モデルの概要](../vsto/visio-object-model-overview.md)」を参照してください。

## <a name="customize-the-user-interface-of-visio"></a>Visio のユーザー インターフェイスをカスタマイズする
 Visio の UI には、次のようなカスタマイズ オプションがあります。

|タスク|詳細情報|
|----------|--------------------------|
|リボンをカスタマイズします。|[リボンの概要](../vsto/ribbon-overview.md)|

 Visio の UI をカスタマイズする方法の詳細については、 [Visio.UIObject](/office/vba/api/Visio.UIObject) クラスの VBA リファレンス ドキュメントを参照してください。

## <a name="see-also"></a>関連項目
- [VSTO アドインのプログラミングの概要](../vsto/getting-started-programming-vsto-add-ins.md)
- [Office ソリューションの開発の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [Architecture of VSTO Add-Ins](../vsto/architecture-of-vsto-add-ins.md)
- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)
- [Office ソリューションでコードを書く](../vsto/writing-code-in-office-solutions.md)
- [Office プライマリ相互運用機能アセンブリ](../vsto/office-primary-interop-assemblies.md)
- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)
- [Visio オブジェクト モデルの概要](../vsto/visio-object-model-overview.md)
- [Office 開発における Visio 2010](/previous-versions/office/developer/office-2010/ff604964(v=office.14))
