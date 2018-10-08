---
title: メッセージ マーカー | Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.cv.markers.message
ms.assetid: 721f40ca-5af2-4a01-b8b6-2b90f6cb7f89
caps.latest.revision: 18
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: dd2487466518622ebd1b2a52c4e4697be23a40d9
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2018
ms.locfileid: "47536977"
---
# <a name="message-markers"></a>メッセージ マーカー
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックの最新バージョンをご覧[メッセージ マーカー](https://docs.microsoft.com/visualstudio/profiling/message-markers)します。  
  
メッセージ マーカーは、ログ出力を表します。 メッセージは、特定のスレッドによって特定の時間に発行される文字列です。 メッセージは、その他のツールで使用するためにテキスト ファイルにエクスポートできます。 メッセージ文字列を確認するには、コンカレンシー ビジュアライザーで、メッセージにポインターを置くことができます。 そして、[マーカー レポート](../profiling/markers-report.md)で、すべてのメッセージ マーカーを確認できます。  次の図は、メッセージ マーカーを示しています。  
  
## <a name="message-aggregation-markers"></a>メッセージの集約マーカー  
 コンカレンシー ビジュアライザーで、複数のメッセージが相互に近接しすぎて、個別に描画できないことがあります。 そのような場合には、基になるメッセージを表す*メッセージ集約マーカー*が表示されます。 それらのアイコンのいずれかにポインターを置くと、表現されている、基になるメッセージの数がツールヒントに表示されます。 メッセージを表示するには、ズームインします。  限界までズームインしてもなお集約マーカーが表示される場合には、基になるメッセージを[マーカー レポート](../profiling/markers-report.md)で確認できます。  
  
## <a name="see-also"></a>関連項目  
 [コンカレンシー ビジュアライザー マーカー](../profiling/concurrency-visualizer-markers.md)   
 [コンカレンシー ビジュアライザー SDK](../profiling/concurrency-visualizer-sdk.md)



