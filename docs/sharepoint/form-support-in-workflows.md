---
title: ワークフローでのフォームのサポート | Microsoft Docs
description: SharePoint ワークフローでのフォームのサポートについて説明します。 ワークフローでは、関連付け、開始、タスク、変更の 4 種類のフォームを使用できます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- workflows [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: adf5de014c7921130bd6f3ecd3cf8c5bb5daa92a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876681"
---
# <a name="form-support-in-workflows"></a>ワークフローでのフォームのサポート
  ワークフローでは、関連付け、開始、タスク、変更の 4 種類のフォームを使用できます。 これらのフォームの種類は、ASPX フォームまたは InfoPath フォームのいずれかに基づいています。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で特定のフォームに対して提供されるサポートのレベルは、次の表で説明する複数の要因によって決まります。 ワークフロー フォームの種類の詳細については、「[ワークフロー フォームの種類](/previous-versions/office/developer/sharepoint-2010/ms457061(v=office.14))」を参照してください。

## <a name="xml-refactoring"></a>XML リファクタリング
 ASPX 関連付けまたは開始フォームを [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のワークフロー プロジェクト項目に追加すると、フォーム名または配置パスが更新されるか、フォームが削除されるたびに、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によってワークフローの *Elements.xml* ファイル内の XML が自動的にリファクタリングされ、関連付けまたは開始フォームを参照する属性の同期が保持されます。 しかし、タスクまたは変更フォームなどの他のフォームの種類をワークフローで使用しても、*Elements.xml* ファイルはリファクタリングされません。

## <a name="form-support-in-new-visual-studio-workflows"></a>新しい Visual Studio ワークフローでのフォームのサポート
 次の表に、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で作成されるワークフロー内の ASPX または InfoPath フォームに基づくさまざまなフォームの種類に対する [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のサポートを示します。

|フォームの種類|Visual Studio で ASPX フォームを使用して作成されたワークフロー|Visual Studio で InfoPath フォームを使用して作成されたワークフロー|
|---------------|---------------------------------------------------------|-----------------------------------------------------------------|
|関連付け|- **ワークフロー関連付けフォーム** 項目テンプレートを使用して ASPX 関連付けフォームをワークフローに追加できます。<br />- フォームが追加、名前変更、削除されたとき、またはその配置パスが変更されたときに、ワークフローの *Elements.xml* ファイルがリファクタリングされます。<br />- 詳細については、「[チュートリアル: 関連付けフォームと開始フォームを持つワークフローの作成](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)」を参照してください。|- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] には InfoPath 関連付けフォーム テンプレートはありません。<br />- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] と InfoPath デザイナーは統合されていません。<br />- ワークフローの *Elements.xml* ファイルはリファクタリングされません。|
|開始|- **ワークフロー開始フォーム** 項目テンプレートを使用して ASPX 開始フォームをワークフローに追加できます。<br />- フォームが追加、名前変更、削除されたとき、またはその配置パスが変更されたときに、ワークフローの *Elements.xml* ファイルがリファクタリングされます。<br />- 詳細については、「[チュートリアル: 関連付けフォームと開始フォームを持つワークフローの作成](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)」を参照してください。|- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] には InfoPath 関連付けフォーム テンプレートはありません。<br />- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] と InfoPath デザイナーは統合されていません。<br />- ワークフローの *Elements.xml* ファイルはリファクタリングされません。|
|タスク|- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で使用できる ASPX タスク フォームテンプレートはありません。 アプリケーション ページを作成し、それにコードを追加する必要があります。<br />- ワークフローの *Elements.xml* ファイルはリファクタリングされません。<br />- 詳細については、「[ワークフローのタスク フォーム (SharePoint Foundation)](/previous-versions/office/developer/sharepoint-2010/ms438856(v=office.14))」を参照してください|- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] には InfoPath タスク フォーム テンプレートはありません。<br />- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] と InfoPath デザイナーは統合されていません。<br />- ワークフローの *Elements.xml* ファイルはリファクタリングされません。|
|変更|- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で使用できる ASPX 変更フォーム テンプレートはありません。 変更フォームを追加するには、アプリケーション ページを作成し、それにコードを追加する必要があります。<br />- ワークフローの *Elements.xml* ファイルはリファクタリングされません。 必要に応じて手動で編集する必要があります。<br />- 詳細については、「[ワークフロー変更フォーム (SharePoint Foundation)](/previous-versions/office/developer/sharepoint-2010/ms480794(v=office.14))」を参照してください|- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] には InfoPath 変更フォーム テンプレートはありません。<br />- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] と InfoPath デザイナーは統合されていません。<br />- ワークフローの *Elements.xml* ファイルはリファクタリングされません。|

## <a name="form-support-in-imported-sharepoint-reusable-workflows"></a>インポートされた SharePoint の再利用可能なワークフローでのフォームのサポート
 次の表に、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] にインポートされる SharePoint の再利用可能なワークフロー内の ASPX または InfoPath フォームに基づくさまざまなフォームの種類に対する [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のサポートを示します。

|フォームの種類|SharePoint Designer からインポートされた ASPX フォームを持つ再利用可能なワークフロー|SharePoint Designer からインポートされた InfoPath フォームを持つ再利用可能なワークフロー|
|---------------|-------------------------------------------------------------------------------| - |
|関連付け|- フォームは、ワークフローの *Elements.xml* ファイルで参照されます。<br />- フォームが名前変更または削除されたとき、あるいはその配置パスが変更されたときに、ワークフローの *Elements.xml* ファイルがリファクタリングされます。|- フォームはインポートされますが、ワークフローの *Elements.xml* ファイルでは参照されません。<br />- ワークフローの *Elements.xml* ファイルはリファクタリングされません。|
|開始|- フォームは、ワークフローの *Elements.xml* ファイル内のワークフローによって参照されます。<br />- フォームが名前変更または削除されたとき、あるいはその配置パスが変更されたときに、ワークフローの *Elements.xml* ファイルがリファクタリングされます。|- フォームはインポートされますが、ワークフローの *Elements.xml* ファイルでは参照されません。<br />- ワークフローの *Elements.xml* ファイルはリファクタリングされません。 **注:** このシナリオが機能するように、ルールとプロパティを追加して変更する必要があります。|
|タスク|- フォームは、ワークフローの *Elements.xml* ファイルで参照されます。<br />- ワークフローの *Elements.xml* ファイルはリファクタリングされません。|- フォームはインポートされますが、ワークフローの *Elements.xml* ファイルでは参照されません。<br />- ワークフローの *Elements.xml* ファイルはリファクタリングされません。 **注:** このシナリオが機能するように、ルールとプロパティを追加して変更する必要があります。|
|変更|適用不可。 SharePoint Designer では ASPX 変更フォームを作成できません。|適用不可。 SharePoint Designer では InfoPath 変更フォームを作成できません (ワークフローをエクスポートするときに .wsp ファイルに含まれていない組み込みの SharePoint Server ワークフローを除く)。|

## <a name="see-also"></a>関連項目
- [チュートリアル: 関連付けフォームと開始フォームを持つワークフローの作成](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)
- [SharePoint ワークフロー ソリューションの作成](../sharepoint/creating-sharepoint-workflow-solutions.md)
- [既存の SharePoint サイトからの項目のインポート](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
