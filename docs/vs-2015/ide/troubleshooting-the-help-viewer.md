﻿---
title: ヘルプ ビューアーのトラブルシューティング |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-help-viewer
ms.topic: troubleshooting
helpviewer_keywords:
- troubleshooting [Help Viewer 2.0]
- Help Viewer 2.0, troubleshooting
ms.assetid: 461a4553-064a-4142-a2d2-058658b9ba12
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 77529ad9957694b1ea1853b3e8b1b1cc29c45e2b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62429731"
---
# <a name="troubleshooting-the-help-viewer"></a>ヘルプ ビューアーのトラブルシューティング
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、ヘルプ ビューアーで発生する可能性のある問題について説明します。  
  
## <a name="audio-doesnt-work"></a>オーディオが機能しない。  
 ヘルプ ビューアーにはオーディオ プレーヤーが含まれていません。 オーディオが含まれるコンテンツをダウンロードした場合に、**[再生]** をクリックしてもコンテンツは再生されません。オーディオ プレーヤーをインストールしてください。  
  
## <a name="search-doesnt-work-in-windows-server-2008-windows-server-2008-with-sp1-or-windows-server-2008-r2"></a>検索は、Windows Server 2008、Windows Server 2008 SP1、または Windows Server 2008 R2 では機能しません。  
 ヘルプ ビューアーの検索機能とフィルター機能を使用するには、Windows Search サービスがインストールされ、オンになっている必要があります。 このサービスは Windows Server 2008、Windows Server 2008 Service Pack 1 (SP1)、および Windows Server 2008 R2 では既定でオフになっています。  
  
#### <a name="to-activate-windows-search-service"></a>Windows Search サービスをアクティブにするには  
  
1. サーバー マネージャーを起動します。  
  
2. 左側のナビゲーション ペインで、**[役割]** を選択します。  
  
3. [役割の概要] ペインで、**[役割の追加]** を選択します。  
  
4. ファイル サービスの役割を選択し、**[次へ]** をクリックします。  
  
5. Windows Search の役割サービスを選択します。  
  
## <a name="additional-resources"></a>その他のリソース  
 次のリソースを使用して、ヘルプ ビューアーで詳細情報を取得し、フィードバックを提供することができます。  
  
- フィードバックを提供するには、Microsoft の Web サイト、[Microsoft Connect](http://go.microsoft.com/fwlink/?linkid=243983) をご覧になるか、[hlpfdbk@microsoft.com](mailto:hlpfdbk@microsoft.com) まで電子メールを送信してください。  
  
- 詳細については、[Developer Documentation and Help System](http://go.microsoft.com/fwlink/?LinkId=232741) (デベロッパー ドキュメントおよびヘルプ システム) フォーラムおよび [The Help Guy](http://go.microsoft.com/fwlink/?LinkId=232743) (ヘルプ ガイ) ブログを参照してください。  
  
## <a name="see-also"></a>関連項目
 [ヘルプ ビューアー 2.1 の管理者ガイド](http://go.microsoft.com/fwlink/?LinkId=243985)
