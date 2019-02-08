---
title: エラー :Web サイトのワーカー プロセスが IIS によって停止されました |Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.web_server_process_terminated
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 30cab8602690df47a6fba18c3bc738a53959f036
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "54946127"
---
# <a name="error-web-site-worker-process-has-been-terminated-by-iis"></a>エラー :Web サイトのワーカー プロセスが IIS によって停止されました
デバッガーが Web サイト上のコードの実行を停止しました。 このため、インターネット インフォメーション サービス (IIS: Internet Information Services) はワーカー プロセスが応答を停止したと見なしました。 したがって、IIS がワーカー プロセスを終了しました。  
  
 デバッグを継続するには、ワーカー プロセスが継続できるように IIS を設定する必要があります。 このエラー メッセージは、IIS 7 より古いバージョンの IIS では表示されません。  
  
### <a name="to-configure-iis-7-to-allow-the-worker-process-to-continue"></a>ワーカー プロセスを継続できるように IIS 7 を構成するには  
  
1. **[管理ツール]** ウィンドウを開きます。  
  
   1.  **[スタート]** ボタンをクリックし、**[コントロール パネル]** をクリックします。  
  
   2.  **コントロール パネル**で必要に応じて **[クラシック表示に切り替える]** を選択し、**[管理ツール]** をダブルクリックします。  
  
2. **[管理ツール]** ウィンドウで、**[インターネット インフォメーション サービス (IIS) マネージャー]** をダブルクリックします。  
  
    IIS マネージャーが開きます。  
  
3. **[接続]** ウィンドウで、必要に応じて [\<computer name>] ノードを展開します。  
  
4. [\<computer name>] ノードの下にある **[アプリケーション プール]** をクリックします。  
  
5. **[アプリケーション プール]** ボックスの一覧で、アプリケーションが実行されているプールの名前を右クリックし、**[詳細設定]** をクリックします。  
  
6. **[詳細設定]** ダイアログ ボックスの **[プロセス モデル]** セクションで、以下のいずれかを実行します。  
  
   - **[Ping の有効化]** を **[False]** に設定します。  
  
   - **[Ping 最大応答時間]** を 90 秒より大きな値に設定します。  
  
     **[Ping の有効化]** を **[False]** に設定すると、IIS でワーカー プロセスがまだ実行されているかどうかのチェックが中止され、デバッグされているプロセスを停止するまでワーカー プロセスは有効な状態を保ちます。 **[Ping 最大応答時間]** を大きな値に設定すると、IIS はワーカー プロセスの監視を継続できます。  
  
7. **[OK]** をクリックして **[詳細設定]** ダイアログ ボックスを閉じます。  
  
8. IIS マネージャーと **[管理ツール]** ウィンドウを閉じます。  
  
## <a name="see-also"></a>関連項目  
 [リモート デバッグ エラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)