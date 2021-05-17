---
title: オフラインまたはオンラインのインストール モードを指定する (ClickOnce)
description: アプリケーションをオフラインまたはオンラインで利用できるかどうかを決定するインストール モードを ClickOnce アプリケーションに対して指定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, specifying install mode
- install mode
- online applications
- offline applications
- ClickOnce install mode
ms.assetid: 0aee5fc1-e966-4bda-9b8f-d9997aeaa779
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 918cb7e60f4e3fed2beee024d51b94499b14b632
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99900422"
---
# <a name="how-to-specify-the-clickonce-offline-or-online-install-mode"></a>方法: ClickOnce のオフラインまたはオンラインのインストール モードを指定する
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの `Install Mode` は、アプリケーションがオフラインまたはオンラインで利用できるかどうかを決定します。 **[アプリケーションをオンラインでのみ利用できる]** を選択した場合、ユーザーはアプリケーションを実行するために、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 発行場所 (Web ページまたはファイル共有) にアクセスできる必要があります。 **[アプリケーションはオフラインでも利用できる]** を選択すると、アプリケーションによってエントリが **[スタート]** メニューと **[プログラムの追加と削除]** ダイアログ ボックスに追加されます。ユーザーは、接続されていないときにアプリケーションを実行できます。

`Install Mode` は、**プロジェクト デザイナー** の **[発行]** ページで設定できます。

> [!NOTE]
> `Install Mode` は、発行ウィザードを使用して設定することもできます。 詳細については、「[方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)」を参照してください。

### <a name="to-make-a-clickonce-application-available-online-only"></a>ClickOnce アプリケーションをオンラインでのみ利用できるようにするには

1. **ソリューション エクスプローラー** でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[公開]** タブをクリックします。

3. **[インストールモードと設定]** 領域で、 **[アプリケーションはオンラインでのみ利用できる]** オプション ボタンをクリックします。

### <a name="to-make-a-clickonce-application-available-online-or-offline"></a>ClickOnce アプリケーションをオンラインまたはオフラインで利用できるようにするには

1. **ソリューション エクスプローラー** でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[公開]** タブをクリックします。

3. **[インストールモードと設定]** 領域で、 **[アプリケーションはオフラインでも利用できる]** オプション ボタンをクリックします。

     アプリケーションをインストールすると、 **[スタート]** メニューと [コントロールパネル] の **[プログラムの追加と削除]** にエントリが追加されます。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
- [ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)