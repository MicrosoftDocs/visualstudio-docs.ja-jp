---
title: '方法: エンドユーザーがからインストールする場所を指定 |Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], specifying an installation URL
- URLs, specifying an installation URL
- installation, specifying installation an URL
- Installation URL property
ms.assetid: 04a804bf-ed55-4a7a-a1e6-f63ed99c0276
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 113356a664d94fdd2e8d3e53fae6025d8ef22e60
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2018
ms.locfileid: "49213006"
---
# <a name="how-to-specify-the-location-where-end-users-will-install-from"></a>方法: エンド ユーザーがインストールを開始する場所を指定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

発行するときに、[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]アプリケーションをダウンロードしてインストール、アプリケーションにアクセスするユーザーの場所は必ずしも、アプリケーションを最初に発行する場所。 たとえば、一部の組織で、開発者は、ステージング サーバーにアプリケーションを公開可能性があり、管理者は、アプリケーションを Web サーバーを移動し。  
  
 この場合、使用することができます、`Installation URL`プロパティをユーザーは、アプリケーションのダウンロードにアクセスする Web サーバーを指定します。 これは、機能は、アプリケーション マニフェストが更新プログラムを検索する場所を認識できるように必要です。  
  
 `Installation URL`でプロパティを設定することができます、**発行**のページ、**プロジェクト デザイナー**します。  
  
 **注**、`Installation URL`を使用してプロパティを設定することも、**発行ウィザード**します。 詳細については、[方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)を参照してください。  
  
### <a name="to-specify-an-installation-url"></a>インストール URL を指定するには  
  
1.  **ソリューション エクスプ ローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2.  **発行**タブをクリックします。  
  
3.  インストール URL フィールドに、形式を使用して完全修飾 URL を使用して、インストール場所を入力します。 http://www.microsoft.com/ApplicationName、または UNC パス形式を使用して\\\Server\ApplicationName します。  
  
## <a name="see-also"></a>関連項目  
 [方法: Visual Studio がファイルをコピーする場所を指定する](../deployment/how-to-specify-where-visual-studio-copies-the-files.md)   
 [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)   
 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)



