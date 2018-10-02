---
title: リソースの詳細ビュー - 競合データ | Microsoft Docs
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
- vs.performance.view.resourcedetails
helpviewer_keywords:
- Resource Details view
ms.assetid: a4ecfe1c-abbc-4fb3-9ab2-34de50486901
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 760240544971062da3a5161eab7d203ba6d097c0
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2018
ms.locfileid: "47534660"
---
# <a name="resource-details-view---contention-data"></a>リソースの詳細ビュー - 競合データ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックの最新バージョンをご覧[リソース詳細ビュー - 競合データ](https://docs.microsoft.com/visualstudio/profiling/resource-details-view-contention-data)します。  
  
リソースの詳細ビューには、選択したリソースに対する競合によって発生したブロック イベントが、タイムライン グラフで表示されます。 ブロック イベントは、リソースに対するアクセスを別のスレッドがロックしているためにスレッドが実行を中断されたときに発生します。  
  
 このビューには、各スレッドの実行タイムラインが横軸で、各ブロック イベントがスレッドのタイムライン上に縦棒で示されます。 必要に応じて、タイムラインのあるセクションを拡大して、個別のイベントを表示することもできます。 イベント到達するまでの関数の実行パス (呼び出し履歴) を表示するには、そのイベントの棒をクリックします。 関数が **[呼び出し履歴]** ウィンドウに表示されます。 関数のソース コードが使用可能な場合は、関数名をクリックして [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のインターフェイスでソース ファイルを編集できます。  
  
## <a name="procedures"></a>手順  
  
#### <a name="to-magnify-a-timeline-segment"></a>タイムライン セグメントを拡大するには  
  
-   タイムラインの領域をマウス ポインターでドラッグします。  
  
     マウス ボタンを離すと、選択した時間セグメントに合わせてビューが表示されます。 セグメントをさらに拡大する手順を繰り返すことができます。 時間スクロール バーのスクロール ボックスは、ビューに表示されている時間セグメントの相対サイズを表します。  
  
#### <a name="to-zoom-out-on-a-timeline"></a>タイムラインを縮小するには  
  
-   次のいずれかの操作を実行します。  
  
    -   前のズーム レベルに戻るには、**[縮小]** をクリックします。  
  
    -   タイムライン全体をビューに表示するには、**[ズームのリセット]** をクリックします。  
  
#### <a name="to-view-the-call-stack-of-an-event"></a>イベントの呼び出し履歴を表示するには  
  
-   タイムライン グラフで、イベント バーをクリックします。  
  
#### <a name="to-view-or-edit-the-source-code-of-a-function-in-the-call-stack"></a>呼び出し履歴内の関数のソース コードを表示または編集するには  
  
-   **[呼び出し履歴]** ウィンドウで関数名をクリックします。  
  
 関数のソース コードは、現在のプロジェクトに含まれている必要があります。  
  
#### <a name="to-view-the-call-tree-of-contention-events-for-the-resource"></a>リソースの競合イベントの呼び出しツリーを表示するには  
  
-   タイムライン グラフで、**[合計]** をクリックします。  
  
     リソースの競合ビューが表示されます。 詳細については、「[Resource Contentions View](../profiling/resource-contentions-view-contention-data.md) (リソースの競合ビュー)」をご覧ください。  
  
#### <a name="to-view-all-the-contention-events-of-a-thread"></a>スレッドのすべての競合イベントを表示するには  
  
-   タイムライン グラフで、スレッドの名前または ID をクリックします。  
  
     選択したスレッドに対して [スレッドの詳細] ビューが表示されます。 詳細については、「[Thread Details View](../profiling/thread-details-view-contention-data.md) (スレッドの詳細ビュー)」をご覧ください。



