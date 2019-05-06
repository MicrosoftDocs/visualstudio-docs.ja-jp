---
title: '方法: CD インストールの自動開始を有効にする |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, AutoStart
- ClickOnce deployment, installation on CD or DVD
- deploying applications [ClickOnce], installation on CD or DVD
ms.assetid: caaec619-900c-4790-90e3-8c91f5347635
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 66f5510ae63507aebb97a7f8bdfd3e367f1afc85
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62928507"
---
# <a name="how-to-enable-autostart-for-cd-installations"></a>方法: CD インストールの自動開始を有効にする
デプロイするときに、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] CD-ROM または DVD-ROM などのリムーバブル メディアを使用して、アプリケーションを有効にできます`AutoStart`ように、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]メディアが挿入されると、アプリケーションが自動的に起動します。

 `AutoStart` 有効にすることができます、**発行**のページ、**プロジェクト デザイナー**します。

### <a name="to-enable-autostart"></a>自動開始を有効にするには

1. **ソリューション エクスプ ローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **発行**タブをクリックします。

3. **[オプション]** ボタンをクリックします。

     **発行オプション** ダイアログ ボックスが表示されます。

4. クリックして**展開**します。

5. 選択、**の CD のインストールは、CD が挿入されたときに自動的にセットアップを開始**チェック ボックスをオンします。

     *Autorun.inf*アプリケーションを発行するときにファイルを発行場所にコピーされます。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)