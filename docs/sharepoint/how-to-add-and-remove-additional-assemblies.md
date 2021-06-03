---
title: '方法: アセンブリを追加および削除する | Microsoft Docs'
description: SharePoint ソリューション パッケージでアセンブリを追加および削除する方法について説明します。 セーフ コントロールとクラス リソースも追加または削除します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.CustomAssembly
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: cc672a8a0ff7edd66504b5ecbf48e622fad085ea
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99923617"
---
# <a name="how-to-add-and-remove-additional-assemblies"></a>方法: アセンブリを追加および削除する
  SharePoint パッケージが機能またはデータについて他のアセンブリに依存している場合、そのアセンブリをソリューション パッケージ (.wsp) に追加できます。 パッケージをインストールする際は、カスタム アセンブリがインストールされているかどうかが、SharePoint サーバーによって確認されます。

 アセンブリに関連付けられているセーフ コントロールやクラス リソース ファイルを追加および変更することもできます。

## <a name="add-additional-assemblies-safe-controls-and-class-resources"></a>アセンブリ、セーフ コントロール、およびクラス リソースを追加する
 SharePoint ソリューション パッケージにアセンブリを追加できます。 サンドボックス ソリューションの追加アセンブリは、グローバル アセンブリ キャッシュに配置されますが、サンドボックス ソリューションの SharePoint プロジェクト項目はコンテンツ データベースに追加されます。 これらの追加アセンブリにセーフ コントロールやクラス リソースを追加することもできます。 セーフ コントロールの詳細については、「[プロジェクト項目でのパッケージ化と配置の情報の提供](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)」または「[SharePoint Foundation で Web パーツを展開する](/previous-versions/office/developer/sharepoint-2010/cc768621(v=office.14))」の「SafeControl エントリの作成」を参照してください。

#### <a name="to-add-an-existing-assembly"></a>既存のアセンブリを追加するには

1. **パッケージ デザイナー** を開きます。 詳細については、「[方法: SharePoint ソリューション パッケージをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)」を参照してください。

2. **[詳細]** タブを選択します。

3. **[追加]** ボタンを選択し、一覧の **[既存のアセンブリの追加]** を選択します。

     **[既存のアセンブリの追加]** ダイアログ ボックスが表示されます。

4. 省略記号 (![ASP.NET モバイル デザイナーの省略記号](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) を選択し、追加するアセンブリを選択します。 移植性を考慮して、選択したアセンブリへの相対パスを使用することをお勧めします。

5. **[配置ターゲット]** で、グローバル アセンブリ キャッシュにアセンブリを配置する場合は **[GlobalAssemblyCache]** オプション ボタンを選択し、SharePoint を実行するサーバーの WebApplication フォルダーにアセンブリを配置する場合は **[WebApplication]** オプション ボタンを選択します。

#### <a name="to-add-an-assembly-from-project-output"></a>プロジェクトの出力からアセンブリを追加するには

1. **パッケージ デザイナー** を開きます。

     詳細については、「[方法: SharePoint ソリューション パッケージをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)」を参照してください。

2. **[詳細]** タブを選択します。

3. **[追加]** ボタンを選択し、一覧の **[プロジェクト出力からアセンブリを追加]** を選択します。

     **[プロジェクト出力からアセンブリを追加]** ダイアログ ボックスが表示されます。

4. **[ソース プロジェクト]** の一覧で、追加するソース プロジェクトを選択します。

5. **[配置ターゲット]** で、グローバル アセンブリ キャッシュにアセンブリを配置する場合は **[GlobalAssemblyCache]** オプション ボタンを選択し、SharePoint を実行するサーバーの WebApplication フォルダーにアセンブリを配置する場合は **[WebApplication]** オプション ボタンを選択します。

#### <a name="to-add-a-safe-control"></a>セーフ コントロールを追加するには

1. **[既存のアセンブリの編集]** ダイアログ ボックスを開きます。 これには、パッケージ デザイナーを開いて **[詳細設定]** タブを選択し、アセンブリを選択して、 **[編集]** ボタンを選択します。

2. **[安全なコントロール]** ペインで、 **[新しい項目を追加するにはここをクリックします]** ボタンを選択します。

3. **[アセンブリ名]** 列に、アセンブリの名前を入力します。

4. **[名前空間]** 列に、セーフ コントロールの名前空間の名前を入力します。

5. **[型の名前]** 列に、型の名前を入力します。

#### <a name="to-add-a-class-resource"></a>クラス リソースを追加するには

1. **[既存のアセンブリの編集]** ダイアログ ボックスを開きます。 これには、パッケージ デザイナーを開いて **[詳細設定]** タブを選択し、アセンブリを選択して、 **[編集]** ボタンを選択します。

2. **[クラス リソース]** ペインで、 **[新しい項目を追加するにはここをクリックします]** ボタンを選択します。

3. **[ファイル名]** 列で省略記号 (![ASP.NET モバイル デザイナーの省略記号](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) を選択し、追加するクラス リソースを選択します。

## <a name="delete-custom-assemblies"></a>カスタム アセンブリを削除する
 SharePoint パッケージからアセンブリを削除したり、既存のアセンブリからセーフ コントロールやクラス リソースを削除することもできます。

#### <a name="to-delete-an-existing-assembly"></a>既存のアセンブリを削除するには

1. **パッケージ デザイナー** を開きます。 詳細については、「[方法: SharePoint ソリューション パッケージをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)」を参照してください。

2. **[詳細]** タブを選択します。

3. **[追加アセンブリ]** ペインで、削除するカスタム アセンブリを選択します。

4. **[削除]** をクリックします。

#### <a name="to-delete-a-safe-control-for-an-assembly"></a>アセンブリの安全なコントロールを削除するには

1. **[既存のアセンブリの編集]** ダイアログ ボックスを開きます。 これには、パッケージ デザイナーを開いて **[詳細設定]** タブを選択し、アセンブリを選択して、 **[編集]** ボタンを選択します。

2. 削除する安全なコントロールをクリックします。

3. Del キーを押します。

#### <a name="to-delete-a-class-resource-for-an-assembly"></a>アセンブリのクラス リソースを削除するには

1. **[既存のアセンブリの編集]** ダイアログ ボックスを開きます。 これには、パッケージ デザイナーを開いて **[詳細設定]** タブを選択し、アセンブリを選択して、 **[編集]** ボタンを選択します。

2. 削除するクラス リソースをクリックします。

3. Del キーを押します。

## <a name="see-also"></a>関連項目
- [SharePoint フィーチャーを作成する](../sharepoint/creating-sharepoint-features.md)
- [方法: SharePoint フィーチャーをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [方法: SharePoint フィーチャーの項目を追加および削除する](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
