---
title: リソース競合データ値について | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- concurrency profiling method
- Profiling Tools, concurrency method
ms.assetid: 071c0f0f-1eba-4dc8-ae87-0810e4086dd0
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f9a6ac882a258767fd1de1ebd45015e9b86912e9
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49911994"
---
# <a name="understanding-resource-contention-data-values"></a>リソース競合データ値について
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

リソース競合プロファイルでは、アプリケーションで競合するスレッドによる共有リソースへのアクセスで待機が発生するたびに、詳細な呼び出し履歴情報が収集されます。  
  
 **必要条件**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]、 [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]、 [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
  リソース競合レポートには、発生した競合の合計数と、リソースに対する合計待機時間 (待機が発生したモジュール、関数、ソース コード行、命令についての合計待機時間) が表示されます。  
  
- 包括値は、リソースの競合により関数を強制的に待機状態にした競合の合計数、および関数が待機した合計時間を示します。  包括値には、関数によって呼び出された子関数によって発生した競合が含まれています。  
  
- 排他値は、関数を待機状態にした競合の数、および関数の本体のコードによって発生した競合の数のみを示します。 子関数によって発生した競合は含まれません。 関数の排他時間には、関数本体のステートメントによって発生した待機時間のみが含まれます。  
  
  リソース競合レポート ビューには、一定期間内の個々の競合イベントを表示するタイムライン グラフも含まれ、特定のイベントを発生させたコール スタックも表示します。 詳細については、次のトピックを参照してください。  
  
- [スレッドの詳細ビュー](../profiling/thread-details-view-contention-data.md)  
  
- [リソースの詳細ビュー](../profiling/resource-details-view-contention-data.md)  
  
  コンカレンシー プロファイルの 2 つ目のモードの詳細については、「[Concurrency Visualizer (コンカレンシー ビジュアライザー)](../profiling/concurrency-visualizer.md)」を参照してください。



