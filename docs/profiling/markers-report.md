---
title: マーカー レポート | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.report.markers
ms.assetid: 829ce099-172e-4c7e-bbd0-578b110c59bd
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3b46cb18e1972d22010ce356f1d9208f391f6d79
ms.sourcegitcommit: 42ea834b446ac65c679fa1043f853bea5f1c9c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/19/2018
---
# <a name="markers-report"></a>マーカー レポート
マーカー レポートには、表示されているタイム フレーム内のマーカーが一覧表示されます。  レーンをパン、ズーム、または非表示にすると、マーカーの表示/非表示が切り替わる場合があります。 レポートには、各マーカーに関する次の情報が含まれています。  
  
-   それを開始したときの、トレースの開始からの相対時間。  
  
-   実行継続時間。 フラグとメッセージの場合には、瞬間を表すために実行継続時間はゼロです。  
  
-   それを生成したスレッドの ID。  
  
-   それを生成した Event Tracking for Windows (ETW) プロバイダー。  
  
-   それが書き始められたマーカーの系列。  
  
-   それが属しているイベントのカテゴリ。  
  
-   その重要度レベル。  
  
-   その種類 (スパン、フラグ、またはメッセージ)。  
  
-   それが表すものについての概要  
  
 マーカー レポートを CSV ファイルとして保存するには、**[エクスポート]** ボタンを選択します。 CSV ファイル内のデータは、他のアプリやツールで使用することができます。  
  
> [!NOTE]
>  マーカー レポートでは 1,000 個のマーカーを表示できます。 すべてのマーカーを表示するには、レポート全体を CSV ファイルにエクスポートします。