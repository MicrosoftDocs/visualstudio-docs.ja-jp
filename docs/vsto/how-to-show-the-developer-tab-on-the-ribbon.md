---
title: '方法: [開発者] タブをリボンに表示する。'
description: Visual Studio を使用して、Microsoft Word 文書のリボンに [開発] タブをプログラムで表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], tabs
- Developer tab [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 081d6740aa31a31173b12e467b1b8e32a074604a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99927718"
---
# <a name="how-to-show-the-developer-tab-on-the-ribbon"></a>方法: [開発者] タブをリボンに表示する。
  Office アプリケーションのリボン内にある **[開発]** タブは既定では表示されないため、このタブにアクセスするには、このタブが表示されるように構成する必要があります。 たとえば、Word のドキュメント レベルのカスタマイズに <xref:Microsoft.Office.Tools.Word.GroupContentControl> を追加しようとする場合、このタブを表示する必要があります。

> [!NOTE]
> このガイダンスは Office 2010 以降のアプリケーションのみに適用されます。 2007 Microsoft Office system でこのタブを表示する場合は、このトピックの次のバージョン「[方法: [開発] タブをリボンに表示する](https://web.archive.org/web/20140303033431/msdn.microsoft.com/library/bb608625(v=vs.90).aspx
)」を参照してください。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

> [!NOTE]
> Access には **[開発]** タブはありません。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="to-show-the-developer-tab"></a>[開発] タブを表示するには

1. このトピックでサポートされている Office アプリケーションのいずれかを起動します。 このトピックで前述されている「**対象:** 」メモを参照してください。

2. **[ファイル]** タブの **[オプション]** をクリックします。

     次の図に、Office 2010 内の **[ファイル]** タブと **[オプション]** ボタンを示します。

     ![Outlook 2010 で [ファイル]、[オプション] を選択](../vsto/media/vsto-office-file-tab.png "Outlook 2010 で [ファイル]、[オプション] を選択")

     次の図に、Office 2013 内の **[ファイル]** タブを示します。

     ![Outlook 2013 の [File] (ファイル) タブ](../vsto/media/vsto-office2013-filetab.png "Outlook 2013 の [File] (ファイル) タブ")

     次の図に、Office 2013 内の **[オプション]** ボタンを示します。

     ![Outlook 2013 Preview の [Options] (オプション) ボタン](../vsto/media/vsto-office2013-optionsbutton.png "Outlook 2013 Preview の [Options] (オプション) ボタン")

3. _[ApplicationName_ **のオプション]** ダイアログ ボックスで、 **[リボンのユーザー設定]** をクリックします。

     次の図に、Excel 2010 内の **[オプション]** ダイアログ ボックスと **[リボンのユーザー設定]** ボタンを示します。 このボタンの位置は、このトピックの上部付近の「対象」セクションに記載されている他のすべてのアプリケーションで同様です。

     ![[リボンのユーザー設定] ボタン](../vsto/media/vsto-office2010-customizeribbonbutton.png "[リボンのユーザー設定] ボタン")

4. メイン タブの一覧で、 **[開発]** チェック ボックスをオンにします。

     次の図に、Word 2010 および [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 内の **[開発]** チェック ボックスを示します。 このチェック ボックスの位置は、このトピックの上部付近の「対象」セクションに記載されている他のすべてのアプリケーションと同様です。

     ![[Word のオプション] ダイアログの [開発] チェック ボックス](../vsto/media/vsto-office2010-developercheckbox.png "[Word のオプション] ダイアログの [開発] チェック ボックス")

5. **[OK]** をクリックして **[オプション]** ダイアログ ボックスを閉じます。

## <a name="see-also"></a>関連項目
- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)
