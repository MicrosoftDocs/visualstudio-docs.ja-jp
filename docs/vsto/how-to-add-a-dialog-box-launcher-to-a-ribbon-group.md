---
title: '方法: リボン グループにダイアログ ボックス起動ツールを追加する'
description: ダイアログ ボックス起動ツールをリボン上の任意のグループに追加して、グループに関連するその他のオプションを提供するダイアログ ボックスまたは作業ウィンドウを開くことができます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- dialog box launcher [Office development in Visual Studio]
- Ribbon [Office development in Visual Studio], dialog box launcher
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d8e04b7549d1b6a458f0993804946502f55f0165
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99942283"
---
# <a name="how-to-add-a-dialog-box-launcher-to-a-ribbon-group"></a>方法: リボン グループにダイアログ ボックス起動ツールを追加する
  リボン上の任意のグループにダイアログ ボックス起動ツールを追加できます。 ダイアログ ボックス起動ツールは、グループ内に表示される小さなアイコンです。 ユーザーはこのアイコンをクリックして、グループに関連するその他のオプションを提供するダイアログ ボックスまたは作業ウィンドウを開くことができます。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-add-a-dialog-box-launcher-to-a-ribbon-group"></a>リボン グループにダイアログ ボックス起動ツールを追加する

1. **ソリューション エクスプローラー** でリボン コードファイル ( *.vb* または *.cs* ファイル) を選択します。

2. **[表示]** メニューの **[デザイナー]** をクリックします。

3. リボン デザイナーで、任意のグループを右クリックし、 **[DialogBoxLauncher の追加]** をクリックします。

     カスタムまたは組み込みのダイアログ ボックスを開くには、グループの <xref:Microsoft.Office.Tools.Ribbon.RibbonGroup.DialogLauncherClick> イベントにコードを追加します。

## <a name="see-also"></a>関連項目
- [リボンの概要](../vsto/ribbon-overview.md)
- [実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)
- [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)
- [リボン デザイナー](../vsto/ribbon-designer.md)
- [リボン オブジェクト モデルの概要](../vsto/ribbon-object-model-overview.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [方法: リボンをリボン デザイナーからリボン XML にエクスポートする](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)
- [方法: リボンのタブの位置を変更する](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)
- [方法: 組み込みタブをカスタマイズする](../vsto/how-to-customize-a-built-in-tab.md)
- [方法: Backstage ビューにコントロールを追加する](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [Outlook のリボンのカスタマイズ](../vsto/customizing-a-ribbon-for-outlook.md)
- [方法: リボンのカスタマイズの概要](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [方法: アドインのユーザー インターフェイス エラーを表示する](../vsto/how-to-show-add-in-user-interface-errors.md)
- [チュートリアル: リボン デザイナーを使用してカスタム タブを作成する](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [チュートリアル: 実行時にリボンのコントロールを更新する](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)
- [チュートリアル : リボン XML を使用してカスタム タブを作成する](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
