---
title: 実行プロファイル レポート | Microsoft ドキュメント
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.cv.threads.report.execution
helpviewer_keywords:
- Concurrency Visualizer, Execution Profile Report
ms.assetid: c8128472-a8ed-46f4-b1c8-a25358d6f2c1
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a66f3961cc6ddd4bb3f8970c77a8f7cff9b0fe22
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49849230"
---
# <a name="execution-profile-report"></a>実行プロファイル レポート
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

実行プロファイル レポートは、従来のサンプリング プロファイルです。 サンプルは、論理コア上でスレッドが実行されている期間中におよそミリ秒ごとに取得されます。コンカレンシー ビジュアライザーが、累積された一連のサンプル セットを照合して、標準的なコール ツリーをビルドします。 このテーブルのデータは、現在の時間範囲と非表示のスレッドの影響、および適用されるフィルターの影響を受ける場合があります。  
  
- [マイ コードのみ] が選択されている場合、ユーザー コードのあるスタック フレームと、そのユーザー コードの 1 つ下のレベルのみが表示されます。  
  
- [不要項目の非表示] 値が設定されている場合、指定した頻度を下回る照合済みスタックはレポートから除外されます。  
  
  次の表は、テーブル内の列を示しています。  
  
|Column|説明|  
|------------|-----------------|  
|名前|呼び出し履歴の各レベルの関数の名前。|  
|包括サンプル|このレベルの呼び出し履歴のツリーにまとめられたすべてのスタックについて集められたサンプルの合計数。 包括数は、この関数の排他サンプルと、すべての子ノードの包括カウンターの合計です。|  
|排他サンプル|この関数が呼び出し履歴の最も低いレベルにある、収集されたサンプルの合計数。|  
|% 包括|包括サンプル列に表示されているサンプルの合計の割合。 割合は小数点以下 2 桁に丸めて表示されます。|  
|% 排他|排他サンプル列に表示されているサンプルの合計の割合。 割合は小数点以下 2 桁に丸めて表示されます。|  
|説明|関数の完全修飾名。 これには、利用できる場合、行数が含まれます。|  
  
 このレポートの表については、[実行時間 (スレッド ビュー)](../profiling/execution-time-threads-view.md) ビューで確認できます。  
  
## <a name="see-also"></a>関連項目  
 [スレッド ビュー](../profiling/threads-view-parallel-performance.md)



