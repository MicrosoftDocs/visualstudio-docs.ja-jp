---
title: カスタムの SharePoint プロジェクト項目の種類の定義 | Microsoft Docs
description: 新しい種類の SharePoint プロジェクト項目を作成する場合には、カスタムの SharePoint プロジェクト項目の種類を定義します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 00ee9f41695078d8bea5daacf1c0ccfd392a64cc
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99948870"
---
# <a name="define-custom-sharepoint-project-item-types"></a>カスタムの SharePoint プロジェクト項目の種類を定義する
  新しい種類の SharePoint プロジェクト項目を作成する場合には、新しい SharePoint プロジェクト項目の種類を定義します。 たとえば、Visual Studio には、フィールドやカスタム アクションを SharePoint サイトに追加するための SharePoint プロジェクト項目は含まれていません。 フィールド、カスタム アクション、またはその他の種類の SharePoint コンポーネントを作成する場合は、独自の種類の SharePoint プロジェクト項目を定義することができます。

## <a name="tasks-for-defining-sharepoint-project-item-types"></a>SharePoint プロジェクト項目の種類を定義するためのタスク
 カスタムのプロジェクト項目の種類を定義するには、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> インターフェイスを実装する Visual Studio 拡張機能アセンブリをビルドします。 詳細については、「[方法: SharePoint プロジェクト項目の種類を定義する](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)」を参照してください。

 カスタムのプロジェクト項目の種類を定義する場合は、プロジェクト項目に次の機能を追加することもできます。

- ショートカット メニュー項目をプロジェクト項目に追加します。 メニュー項目は、**ソリューション エクスプローラー** でプロジェクト項目のショートカット メニューを開いたときに表示されます。そのためには、プロジェクト項目を右クリックするか、選択してから **Shift**+**F10** キーを押します。 [ショートカット メニュー項目をカスタムの SharePoint プロジェクト項目の種類に追加する方法](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)に関するページを参照してください。

- カスタム プロパティをプロジェクト項目に追加します。 プロパティは、**ソリューション エクスプローラー** でプロジェクト項目が選択されたときに、 **[プロパティ]** ウィンドウに表示されます。 詳細については、「[方法: カスタムの SharePoint プロジェクト項目の種類にプロパティを追加する](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)」を参照してください。

  他の開発者が Visual Studio でプロジェクト項目を使用できるようにするには、.spdata ファイルを作成し、プロジェクト項目に関連付けられている項目テンプレートまたはプロジェクト テンプレートを作成します。 詳細については、[SharePoint プロジェクト項目の項目テンプレートとプロジェクト テンプレートの作成](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)に関するページを参照してください。

## <a name="understand-the-relationship-between-project-item-types-and-project-item-instances"></a>プロジェクト項目の種類とプロジェクト項目のインスタンスの関係を理解する
 SharePoint プロジェクト項目の種類を定義すると、関連付けられている種類のプロジェクト項目が SharePoint プロジェクトに追加されたときに、Visual Studio によって拡張機能が読み込まれます。 たとえば、新しい "**カスタム アクション**" プロジェクト項目の種類を定義すると、ユーザーがプロジェクトに "**カスタム アクション**" プロジェクト項目を追加したときに、Visual Studio によって拡張機能が読み込まれます。 Visual Studio では、関連付けられているプロジェクト項目の種類のすべてのインスタンスに対して、拡張機能の同じインスタンスが使用されます。 前の例では、ユーザーが 2 つ目の "**カスタム アクション**" プロジェクト項目をプロジェクトに追加した場合は、2 つ目のプロジェクト項目をカスタマイズするために、拡張機能の同じインスタンスが使用されます。

 プロジェクト項目の種類の特定のインスタンスにアクセスするには、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> メソッドの実装で *projectItemTypeDefinition* パラメーターの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> イベントの 1 つを処理します。 たとえば、カスタムの種類のプロジェクト項目がいつプロジェクトに追加されたかを確認するには、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> イベントを処理します。 詳細については、「[方法: SharePoint プロジェクト項目の種類を定義する](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: SharePoint プロジェクト項目の種類を定義する](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)
- [方法: プロパティをカスタムの SharePoint プロジェクト項目の種類に追加する](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
- [方法: ショートカット メニュー項目をカスタム SharePoint プロジェクト項目の種類に追加する](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)
- [SharePoint プロジェクト項目の項目テンプレートとプロジェクト テンプレートを作成する](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [チュートリアル: プロジェクト テンプレートを使ってサイト列プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [チュートリアル: 項目テンプレートを使ってカスタム アクション プロジェクト項目を作成する (パート 2)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)
- [チュートリアル: プロジェクト テンプレートを使用してサイト列プロジェクト項目を作成する (パート 2)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)
- [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)
