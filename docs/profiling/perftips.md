---
title: PerfTips | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 509d2d4f-48a5-4cdf-acad-6f7b75421303
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: aea4cc095b900a1a81da4b85281c03b4bd8a7d1d
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53831642"
---
# <a name="perftips"></a>パフォーマンスのヒント
Visual Studio デバッガーの *PerfTips* 、および統合デバッガー **診断ツール** は、デバッグ中のアプリのパフォーマンス監視と分析に役立ちます。  
  
 デバッガー統合診断ツールは開発中のパフォーマンスの問題を発見する優れた手段ですが、デバッガーはアプリのパフォーマンスに大きな影響を与えることがあります。 より正確なパフォーマンス データを収集するには、Visual Studio 診断ツールの使用を検討してください。このツールは、パフォーマンス調査の追加手段としてデバッガーの外部で実行されます。 「[デバッガーを使用して、または使用せずにプロファイリング ツールを実行する](../profiling/running-profiling-tools-with-or-without-the-debugger.md)」をご覧ください。  
  
## <a name="perftips"></a>パフォーマンスのヒント  
 デバッガーがブレークポイントで実行を停止するか、ステップ実行を停止した場合、エディター ウィンドウに、ヒントとして前のブレークポイントからその中断までの経過時間が表示されます。 詳細については、「[PerfTips:Performance Information at-a-glance while Debugging with Visual Studio](https://blogs.msdn.microsoft.com/devops/2014/08/18/perftips-performance-information-at-a-glance-while-debugging-with-visual-studio/)」 (パフォーマンスのヒント: Visual Studio を使用したデバッグ中のパフォーマンス概要の参照) を参照してください。  
  
 ![PerfTip](../profiling/media/dbgdiag_perf_perftip.png "DBGDIAG_PERF_PerfTip")  
  
## <a name="diagnostics-tools-window"></a>[診断ツール] ウィンドウ  
 ブレークポイントおよび関連付けられているタイミング データは、**[診断ツール]** ウィンドウに記録されます。  
  
 次の図は、Visual Studio 2015 Update 1 の **[診断ツール]** ウィンドウを示しています。  
  
 ![DiagnosticTools&#45;Update1](../profiling/media/diagnostictools-update1.png "DiagnosticTools-Update1")  
  
-   **[Break イベント]** タイムラインは、デバッグ セッションでヒットしたブレークポイントにマークを付けます。 イベントをクリックして、 **[デバッガー]** の詳細リストで選択します。  
  
-   **[CPU 使用率]** グラフには、すべてのプロセッサ コアのデバッグ セッション中の CPU 使用率の変化が表示されます。  
  
-   **[デバッガー]** 詳細ペインの **[イベント]** の一覧には、各中断イベントの項目が含まれます。  
  
-   中断イベントの **[期間]** の列には、前のブレークポイントからそのイベントまでの経過時間が表示されます。  
  
## <a name="turn-perftips-on-or-off"></a>PerfTips をオンまたはオフにする  
 PerfTips を有効または無効にするには:  
  
1.  **[デバッグ]** メニューの **[オプション]** をクリックします。  
  
2.  **[デバッグ中に経過時間の PerfTip を表示する]** チェック ボックスをオンまたはオフにします。  
  
## <a name="turn-the-diagnostic-tools-window-on-or-off"></a>[診断ツール] ウィンドウをオンまたはオフにする  
 [診断ツール] ウィンドウを有効または無効にするには:  
  
1.  **[デバッグ]** メニューの **[オプション]** をクリックします。  
  
2.  **[デバッグ中に診断ツールを有効にする]** チェック ボックスをオンまたはオフにします。

## <a name="see-also"></a>関連項目
 [Visual Studio のプロファイル](../profiling/index.md)  
 [プロファイル ツールの概要](../profiling/profiling-feature-tour.md)
