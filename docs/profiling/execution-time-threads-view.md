---
title: "実行時間 (スレッド ビュー) | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-debug"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vs.cv.threads.timeline.execution"
helpviewer_keywords: 
  - "同時実行ビジュアライザー、実行時間 (スレッド ビュー)"
ms.assetid: 80c100f8-2502-4613-bfef-4f4f2e09cc8d
caps.latest.revision: 10
author: "mikejo5000"
ms.author: "mikejo"
manager: "ghogen"
caps.handback.revision: 10
---
# <a name="execution-time-threads-view"></a>実行時間 (スレッド ビュー)
スレッド ビュー タイムラインのこれらのセグメントは、スレッドがシステムの論理コア上で動作中である場合、実行時間を表します。  
  
 スレッド ステータスの変更は、カーネル コンテキスト スイッチ イベントを介して検出されます。 Windows イベント トレーシング (ETW) でミリ秒ごとにサンプル履歴がキャプチャされます。 非常に短い緑のセグメントでは、サンプルが取得されない可能性があります。 そのため、一部の短い実行セグメントには、呼び出し履歴が表示されない場合があります。  
  
 実行セグメントをクリックすると、同時実行ビジュアライザーがクリックの位置に最も近いサンプル履歴を表示します。 そのサンプル履歴の場所は、タイムラインの上に黒の矢印 (キャレット) で示され、サンプル履歴が **[現在]** タブに表示されます。  
  
 現在のビューのすべての実行セグメントについて、従来のサンプリング プロファイルを参照するには、表示されているタイムライン プロファイルで **[実行]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [実行プロファイル レポート](../profiling/execution-profile-report.md)   
 [スレッド ビュー](../profiling/threads-view-parallel-performance.md)


<!--HONumber=Feb17_HO4-->


