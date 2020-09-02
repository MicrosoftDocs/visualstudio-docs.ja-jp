---
title: スリープ時間 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.sleep
helpviewer_keywords:
- Concurrency Visualizer, Sleep Time
ms.assetid: 3ddb96f9-9bda-4a68-ad4d-ef488a0a68dc
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8a79bbca9f6275f115105cc2ba6b001ac0ca7d44
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198375"
---
# <a name="sleep-time"></a>スリープ時間
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

タイムライン内のこれらのセグメントは、スリープとして分類されるブロック時間と関連付けられています。 スリープのカテゴリは、スレッドが自発的にその論理コアを明け渡して、処理を行わなかったことを示しています。 この期間中、コンカレンシー ビジュアライザーがスリープとしてカウントしている API で、1 つのスレッドがブロックされています。 `Sleep()` や `SwitchToThread()` などの API がこのグループになります。  
  
## <a name="see-also"></a>参照  
 [スレッドビュー](../profiling/threads-view-parallel-performance.md)
