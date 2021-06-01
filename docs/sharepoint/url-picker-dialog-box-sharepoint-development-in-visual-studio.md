---
title: URL ピッカー ダイアログ ボックス (SharePoint の開発)
description: ユーザーがプロジェクト内または SharePoint を実行しているローカル サーバー上にあるファイルを選択できる URL ピッカー ダイアログ ボックスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.VWD.URLPicker
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, URL picker
- SharePoint development in Visual Studio, designer
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d04857f0e61e5d9f293d73902cd090f718c65cd0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99892217"
---
# <a name="url-picker-dialog-box-sharepoint-development-in-visual-studio"></a>URL ピッカー ダイアログ ボックス (Visual Studio での SharePoint 開発)
  URL ピッカー ダイアログ ボックスでは、プロジェクト内または SharePoint を実行しているローカル サーバー上にあるマスター ページ ファイルやイメージ ファイルなどのファイルを選択できます。

 このダイアログ ボックスは、プロパティを設定するためにファイルを選択できる場合に表示されます。 このダイアログ ボックスを開くには、 **[プロパティ]** ウィンドウのさまざまなプロパティの横にある省略記号ボタン (![ASP.NET モバイル デザイナーの省略記号](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) を選択します。 省略記号ボタンは、デザイナーの **[ソース]** ビューで特定の属性に値を割り当てるときに、IntelliSense のプロンプトとしても表示されます。

## <a name="uielement-list"></a>UIElement の一覧
 **[プロジェクト フォルダー]** プロジェクト内または SharePoint が実行されているローカル サーバー上で定義されている、フォルダーの一覧が表示されます。 サブフォルダーを表示するには、展開ボタンを選択します。

 プロジェクト内のファイルを選択するには、 **[プロジェクト]** ノードを展開します。 ダイアログ ボックスで選択可能なものとして表示されるには、プロジェクト内のファイルが次の条件を満たしている必要があります。

- ファイルは、マップされたフォルダーに格納されている必要があります。

- ファイルは、ソリューション パッケージに追加されている必要があります。

- ファイルが別のプロジェクトに存在していてはなりません。

  これらの条件を満たしていないファイルを参照する場合は、ファイルのパスを手動で入力する必要があります。

  SharePoint が実行されているローカル サーバー上にあるファイルを選択するには、 **[サーバー]** ノードを展開します。 ダイアログ ボックスで選択可能なものとして表示されるには、これらのファイルが次の条件を満たしている必要があります。

- ファイルは、**Images**、**Layouts**、または **ControlTemplates** のいずれかのマップされたフォルダーに存在する必要があります。

- ファイルが SharePoint コンテンツ データベースに存在していてはなりません。

  これらの条件を満たしていないファイルを参照する場合は、ファイルのパスを手動で入力する必要があります。

  **[フォルダーの内容]** 選択したフォルダー内のファイルの一覧が表示されます。 ファイルを選択して、 **[OK]** ボタンを選択すると、ダイアログ ボックスが閉じて、呼び出し元のプロセスに選択内容が送信されます。

  **[ファイルの種類]** 実行しているタスクに適したファイルの一覧から選択できます。

## <a name="see-also"></a>こちらもご覧ください
- [SharePoint のアプリケーション ページの作成](../sharepoint/creating-application-pages-for-sharepoint.md)
- [SharePoint の Web パーツを作成する](../sharepoint/creating-web-parts-for-sharepoint.md)
- [Web パーツまたはアプリケーション ページの再利用できるコントロールを作成する](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
