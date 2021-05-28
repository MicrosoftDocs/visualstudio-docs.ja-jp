---
title: 再利用可能なワークフローをインポートするためのガイドライン | Microsoft Docs
description: SharePoint Designer で作成された再利用可能なワークフローを Visual Studio にインポートするためのガイドラインについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing items
- SharePoint development in Visual Studio, reusable workflows
- importing items [SharePoint development in Visual Studio]
- reusable workflows [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: a8fbf218f032c9d580c490f91f6169681dc93cef
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876707"
---
# <a name="guidelines-for-importing-reusable-workflows"></a>再利用可能なワークフローをインポートするためのガイドライン
  SharePoint Designer で作成された再利用可能なワークフローをインポートするには、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で再利用可能な SharePoint 2010 ワークフローのインポート テンプレートを使用します。 このテンプレートを使用すると、"*宣言型* *ワークフロー*" ([!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] のみ) がインポートされて、"*コード ワークフロー*" に変換されます。これは、[!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] または [!INCLUDE[csprcs](../sharepoint/includes/csprcs-md.md)] のコードで拡張できるワークフローです。 [!INCLUDE[crdefault](../sharepoint/includes/crdefault-md.md)]、「[チュートリアル: SharePoint Designer の再利用可能なワークフローを Visual Studio にインポートする](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)」を参照してください。

 ただし、再利用可能な SharePoint 2010 ワークフローのインポート テンプレートでインポートできるのは、ファーム ソリューションだけです。 ワークフローをサンドボックス ソリューションとして配置する場合は、SharePoint 2010 ソリューション パッケージのインポート テンプレートを使用してインポートします。 ただし、この方法を使用すると、コード ワークフローに変換することはできず、そのように変更することはできません。

## <a name="import-reusable-workflows-by-using-the-import-reusable-workflow-template"></a>再利用可能なワークフローのインポート テンプレートを使用して再利用可能なワークフローをインポートする
 再利用可能な SharePoint 2010 ワークフローのインポート テンプレートを使用して再利用可能なワークフローをインポートする場合は、他の [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint ソリューションと同様にソリューションを実行または変更できますが、いくつかの項目を手動で修正することが必要になる場合があります。

### <a name="import-task-forms"></a>タスク フォームをインポートする
 再利用可能な SharePoint 2010 ワークフローのインポート プロジェクト テンプレートにより、すべての開始フォームと関連付けフォームがインポートされますが、タスク フォームは 1 つしかインポートされません。これは、コード ワークフロー スキーマで許可されるタスク フォームが 1 つだけのためです。 元のワークフロー ソリューションの他のタスク フォームは、**ソリューション エクスプローラー** の **[Other Imported Files]\(その他のインポートされたファイル\)** フォルダーに格納されます。

## <a name="import-reusable-workflows-by-using-the-import-sharepoint-2010-solution-package-template"></a>SharePoint 2010 ソリューション パッケージのインポート テンプレートを使用して再利用可能なワークフローをインポートする
 SharePoint 2010 ソリューション パッケージのインポート テンプレートを使用して再利用可能なワークフローをインポートする場合は、次の問題を考慮する必要があります。

- ワークフローをインポートした後は、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で **F5** キーを押すことにより、すぐに配置して実行できます。 ただし、インポートされたソリューションのワークフローで何かを変更した場合は、ワークフローを配置して実行する前に、プロジェクト内の要素を手動で修正することが必要になる場合があります。

- ワークフローは宣言型であるため、コードを追加することはできません。 ワークフローをコード ワークフローに変換するには、再利用可能な SharePoint 2010 ワークフローのインポート テンプレートを使用して、それを [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] にインポートする必要があります。

- デザイン ビューでワークフロー デザイナー (.xoml) ファイルを編集できますが、ワークフロー デザイナーで誤ったエラーが表示されるため、ソース ビューで編集することをお勧めします。

- ワークフローでのデバッグは、宣言型コンテンツに対しては機能しません。 [!INCLUDE[wfd2](../sharepoint/includes/wfd2-md.md)] で設定されたブレークポイントはヒットしません。

## <a name="import-globally-reusable-workflow-solutions"></a>グローバルに再利用可能なワークフロー ソリューションをインポートする
 再利用可能な SharePoint 2010 ワークフローのインポート テンプレートを使用して、グローバルに再利用可能なワークフローをインポートすることはできません。 グローバルに再利用可能なワークフローをインポートするには、グローバルに再利用可能ではないワークフローに変換するか、または SharePoint 2010 ソリューション パッケージのインポート テンプレートを使用する必要があります。

 ワークフローを変換するには、SharePoint デザイナーでグローバルに再利用可能なワークフローのコピーを作成します (ワークフローのショートカット メニューを開き、 **[コピーとして保存]** を選択します)。 次に、再利用可能な SharePoint 2010 ワークフローのインポート テンプレートを使用して、新しい再利用可能なワークフローを [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] にインポートします。

 グローバルに再利用可能なワークフローを変更せずにインポートするには、SharePoint 2010 ソリューション パッケージのインポート テンプレートを使用します。 この方法を使用すると、ワークフローはコード ワークフローに変換されず、宣言型ワークフローのままになります。

## <a name="see-also"></a>こちらもご覧ください
- [既存の SharePoint サイトからのアイテムのインポート](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [チュートリアル: SharePoint Designer の再利用可能なワークフローを Visual Studio にインポートする](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)
