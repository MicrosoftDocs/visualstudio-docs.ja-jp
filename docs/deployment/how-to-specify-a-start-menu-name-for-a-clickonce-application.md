---
title: ClickOnce アプリケーションのスタート メニューの名前を指定する
description: '[発行オプション] ダイアログ ボックスで製品名を設定して ClickOnce アプリケーションの表示名を変更する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Start menu resource name
- Start menu name
- ClickOnce deployment, Start menu name
ms.assetid: 4b5183b2-2fd4-4433-9310-4a73bb12c4e3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a9c9dee27ae78375dcb667bba5157ea84c046073
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99940437"
---
# <a name="how-to-specify-a-start-menu-name-for-a-clickonce-application"></a>方法: ClickOnce アプリケーションのスタート メニューの名前を指定する
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションがオンラインとオフラインの両方で使用するようにインストールされると、 **[スタート]** メニューと **[プログラムの追加と削除]** の一覧にエントリが追加されます。 既定では、表示名はアプリケーション アセンブリの名前と同じですが、 **[発行オプション]** ダイアログ ボックスの **[製品名]** を設定して表示名を変更できます。

 **[製品名]** は *publish.htm* ページに表示されます。インストール済みのオフライン アプリケーションの場合は、 **[スタート]** メニューのエントリの名前になり、 **[プログラムの追加と削除]** に表示される名前にもなります。

 **[パブリッシャー名]** は *publish.htm* ページで **[製品名]** の上部に表示されます。インストール済みのオフライン アプリケーションの場合は、 **[スタート]** メニュー内のアプリケーションのアイコンが含まれるフォルダーの名前にもなります。

 [スタート] メニューのショートカットまたはアプリケーション参照は、 *%Appdata%\Microsoft\Windows\Start Menu\Programs \\<publisher name\>* で作成されます。 ショートカットまたはアプリケーション参照には、製品名と同じ名前が付けられます。

 **[発行オプション]** ダイアログ ボックスでは、 **[製品名]** プロパティと **[パブリッシャー名]** プロパティを設定できます。このダイアログ ボックスは、**プロジェクト デザイナー** の **[発行]** ページにあります。

### <a name="to-specify-a-start-menu-name"></a>[スタート] メニューの名前を指定するには

1. **ソリューション エクスプローラー** でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[公開]** タブをクリックします。

3. **[オプション]** ボタンをクリックして、 **[発行オプション]** ダイアログ ボックスを開きます。

4. **[説明]** をクリックします。

5. **[発行オプション]** ダイアログ ボックスで、表示する名前を **[製品名]** に入力します。

6. 必要に応じて、 **[パブリッシャー名]** にパブリッシャー名を入力できます。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)