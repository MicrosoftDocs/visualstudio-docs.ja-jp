---
title: 同期時間 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.synchronization
helpviewer_keywords:
- Concurrency Visualizer, Synchronization Time
ms.assetid: affa04cc-8bba-4848-9301-b19846d3c2cb
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 8d4c6542c2e72428c06825a1d44ba7d0b04b7648
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53903826"
---
# <a name="synchronization-time"></a>同期時間
タイムライン内のこれらのセグメントは、同期として分類されたブロック時間に関連付けられています。 同期でスレッドにブロックされたマークが付いている場合、次のいずれかを示しています。  
  
- スレッドの実行が、`EnterCriticalSection()` または `WaitForSingleObject()` などの既知のスレッド同期 API を呼び出す結果になった可能性がある。  
  
- API 照合アルゴリズムが全体として包括的にならず、そのために他のカテゴリにマップされている可能性がある一部の API も同期として表示されている可能性がある。呼び出し履歴内のフレームの最終的な到達先が、このカテゴリにマップされた、基になるカーネルをブロックしている基本要素である場合にこの状態になります。  
  
  スレッド ブロック イベントの根本的な原因を理解するために、ブロック呼び出し履歴とプロファイル レポートをよく調べてください。  
  
## <a name="see-also"></a>関連項目  
 [スレッド ビュー](../profiling/threads-view-parallel-performance.md)