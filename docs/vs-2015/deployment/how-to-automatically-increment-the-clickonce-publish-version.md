---
title: '方法: 発行のバージョンに自動的にインクリメント ClickOnce |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], incrementing publish version automatically
- Publish Version property, incrementing
- ClickOnce deployment, incrementing publish version automatically
- publishing, ClickOnce
ms.assetid: 686ab88a-6305-4914-a05b-fe269cc0ae1e
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0d779e364f5cbe7bc4b90e0a77ab3fb825a7b6c2
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58976267"
---
# <a name="how-to-automatically-increment-the-clickonce-publish-version"></a>方法: ClickOnce の発行バージョンを自動的にインクリメントする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

発行するときに、[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]を変更するアプリケーション、`Publish Version`プロパティにより、アプリケーションの更新プログラムとして発行します。 既定では、Visual Studio が自動的にインクリメント、`Revision`の数、`Publish Version`アプリケーションを発行するたびにします。  
  
 この動作を無効にすることができます、**発行**のページ、**プロジェクト デザイナー**します。  
  
> [!NOTE]
>  実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「 [Visual Studio での開発設定のカスタマイズ](http://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
### <a name="to-disable-automatically-incrementing-the-publish-version"></a>発行バージョンを自動的にインクリメントを無効にするには  
  
1.  **ソリューション エクスプ ローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2.  **発行**タブをクリックします。  
  
3.  **発行バージョン** セクションで、クリア、**リリースごとにリビジョンを自動的に**チェック ボックスをオンします。  
  
## <a name="see-also"></a>関連項目  
 [方法: 発行バージョンを設定、ClickOnce](../deployment/how-to-set-the-clickonce-publish-version.md)   
 [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)   
 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
