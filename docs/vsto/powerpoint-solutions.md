---
title: PowerPoint ソリューション
description: Visual Studio から、Microsoft PowerPoint 用の VSTO アドインを作成するために使用できるプロジェクト テンプレートが提供されていることを説明します。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office solutions [Office development in Visual Studio], PowerPoint
- templates [Office development in Visual Studio], PowerPoint
- solutions [Office development in Visual Studio], PowerPoint
- projects [Office development in Visual Studio], PowerPoint
- PowerPoint [Office development in Visual Studio]
- Office projects [Office development in Visual Studio], PowerPoint
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4033c3fbae9aaefdc094d94d3a4ba70b67d40bf5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99891905"
---
# <a name="powerpoint-solutions"></a>PowerPoint ソリューション
  Visual Studio には、Microsoft Office PowerPoint の VSTO アドインを作成するために使用できるプロジェクト テンプレートが用意されています。 VSTO アドインを使用すると、PowerPoint の自動化、PowerPoint 機能の拡張、PowerPoint ユーザー インターフェイス (UI) のカスタマイズが可能です。

 VSTO アドインの詳細については、「[VSTO アドインのプログラミングの概要](getting-started-programming-vsto-add-ins.md)」と「[VSTO アドインのアーキテクチャ](architecture-of-vsto-add-ins.md)」を参照してください。Microsoft Office を使用したプログラミングを初めて行う場合は、[はじめに &#40;Visual Studio での Office 開発&#41;](getting-started-office-development-in-visual-studio.md) に関するページを参照してください。

 [!INCLUDE[appliesto_pptallapp](includes/appliesto-pptallapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="automate-powerpoint-by-using-the-powerpoint-object-model"></a>PowerPoint のオブジェクト モデルを使用して PowerPoint を自動化する
 PowerPoint オブジェクト モデルでは、PowerPoint の自動化に使用できる型が多数公開されています。 それらの型によって、次のような一般的なタスクを実行するコードを作成できます。

- プログラムによるプレゼンテーションの作成と書式指定

- プレゼンテーションへのスライドの追加または削除

- スライドへの図形の追加または変更

  VSTO アドインから PowerPoint オブジェクト モデルにアクセスするには、プロジェクトの `ThisAddIn` クラスの `Application` フィールドを使用します。 `Application` フィールドからは、PowerPoint の現在のインスタンスを表す [Application](/previous-versions/office/developer/office-2010/ff764034(v=office.14)) オブジェクトが返されます。 詳細については、「[VSTO アドインのプログラミング](programming-vsto-add-ins.md)」を参照してください。

  PowerPoint オブジェクト モデルを呼び出すときには、PowerPoint のプライマリ相互運用機能アセンブリに用意された型を使用します。 プライマリ相互運用機能アセンブリは、VSTO アドインのマネージド コードと PowerPoint の COM オブジェクト モデルとの仲介役を果たします。 PowerPoint のプライマリ相互運用機能アセンブリ内の型はすべて、[Microsoft.Office.Interop.PowerPoint](/previous-versions/office/developer/office-2010/ff763170(v=office.14)) 名前空間で定義されています。 プライマリ相互運用機能アセンブリの詳細については、「[Office ソリューションの開発の概要 &#40;VSTO&#41;](office-solutions-development-overview-vsto.md)」および「[Office プライマリ相互運用機能アセンブリ](office-primary-interop-assemblies.md)」を参照してください。

## <a name="use-the-powerpoint-object-model-documentation"></a><a name="WordOMDocumentation"></a> PowerPoint オブジェクト モデルのドキュメントを使用する
 PowerPoint オブジェクト モデルの詳細については、PowerPoint プライマリ相互運用機能アセンブリ (PIA) のリファレンスと、VBA オブジェクト モデルのリファレンスを参照してください。

### <a name="primary-interop-assembly-reference"></a>プライマリ相互運用機能アセンブリのリファレンス
 PowerPoint PIA のリファレンス ドキュメントは、PowerPoint のプライマリ相互運用機能アセンブリの型について説明しています。 このドキュメントは、[PowerPoint 2010 プライマリ相互運用機能アセンブリのリファレンス](office-primary-interop-assemblies.md)に関する記事から利用できます。

 PIA のクラスとインターフェイスの違い、PIA のイベントの実装方法など、PowerPoint PIA の設計の詳細については、[Office プライマリ相互運用機能アセンブリのクラスとインターフェイスの概要](/previous-versions/office/developer/office-2010/ff759900(v=office.14))に関する記事を参照してください。

### <a name="vba-object-model-reference"></a>VBA オブジェクト モデルのリファレンス
 VBA オブジェクト モデルのリファレンスでは、Visual Basic for Applications (VBA) コードに公開される PowerPoint オブジェクト モデルについて説明しています。 詳細については、[PowerPoint 2010 オブジェクト モデルのリファレンス](/office/vba/api/overview/PowerPoint/object-model)に関する記事を参照してください。

 VBA オブジェクト モデルのリファレンス内のオブジェクトとメンバーはすべて、PowerPoint プライマリ相互運用機能アセンブリ (PIA) の型とメンバーに対応します。 たとえば、VBA オブジェクト モデルのリファレンスの Presentation オブジェクトは、PowerPoint PIA の [Presentation](/previous-versions/office/developer/office-2010/ff761925(v=office.14)) 型に対応します。 VBA オブジェクト モデルのリファレンスでは、ほとんどのプロパティ、メソッド、およびイベントのコード例を紹介しています。ただし、Visual Studio を使用して作成した PowerPoint VSTO アドイン プロジェクトでこのリファレンス内の VBA コードを使用するには、それらを Visual Basic または Visual C# に変換する必要があります。

## <a name="customize-the-user-interface-of-powerpoint"></a>PowerPoint のユーザー インターフェイスをカスタマイズする
 PowerPoint の UI を次のように変更できます。

|タスク|詳細情報|
|----------|--------------------------|
|カスタム作業ウィンドウを作成する。|[カスタム作業ウィンドウ](custom-task-panes.md)|
|リボンにカスタム タブを追加する。|[リボンの概要](ribbon-overview.md)|
|リボン上の組み込みタブにカスタム グループを追加する。|[方法: 組み込みタブをカスタマイズする](how-to-customize-a-built-in-tab.md)|

 PowerPoint およびその他の Microsoft Office アプリケーションの UI をカスタマイズする方法の詳細については、「[Office UI のカスタマイズ](office-ui-customization.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [チュートリアル: 初めての PowerPoint 用 VSTO アドインを作成する](walkthrough-creating-your-first-vsto-add-in-for-powerpoint.md)
- [VSTO アドインのプログラミングの概要](getting-started-programming-vsto-add-ins.md)
- [Office ソリューションの開発の概要 &#40;VSTO&#41;](office-solutions-development-overview-vsto.md)
- [Architecture of VSTO Add-Ins](architecture-of-vsto-add-ins.md)
- [方法: Visual Studio で Office プロジェクトを作成する](how-to-create-office-projects-in-visual-studio.md)
- [VSTO アドインのプログラミング](programming-vsto-add-ins.md)
- [Office ソリューションでコードを書く](writing-code-in-office-solutions.md)
- [Office プライマリ相互運用機能アセンブリ](office-primary-interop-assemblies.md)
- [Office UI のカスタマイズ](office-ui-customization.md)
- [Office 開発における PowerPoint 2010](/previous-versions/office/developer/office-2010/ff604967(v=office.14))
