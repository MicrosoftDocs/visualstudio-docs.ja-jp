---
title: 優先時間 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.preemption
helpviewer_keywords:
- Concurrency Visualizer, Preemption Time
ms.assetid: 6b78f91e-a006-440c-83fb-e7368040951d
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6fd209f65464126650106eb4509cd3de39ad8c25
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2019
ms.locfileid: "54752640"
---
# <a name="preemption-time"></a>優先時間
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

タイムライン内のこれらのセグメントは、優先として分類されるブロック時間と関連付けられています。 このカテゴリは、次のいずれかの理由によってスレッドが切り替えられたことを意味します。  
  
- より優先順位の高いスレッドを使用してスケジューラが置換した。  
  
- そのスレッドの実行クォンタムが期限切れになり、別のスレッドの実行準備が整った。  
  
  この期間中、コンカレンシー ビジュアライザーが優先としてカウントしているカーネル待機理由によって、1 つのスレッドがブロックされています。 優先セグメントは、1 つのスレッドが論理コアから排除されたときに開始し、そのスレッドが実行を再開したときに終了します。  
  
  優先セグメントのツールヒントには、優先の原因となったプロセスまたはスレッドの名前が表示されます。 ただし、優先されたプロセスまたはスレッドが優先期間を通じて実際に実行されることを意味するものではありません。  
  
## <a name="see-also"></a>関連項目  
 [スレッド ビュー](../profiling/threads-view-parallel-performance.md)
