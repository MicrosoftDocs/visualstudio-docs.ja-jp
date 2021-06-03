---
title: '方法: リボンのタブの位置を変更する'
description: リボンのカスタム タブの順序を変更したり、タブ コレクション エディターを使用して、リボン上の組み込みタブの前または後にカスタム タブを配置したりすることができます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], tabs
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: dc0b4548ffa4e5efa75734b5528a7021cf122bfa
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99921914"
---
# <a name="how-to-change-the-position-of-a-tab-on-the-ribbon"></a>方法: リボンのタブの位置を変更する
  リボンのカスタム タブの順序は、**タブ コレクション エディター** を使用して変更できます。 リボン上の組み込みタブの前または後ろにカスタム タブを配置することができます。 組み込みタブは、Microsoft Office アプリケーションのリボンに用意されているタブです。 たとえば、 **[データ]** タブは、Excel の組み込みタブです。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-change-the-order-of-tabs-on-the-ribbon"></a>リボンのタブの順序を変更するには

1. **ソリューション エクスプローラー** でリボン コードファイル ( *.vb* または *.cs* ファイル) を選択します。

2. **[表示]** メニューの **[デザイナー]** をクリックします。

3. リボン デザイナーを右クリックし、 **[プロパティ]** をクリックします。

4. **[プロパティ]** ウィンドウで **[タブ]** プロパティを選択してから、省略記号ボタン (![ASP.NET モバイル デザイナーの省略](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) をクリックします。

     **タブ コレクション エディター** が表示されます。

5. **タブ コレクション エディター** の **[メンバー]** リストで、移動するタブを選択し、上矢印または下矢印をクリックしてタブ オーダーを変更します。

### <a name="to-position-a-tab-before-or-after-a-built-in-tab-on-the-ribbon"></a>リボン上の組み込みタブの前または後にタブを配置するには

1. リボン デザイナーで、カスタム タブを選択します。

2. **プロパティ]** [ ウィンドウで、] **[ControlId** プロパティを展開し、 **[ControlIdType]** プロパティの値が **Custom** に設定されていることを確認します。

3. **[プロパティ]** ウィンドウで **[Position]** プロパティを展開します。

4. **[PositionType]** プロパティを適切な値に設定します。

    - **BeforeOfficeId** に設定すると、グループは指定の組み込みタブの前に配置されます。

    - **AfterOfficeId** に設定すると、グループは指定の組み込みタブの後ろに配置されます。

5. 組み込みタブのコントロール ID に **OfficeId** プロパティを設定します。

     コントロール ID の一覧については、「[Office 2010 ヘルプ ファイル: Office Fluent ユーザー インターフェイスのコントロール ID](https://www.microsoft.com/download/details.aspx?id=6627)」を参照してください。

## <a name="see-also"></a>関連項目
- [リボンの概要](../vsto/ribbon-overview.md)
- [リボン デザイナー](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [チュートリアル: リボン デザイナーを使用したカスタムタブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [チュートリアル : リボン XML を使用してカスタム タブを作成する](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
