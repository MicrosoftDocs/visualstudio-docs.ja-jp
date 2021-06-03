---
title: SharePoint プロジェクトの拡張 | Microsoft Docs
description: SharePoint プロジェクトのプロジェクトレベルの機能をカスタマイズする場合に、プロジェクトの拡張機能を作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], extending
- SharePoint development in Visual Studio, extending projects
- SharePoint projects, extending
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 8efeb704bb247e653af0ee062efcc71ad390c5ea
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99948662"
---
# <a name="extend-sharepoint-projects"></a>SharePoint プロジェクトを拡張する
  SharePoint プロジェクトのプロジェクトレベルの機能をカスタマイズする場合は、プロジェクトの拡張機能を作成します。 たとえば、カスタム プロジェクトのプロパティを追加したり、ユーザーが Visual Studio で SharePoint ソリューションを開発するときに発生するプロジェクトレベルのイベントに応答したりできます。

## <a name="create-project-extensions"></a>プロジェクトの拡張機能を作成する
 プロジェクト項目を拡張するには、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> インターフェイスを実装する Visual Studio 拡張機能アセンブリをビルドします。 詳細については、「[方法: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-extension.md)」を参照してください。

 プロジェクトの拡張機能を作成する場合は、SharePoint プロジェクトに次の機能を追加することもできます。

- ショートカット メニュー項目を追加します。 メニュー項目は、**ソリューション エクスプローラー** で SharePoint プロジェクト ノードのショートカット メニューを開いたときに表示されます。そのためには、ノードを右クリックするか、選択してから **Shift**+**F10** キーを押します。 詳細については、「[方法: SharePoint プロジェクトにショートカット メニュー項目を追加する](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)」を参照してください。

- カスタム プロパティを追加します。 プロパティは、**ソリューション エクスプローラー** で SharePoint プロジェクトが選択されたときに、 **[プロパティ]** ウィンドウに表示されます。 詳細については、「[方法: SharePoint プロジェクトにプロパティを追加する](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)」を参照してください。

  プロジェクトの拡張機能を作成、配置、およびテストする方法を示すチュートリアルについては、「[チュートリアル: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)」を参照してください。

## <a name="understand-the-relationship-between-project-extensions-and-project-instances"></a>プロジェクトの拡張機能とプロジェクト インスタンスの関係を理解する
 プロジェクト拡張機能を作成すると、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で任意の種類の SharePoint プロジェクトが開かれたときに、拡張機能が読み込まれます。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] には、リスト定義、コンテンツ タイプ、イベント レシーバーなど、いくつかの SharePoint プロジェクト テンプレートが含まれています。 ただし、SharePoint プロジェクトの種類は 1 つだけです。 **[新しいプロジェクト]** ダイアログ ボックスに表示されるプロジェクトの種類は、1 つ以上の SharePoint プロジェクト項目をバンドルするテンプレートにすぎません。 SharePoint プロジェクトの種類は 1 つだけなので、1 つのプロジェクトに対して作成された拡張機能は、すべての SharePoint プロジェクトに適用されます。 たとえば、"**コンテンツ タイプ**" プロジェクトにのみ適用される拡張機能を作成することはできません。

 特定のプロジェクト インスタンスにアクセスするには、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> メソッドの実装で、*projectService* パラメーターの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents> イベントの 1 つを処理します。 たとえば、SharePoint プロジェクトがソリューションに追加されたことを確認するには、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectAdded> イベントを処理します。 詳細については、「[方法: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-extension.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [方法: ショートカット メニュー項目を SharePoint プロジェクトに追加する](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)
- [方法: SharePoint プロジェクトにプロパティを追加する](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [チュートリアル: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)
- [カスタムの SharePoint プロジェクト項目の種類を定義する](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [SharePoint プロジェクト項目を拡張する](../sharepoint/extending-sharepoint-project-items.md)
- [SharePoint のパッケージ化と配置を拡張する](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)
