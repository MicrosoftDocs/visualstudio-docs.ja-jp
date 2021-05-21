---
title: '方法: マップされたフォルダーの追加と削除を行う | Microsoft Docs'
description: SharePoint プロジェクトにマップされたフォルダーの追加と削除を行います。  マップされたフォルダーの配置場所を変更します。 マップされたフォルダーの名前を変更または削除します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.Project.MappedFolder
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, mapped folders
- mapped folders [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e6771482925a935d1b6424412d4176db5e9ad6c6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99923475"
---
# <a name="how-to-add-and-remove-mapped-folders"></a>方法: マップされたフォルダーの追加と削除を行う
  画像やレイアウトなど、SharePoint でよく使用されるフォルダーの中には、ファイル階層に深く埋め込まれているものがあります。 これらのフォルダーを SharePoint プロジェクトにマップして、より簡単にアクセスすることができます。 マップされたフォルダーは、SharePoint サーバーのインストール内のファイルの物理的な場所に対応する SharePoint プロジェクト内のフォルダーです。

 SharePoint アプリケーションを配置すると、ソリューション パッケージ (.wsp) によって、マップされたフォルダーとそのすべてのサブフォルダーの内容が、SharePoint を実行しているサーバーの SharePoint フォルダー ツリー内の特定の場所にコピーされます。 この場所は、マップされたフォルダーに設定されている **[配置場所]** プロパティによって決まります。 マップされたフォルダー内のすべてのサブフォルダーは、マップされたフォルダーの **配置場所** を基準としています。 マップされたフォルダーの名前ではなく、 **[配置場所]** プロパティによって、項目が配置される場所が決まります。
プロジェクトのメニュー バーまたはショートカット メニューのコマンドを使用して、マップされたフォルダーをプロジェクトに追加できます。 **[Add SharePoint "Images" Mapped Folder]\(SharePoint のマップされた "Images" フォルダーの追加\)** と **[Add SharePoint "Layouts" folder]\(SharePoint の "Layouts" フォルダーの追加\)** コマンドを使用して、最も頻繁に使用されるマップされたフォルダーを追加できます。 ショートカット メニューの **[SharePoint のマップされたフォルダーの追加]** コマンドを使用した後、 **[SharePoint のマップされたフォルダーの追加]** ダイアログ ボックスでフォルダーを指定することで、他の利用可能な SharePoint フォルダーをプロジェクトにマップできます。

## <a name="add-mapped-folders-to-a-project"></a>マップされたフォルダーをプロジェクトに追加する
 次の手順では、2 つのマップされたフォルダーを視覚的 Web パーツ プロジェクトに追加する方法について説明します。 始めるには、視覚的 Web パーツ プロジェクトを作成します。

#### <a name="to-add-mapped-folders-to-a-project"></a>マップされたフォルダーをプロジェクトに追加するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual Basic]** または **[Visual C#]** のいずれかのノードを展開します。 **[Office/SharePoint]** ノードを展開し、 **[SharePoint ソリューション]** ノードを選択します。

3. プロジェクト テンプレートの一覧で、 **[SharePoint 2013 Visual Web パーツ]** テンプレートを選択します。

4. **[名前]** ボックスに「**TestProject1**」と入力した後、 **[OK]** ボタンをクリックします。

5. **SharePoint カスタマイズ ウィザード** で、 **[完了]** ボタンをクリックして既定の設定を保持します。

6. **ソリューション エクスプローラー** で、プロジェクト ノードを選択します。次に、メニュー バーで **[プロジェクト]**  >  **[Add SharePoint "Images" Mapped Folder]\(Add SharePoint のマップされた "Images" フォルダーの追加\)** を選択します。

     TestProject1 という名前のサブフォルダーを含む **Images** という名前のフォルダーがプロジェクト内に表示されます。 このマップされたフォルダーには、視覚的 Web パーツ プロジェクトの画像が含まれています。

7. **ソリューション エクスプローラー** で、プロジェクト ノードを選択します。次に、メニュー バーで **[プロジェクト]**  >  **[SharePoint のマップされたフォルダーの追加]** を選択して、 **[SharePoint のマップされたフォルダーの追加]** ダイアログ ボックスを表示します。

8. マッピングに使用できるフォルダーのツリー ビューで、 **[リソース]** フォルダーを選択し、 **[OK]** ボタンをクリックします。

     **Resources** という名前のフォルダーがプロジェクトに表示されます。 このフォルダーに、文字列リソース ファイルなどのアイテムを格納できます。 サブフォルダーは、マップされたフォルダーの内容を整理するのに便利ですが、 **[SharePoint マップ フォルダーの追加]** コマンドを使用してマップされたフォルダーを追加しても、自動的には作成されません。 サブフォルダーを追加するには、**Resources** フォルダーを選択し、メニュー バーで **[プロジェクト]**  >  **[新しいフォルダー]** を選択します。

## <a name="change-the-deployment-location-of-a-mapped-folder"></a>マップされたフォルダーの配置場所を変更する
 既定では、マップされたフォルダーは、SharePoint ルート インストール パスを基準とする特定の場所に追加されます。それは \<SharePointRoot> トークンによって示されます。 ただし、マップされたフォルダーの **[配置場所]** プロパティを変更することで、この場所を変更できます。 マップされたフォルダーには、それぞれに固有の **[配置場所]** プロパティがあります。

#### <a name="to-change-the-deployment-location-of-a-mapped-folder"></a>マップされたフォルダーの配置場所を変更するには

1. 前の手順で作成したプロジェクトで、マップされたフォルダーを選択します。

2. **[プロパティ]** ウィンドウで、 **[配置場所]** プロパティの省略記号 (![ASP.NET Mobile デザイナーの省略記号](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) ボタンをクリックします。

3. **[SharePoint のマップされたフォルダーの追加]** ダイアログ ボックスで、マップされたフォルダーのポイント先となるフォルダーを参照します。

4. ノードを選択し、 **[OK]** ボタンをクリックします。

## <a name="rename-or-remove-mapped-folders"></a>マップされたフォルダーの名前変更または削除を行う

#### <a name="to-rename-or-remove-a-mapped-folder"></a>マップされたフォルダーの名前変更または削除を行うには

1. 前の手順で作成したプロジェクトで、マップされたフォルダーを選択します。

2. マップされたフォルダーの名前を変更するには、そのショートカット メニューを開き、 **[名前の変更]** をクリックし、新しい名前を入力して Enter キーを押します。

     別の方法として、名前を変更するマップされたフォルダーを選択し、 **[プロパティ]** ウィンドウを開き、 **[フォルダー名]** プロパティの値を新しい名前に設定できます。

3. マップされたフォルダーをプロジェクトから削除するには、そのショートカット メニューを開き、 **[削除]** を選択してから、ダイアログ ボックスの **[OK]** ボタンをクリックして削除を確定します。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
