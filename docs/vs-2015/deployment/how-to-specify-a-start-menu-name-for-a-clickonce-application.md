---
title: '方法: ClickOnce アプリケーションのスタート メニューの名前を指定します |。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Start menu resource name
- Start menu name
- ClickOnce deployment, Start menu name
ms.assetid: 4b5183b2-2fd4-4433-9310-4a73bb12c4e3
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 30bb4050399bf7a6d9120f7e5454b26ce505af35
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68149761"
---
# <a name="how-to-specify-a-start-menu-name-for-a-clickonce-application"></a>方法: ClickOnce アプリケーションのスタート メニューの名前を指定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

オンラインまたはオフラインで利用できる [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションがインストールされると、**スタート**メニューおよび**プログラムの追加と削除** の一覧にエントリが追加されます。 既定では、表示される名前はアプリケーション アセンブリの名前と同じですが、**発行オプション** のダイアログ ボックスで**製品名**を設定することで表示名を変更することがきます。  
  
 **製品名** は publish.htm のページに表示されます；インストールされたオフライン アプリケーションの場合、この名前が **スタート** メニューに表示されるエントリの名前になり、**プログラムの追加または削除** にも同じ名前が表示されます。  
  
 **パブリッシャー名** は publish.htm ページの**製品名**の上に表示され、インストールされたオフライン アプリケーションの場合、**スタート**メニューの中で、アプリケーションのアイコンが含まれているフォルダーの名前として表示されます。  
  
 **製品名**と**パブリッシャー名**のプロパティは、**プロジェクト デザイナー**の**発行**ページにある**発行オプション** ダイアログ ボックスで設定することができます。  
  
### <a name="to-specify-a-start-menu-name"></a>スタート メニューの名前を指定するには  
  
1. **ソリューション エクスプ ローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **発行**タブをクリックします。  
  
3. **オプション**ボタンをクリックして、**発行オプション** ダイアログ ボックスを開きます。  
  
4. **説明**をクリックします。  
  
5. **発行オプション** ダイアログ ボックスで、**製品名**に表示する名前を入力します。  
  
6. 必要に応じて、**パブリッシャー名**にパブリッシャー名を入力します。  
  
## <a name="see-also"></a>関連項目  
 [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)   
 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
