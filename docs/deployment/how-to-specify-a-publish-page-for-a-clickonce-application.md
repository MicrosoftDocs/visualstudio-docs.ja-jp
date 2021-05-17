---
title: 発行ページを指定する (ClickOnce アプリケーション)
description: プロジェクトの [発行ページ] プロパティを設定する方法について説明します。これにより、ClickOnce アプリケーションの Web ページを指定できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], specifying publish page
- Publish Page property
- publishing, ClickOnce
- ClickOnce deployment, specifying publish page
ms.assetid: 9d70eebb-bdee-4b42-8e7e-7a07e199bdf7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f58b7d8d4244f7c429c3866bf76c514bf24164ff
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99940450"
---
# <a name="how-to-specify-a-publish-page-for-a-clickonce-application"></a>方法: ClickOnce アプリケーションの発行ページを指定する
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを発行すると、既定の Web ページ (publish.htm) が生成され、アプリケーションと共に発行されます。 このページには、アプリケーションの名前、アプリケーションをインストールするためのリンクや前提条件、および [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] を説明するヘルプ トピックへのリンクが含まれます。 プロジェクトの **[発行ページ]** プロパティを使用すると、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの Web ページの名前を指定できます。

 発行ページが指定されると、次回の発行時、その発行場所にコピーされます。再び発行する場合は、上書きされません。 ページの外観をカスタマイズする場合、変更内容が失われることを心配せずに行うことができます。 詳細については、「[方法: ClickOnce の既定の Web ページをカスタマイズする](../deployment/how-to-customize-the-default-web-page-for-a-clickonce-application.md)」を参照してください。

 **[発行ページ]** プロパティは、**プロジェクト デザイナー** の **[発行]** ペインからアクセスできる **[発行オプション]** ダイアログ ボックスで設定できます。

### <a name="to-specify-a-custom-web-page-for-a-clickonce-application"></a>ClickOnce アプリケーションの発行ページを指定するには

1. **ソリューション エクスプ ローラー** でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[発行]** ペインを選択します。

3. **[オプション]** ボタンをクリックして、 **[発行オプション]** ダイアログ ボックスを開きます。

4. **[デプロイ]** をクリックします。

5. **[発行オプション]** ダイアログ ボックスで、 **[公開後に配置 Web ページを開く]** チェック ボックスがオンになっていることを確認します (既定ではオンになっています)。

6. **[配置 Web ページ]** ボックスに、Web ページの名前を入力し、 **[OK]** をクリックします。

### <a name="to-prevent-the-publish-page-from-launching-each-time-you-publish"></a>発行するたびに発行ページが起動されないようにするには

1. **ソリューション エクスプ ローラー** でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[発行]** ペインを選択します。

3. **[オプション]** ボタンをクリックして、 **[発行オプション]** ダイアログ ボックスを開きます。

4. **[デプロイ]** をクリックします。

5. **[発行オプション]** ダイアログ ボックスで、 **[公開後に配置 Web ページを開く]** チェック ボックスをオフにします。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
- [方法: ClickOnce の既定の Web ページをカスタマイズする](../deployment/how-to-customize-the-default-web-page-for-a-clickonce-application.md)