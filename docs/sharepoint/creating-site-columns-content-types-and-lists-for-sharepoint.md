---
title: SharePoint のサイト列、コンテンツ タイプ、およびリストの作成 | Microsoft Docs
titleSuffix: ''
description: SharePoint のサイト列、コンテンツ タイプ、リストを作成します。 Visual Studio には、これらの種類の SharePoint 項目のプロジェクト項目テンプレートが用意されています。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.ListDesigner.ContentTypeSetting
- VS.SharePointTools.ContentTypeDesigner.CommonPropertiesPage
- VS.SharePointTools.ListDesigner.CreatingLists
- VS.SharePointTools.ListDesigner.ListPage
- VS.SharePointTools.ListDesigner.ViewPage
- VS.SharePointTools.ListDesigner.CommonPropertiesPage
- VS.SharePointTools.ContentTypeDesigner.ColumnsPage
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: dfdf94f58c0fa7ba40d7c08309f8ea57949310df
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99949026"
---
# <a name="create-site-columns-content-types-and-lists-for-sharepoint"></a>SharePoint のサイト列、コンテンツ タイプ、リストの作成
  Visual Studio には、"*リスト*" や "*コンテンツ タイプ*" (どちらもサイト列 (または "*フィールド*") を組み込むことができます) など、多くのさまざまな基本的な SharePoint 項目のプロジェクト項目テンプレートが用意されています。 コンテンツ タイプとリスト用の新しいデザイナーでは、これらの項目をこれまで以上に簡単に作成することができます。

## <a name="site-columns"></a>サイト内の列
 サイト列は、SharePoint プロジェクトに追加できる最も基本的な要素の 1 つです。 サイト列はデータの種類を表します。たとえば、連絡先一覧であれば、連絡先の電話番号、コメント、都市名などです。

 新しいサイト列プロジェクト項目テンプレートでは、以前のバージョンの Visual Studio よりも簡単にサイト列を作成できます。 新しいサイト列を作成した後、サイト列の *Elements.xml* ファイル内の XML を変更して、その表示名、データ型、および SharePoint にサイト列を表示するグループなどの目的の情報を含めることができます。 サイト列の詳細については、「[列について](/previous-versions/office/developer/sharepoint-2010/ms450825(v=office.14))」を参照してください。

## <a name="content-types-and-lists"></a>コンテンツ タイプとリスト
 コンテンツ タイプとリストは、SharePoint で最も頻繁に使用される要素の 1 つです。

 コンテンツ タイプは、SharePoint のリストまたはドキュメント ライブラリ内の項目のカテゴリのメタデータ、ワークフロー、および動作を定義します。 たとえば、連絡先一覧やタスク一覧の情報のコンテンツ タイプを作成できます。 連絡先のコンテンツ タイプには、名前、電子メール、電話番号、住所などの列が含まれる場合があります。 サイト レベルで定義するコンテンツ タイプは、サイト内のどのリストまたはドキュメント ライブラリからも独立しています。 SharePoint サイトのさまざまなリストやドキュメント ライブラリで同じコンテンツ タイプを使用できます。 また、同じリストやドキュメント ライブラリで複数のコンテンツ タイプを使用することもできます。

 リストは、他のユーザーと共有できる、SharePoint 内の情報のコレクションです。 リストは、データが含まれている列の行で構成されます。 リストの例としては、タスク一覧、連絡先一覧、お知らせリストなどがあります。

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の新しいコンテンツ タイプとリストのデザイナーにより、以前のバージョンの Visual Studio よりもはるかに簡単で直感的にサイトのコンテンツ タイプとリストを作成できます。 この UI では、使い慣れた方法でコンテンツ タイプとリストを視覚的に作成できます。また、リストのデータを並べ替えたりグループ化したり、グループの見出しを使用したりすることができます。 コンテンツ タイプの詳細については、「[コンテンツ タイプ](/previous-versions/office/developer/sharepoint-2010/ms479905(v=office.14))」を参照してください。 リストの詳細については、「[リスト フォーム](/previous-versions/office/developer/sharepoint-2010/aa543232(v=office.14))」と「[リスト ビュー](/previous-versions/office/developer/sharepoint-2010/ff604021(v=office.14))」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[チュートリアル: SharePoint のサイト列、コンテンツ タイプ、リストの作成](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)|カスタムのコンテンツ タイプで使用されるサイト列を作成する方法を示します。 その後、コンテンツ タイプはカスタム リストで使用されます。|

## <a name="see-also"></a>関連項目
- [SharePoint 2010 での開発入門](/sharepoint/dev/)
