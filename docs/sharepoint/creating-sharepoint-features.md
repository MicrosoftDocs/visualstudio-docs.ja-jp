---
title: SharePoint 機能の作成 | Microsoft Docs
description: SharePoint 機能を作成して、配置を簡単にするために関連する SharePoint プロジェクト項目をグループ化します。 SharePoint ソリューションに機能を追加します。 機能デザイナーを使用します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, features
- features [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 8fc572f6fc5c0444fda619af5af49c6c2e52ac5d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99949117"
---
# <a name="create-sharepoint-features"></a>SharePoint 機能を作成する
  SharePoint 機能を使用すると、関連する SharePoint プロジェクト項目をグループ化して、配置を簡単にすることができます。 SharePoint 機能デザイナーを使用して、フィーチャーを作成したり、スコープを設定したり、他のフィーチャーを依存関係としてマークしたりできます。 このデザイナーでは、マニフェスト (個々の機能を記述する XML ファイル) を生成することもできます。

## <a name="add-features-to-the-sharepoint-solution"></a>SharePoint ソリューションに機能を追加する
 ソリューション エクスプローラーまたはパッケージング エクスプローラーを使用することで、SharePoint ソリューションに機能を追加できます。 機能を追加するには、次のいずれかの方法を使用できます。

- **ソリューション エクスプローラー** で、 **[機能]** のショートカット メニューを開き、 **[機能の追加]** を選択します。

- **パッケージ エクスプローラー** で、[パッケージ] のショートカット メニューを開き、 **[機能の追加]** を選択します。

## <a name="using-the-feature-designer"></a>機能デザイナーの使用
 SharePoint ソリューションには、1 つ以上の SharePoint 機能を含めることができ、ソリューション エクスプローラーの機能ノードの下にグループ化されます。 各機能には、機能のプロパティをカスタマイズするために使用できる独自の **機能デザイナー** があります。 詳細については、「[方法:SharePoint フィーチャーをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-feature.md)」を参照してください。 機能を相互に区別するために、タイトル、説明、バージョン、スコープなどの機能のプロパティを構成できます。

### <a name="feature-designer-options"></a>機能デザイナーのオプション
 機能を作成した後、機能デザイナーを使用してカスタマイズできます。

 機能デザイナーに表示される機能のプロパティを次の表に示します。

|プロパティ|説明|
|--------------|-----------------|
|タイトル|省略可能。 この機能の既定のタイトルは、 *[SolutionName* *FeatureName]* に設定されます。|
|説明|省略可能。 SharePoint 機能の説明です。|
|Scope|必須。 **ソリューション エクスプローラー** を使用して機能を作成した場合、既定ではスコープは [Web] に設定されます。<br /><br /> - Farm: サーバー ファーム全体に対して機能をアクティブにします。<br /><br /> - Site: サイト コレクション内のすべての Web サイトに対して機能をアクティブにします。<br /><br /> - Web: 特定の Web サイトに対して機能をアクティブにします。<br /><br /> - WebApplication: Web アプリケーション内のすべての Web サイトに対して機能をアクティブにします。|
|[ソリューション内の項目]|機能に追加できるすべての SharePoint 項目。|
|機能内の項目|機能に追加されている SharePoint プロジェクト項目。|

## <a name="add-and-remove-sharepoint-project-items"></a>SharePoint プロジェクト項目を追加および削除する
 配置のために SharePoint 機能を追加する SharePoint プロジェクト項目を選択できます。 **機能デザイナー** を使用して、機能の項目の追加と削除を行ったり、機能マニフェストを表示したりします。 詳細については、「[方法: SharePoint 機能に項目を追加および削除する](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)」を参照してください。

## <a name="add-feature-dependencies"></a>機能の依存関係を追加する
 機能マニフェストを構成して、作成した機能がアクティブになる前に SharePoint サーバーによって特定の機能がアクティブ化されるようにできます。 たとえば、作成した SharePoint 機能が機能上またはデータに関して他の機能に依存している場合は、まず機能が依存しているすべての機能のアクティブ化を SharePoint サーバーで試みることができます。 詳細については、「[方法: 機能の依存関係を追加および削除する](../sharepoint/how-to-add-and-remove-feature-dependencies.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [方法: SharePoint 機能をカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [方法: SharePoint 機能の項目を追加および削除する](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
- [方法: 機能の依存関係を追加および削除する](../sharepoint/how-to-add-and-remove-feature-dependencies.md)
