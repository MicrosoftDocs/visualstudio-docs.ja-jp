---
title: '方法: ClickOnce アプリケーションのセキュリティ ゾーンの設定 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, security settings
- code access security, ClickOnce applications
- security zones, ClickOnce applications
ms.assetid: d3dac454-518a-44d7-a76e-ccb7b9c3a150
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0da7c3d4129102339eaf74fac815f086e027a4f3
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "54980675"
---
# <a name="how-to-set-a-security-zone-for-a-clickonce-application"></a>方法: ClickOnce アプリケーションのセキュリティ ゾーンを設定する
ClickOnce アプリケーションのコード アクセス セキュリティ アクセス許可を設定するときは、まず、 **プロジェクト デザイナー** の **[セキュリティ]** ページで、アクセス許可の基本セットを指定する必要があります。  
  
 また、ほとんどの場合、制限されたアクセス許可セットを含む **[インターネット]** ゾーン、またはより大きいアクセス許可セットを含む **[ローカル イントラネット]** ゾーンを選択することもできます。 アプリケーションにカスタムのアクセス許可が必要な場合は、 **[カスタム]** セキュリティ ゾーンを選択します。 カスタム アクセス許可の設定の詳細については、次を参照してください。[方法。ClickOnce アプリケーションのカスタム アクセス許可を設定する](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)  
  
### <a name="to-set-a-security-zone"></a>セキュリティ ゾーンを設定するには  
  
1.  **ソリューション エクスプ ローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2.  **[セキュリティ]** タブをクリックします。  
  
3.  **[ClickOnce セキュリティ設定を有効にする]** チェック ボックスをオンにします。  
  
4.  **[これは部分的に信頼するアプリケーションです]** オプション ボタンを選択します。  
  
     **[ClickOnce セキュリティのアクセス許可]** セクション内のコントロールが有効になります。  
  
5.  **[アプリケーションのインストール元のゾーン]** ドロップダウン リストでセキュリティ ゾーンを選択します。  
  
## <a name="see-also"></a>関連項目  
 [方法: ClickOnce アプリケーションのカスタム アクセス許可を設定する](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)   
 [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)   
 [ClickOnce アプリケーションのコード アクセス セキュリティ](../deployment/code-access-security-for-clickonce-applications.md)   
