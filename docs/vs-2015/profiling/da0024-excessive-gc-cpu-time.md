---
title: 'DA0024: 過剰な GC CPU 時間 | Microsoft Docs'
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
- vs.performance.DA0024
- vs.performance.24
- vs.performance.rules.DA0024
ms.assetid: 228872da-77d0-4da5-b455-ac57fb1867c9
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9fdc10bc78bed3597ea121376ca2235cfd6acbc7
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2018
ms.locfileid: "47534940"
---
# <a name="da0024-excessive-gc-cpu-time"></a>DA0024: 過剰な GC CPU 時間
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックの最新バージョンをご覧[da 0024: 過剰な GC CPU 時間](https://docs.microsoft.com/visualstudio/profiling/da0024-excessive-gc-cpu-time)します。  
  
規則 Id |DA 0024 |  
|カテゴリ |。NET Framework の使用 |  
|プロファイル方法 |すべて |  
|メッセージ | % Time in GC が非常に高いです。 ガベージ コレクションのオーバーヘッドの量が過剰な |。  
|規則の種類 |警告 |  
  
 サンプリング、.NET メモリ、またはリソース競合メソッドを使用してプロファイリングを行うときは、この規則を呼び出すためのサンプルを少なくとも 10 個収集する必要があります。  
  
## <a name="cause"></a>原因  
 プロファイリングの間に収集されたシステム パフォーマンス データで、ガベージ コレクションに費やされた時間がアプリケーション処理時間全体と比較して大き過ぎることが示されています。  
  
## <a name="rule-description"></a>規則の説明  
 Microsoft .NET 共通言語ランタイム (CLR: Common Language Runtime) は、自動メモリ管理メカニズムを備えています。このメカニズムでは、ガベージ コレクターを使用して、アプリケーションが使用しなくなったオブジェクトのメモリを解放します。 ガベージ コレクターはジェネレーション指向です。これは、多くの割り当てが短時間で終了することを前提としています。 たとえば、ローカル変数の有効期間は短時間です。 新しく作成されたオブジェクトはジェネレーション 0 (gen 0) から始まり、ガベージ コレクションの実行中に破棄されなければジェネレーション 1 に昇格します。その後もアプリケーションによって引き続き使用されていれば、最後はジェネレーション 2 に昇格します。  
  
 ジェネレーション 0 のオブジェクトの収集頻度は高く、通常は非常に効率的に収集されます。 ジェネレーション 1 のオブジェクトの収集頻度はそれよりも低くなり、収集効率も下がります。 有効期間の長いジェネレーション 2 のオブジェクトの場合、収集頻度はさらに低くなります。 また、ジェネレーション 2 のコレクション (フル ガベージ コレクションの実行) は、最も負荷のかかる操作になります。  
  
 この規則は、ガベージ コレクションに費やされた時間がアプリケーションの全体の処理時間と比較して過度に大きい場合に適用されます。  
  
> [!NOTE]
>  ガーベジ コレクションに費やされた時間の割合が、アプリケーション全体の処理時間と比較して高いが過度ではない場合、この規則ではなく、「[DA0023: 高い GC CPU 時間。](../profiling/da0023-high-gc-cpu-time.md)」の警告が適用されます。  
  
## <a name="how-to-investigate-a-warning"></a>警告の調査方法  
 [エラー一覧] ウィンドウに表示されたメッセージをダブルクリックして、プロファイル データの [[マーク] ビュー](../profiling/marks-view.md)に移動します。 **.NET CLR Memory\\% Time in GC** 列を探します。 マネージド メモリのガベージ コレクションが他のフェーズよりも多い特定のプログラム実行フェーズがあるかどうかを確認します。 % Time in GC の値と、**# of Gen 0 Collections**、**# of Gen 1 Collections**、**# of Gen 2 Collections** 値で報告されているガベージ コレクションの割合を比較してください。  
  
 % Time in GC 値は、アプリケーションの処理時間全体に占めるガベージ コレクションの実行時間を報告します。 % Time in GC 値が非常に高くても、それが過度なガベージ コレクションのためではない場合もあることに注意してください。 % Time in GC 値の計算方法の詳細については、MSDN の「**Maoni's Weblog**」 (Maoni のブログ) の「[Difference Between Perf Data Reported by Different Tools – 4](http://go.microsoft.com/fwlink/?LinkId=177863)」 (ツールによってレポートされるパフォーマンス データの違い 4) を参照してください。 ページ フォールトが発生している場合や、コンピューター上の優先順位の高い処理のためにアプリケーションに割り込みが発生している場合、% Time in GC カウンターにはそれらの遅延が反映されます。



