---
title: リモートで SharePoint ソリューション パッケージの配置、発行、およびアップグレードを行う
titleSuffix: ''
description: リモート サイトまたはローカル SharePoint サイトで、サンドボックス化された SharePoint ソリューションを配置、発行、およびアップグレードします。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- remote deployment [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, remote deployment
- deploying [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ab301f11ffdae03564f05388dfbba55a90d12391
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99913688"
---
# <a name="how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server"></a>方法: リモート サーバー上で SharePoint ソリューションを配置、発行、およびアップグレードする
  SharePoint ソリューションをローカル システムに配置するだけでなく、リモート サイトまたはローカル SharePoint サイトに対して、サンドボックス化された SharePoint ソリューションを発行できます。 リモート発行プロセスでは、SharePoint サーバーに *.wsp* ファイルがコピーされ、ソリューションがインストールされて、ソリューションのアクティブ化が可能になります。 リモート SharePoint ソリューションを変更した後に、そのインストールをアップグレードすることもできます。

## <a name="to-publish-a-sandboxed-sharepoint-solution-to-a-remote-sharepoint-server"></a>サンドボックス化される SharePoint ソリューションをリモート SharePoint サーバーに発行するには

1. **ソリューション エクスプローラー** で、発行するサンドボックス化された SharePoint プロジェクトのショートカット メニューを開き、 **[発行]** を選択します。

2. **[発行]** ダイアログ ボックスで、 **[SharePoint サイトに発行する]** オプションを選択し、オンライン発行サイトの URL (`https://mytestsite.sharepoint.microsoftonline.com` など) を入力します。

3. 発行後に **ソリューション ギャラリー** ページにソリューションの一覧を表示するには、 **[発行後にブラウザーでソリューション ギャラリーを開く]** オプション ボタンを選択します。

4. **[発行]** をクリックします。

5. ユーザー認証が必要な場合は、リモート サーバーにサインインします。

     発行の進行状況が Visual Studio の **[出力]** ウィンドウに表示されます。 プロセスが終了すると、ソリューション ( *.wsp*) ファイルがリモートの SharePoint サーバーにインストールされます。 ただし、SharePoint で使用する前に、アクティブにする必要があります。

6. **[ソリューション ギャラリー]** ページで SharePoint アプリケーションを選択し、リボンの **[アクティブ化]** ボタンをクリックします。

7. **[ソリューションのアクティブ化]** ダイアログ ボックスのリボンで、 **[アクティブ化]** ボタンをもう一度選択します。

     **[ソリューション ギャラリー]** ページの **[状態]** 列に、アプリケーションがアクティブであることが示されます。

## <a name="to-upgrade-a-sandboxed-sharepoint-solution-on-a-remote-sharepoint-server"></a>サンドボックス化された SharePoint ソリューションをリモート SharePoint サーバーに発行するには
 セキュリティで保護された SharePoint ソリューションがリモート サーバーで既に発行されている場合、次のプロセスを使用すると、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] でアプリケーションを変更した後で、アップグレードできます。

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で SharePoint パッケージの名前を変更します。 これをするには、**ソリューション エクスプローラー** で、パッケージを開きます。 **パッケージ エクスプローラー** に表示されます。

2. **パッケージ エクスプローラー** の **[名前]** ボックスで、パッケージ名を一意の名前に変更します。

3. プロジェクトを保存します。

4. **ソリューション エクスプローラー** で、プロジェクトのショートカット メニューを開き、 **[発行]** を選択します。

5. **[発行]** ダイアログ ボックスで、 **[SharePoint サイトに発行する]** オプション ボタンを選択し、その後ソリューションが保存されているリモート サーバーの URL がない場合は、それを入力します。

6. 発行後に **ソリューション ギャラリー** ページにソリューションの一覧を表示するには、 **[発行後にブラウザーでソリューション ギャラリーを開く]** オプション ボタンを選択します。

7. **[発行]** をクリックします。

8. ユーザー認証が必要な場合は、リモート サーバーにサインインします。

     最近リモート サーバーにログインした場合、認証は必要ない可能性があります。

     同じ名前を持つ古いバージョンのアプリケーションが SharePoint サーバーにまだ存在している場合は、同じ名前のパッケージが SharePoint サーバーに既に存在するというエラーが表示されます。 発行する前に、パッケージ名を一意の名前に変更する必要があります。

9. SharePoint で新しいアプリケーションを選択し、リボンの **[アップグレード]** ボタンを選択します。

10. **[ソリューションのアップグレード]** ダイアログ ボックスのリボンで、 **[アップグレード]** ボタンをもう一度選択します。 **[ソリューション ギャラリー]** ページの **[状態]** 列に、アプリケーションがアクティブであることが示されるようになったはずです。

     以前のバージョンのソリューションは非アクティブ化されています。新しいバージョンのソリューションは、古いソリューションから保持されているデータでアップグレードされ、新しいソリューションは SharePoint でアクティブ化されます。

## <a name="see-also"></a>関連項目
- [方法: SharePoint ソリューションをローカルの SharePoint サイトに配置および発行する](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)
- [SharePoint ソリューション パッケージを作成する](../sharepoint/creating-sharepoint-solution-packages.md)
- [方法: SharePoint ソリューション パッケージをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [方法: パッケージ デザイナーを使用してパッケージのフィーチャーおよび項目を追加および削除する](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)
