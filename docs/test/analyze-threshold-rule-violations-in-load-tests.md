---
title: Visual Studio でロード テストのしきい値規則違反を分析する
ms.date: 10/19/2016
ms.topic: conceptual
f1_keywords:
- vs.test.load.monitor.threshholdresult
helpviewer_keywords:
- load tests, thresholds
- threshold violations
- threshold counts
- load tests, threshold violations
- load test results, analyzing threshold violations
- thresholds in load tests
ms.assetid: 969ed346-cf2e-4d48-82b3-edb3e075e1c0
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 41837a9ff3d67f2d712352115bcb6581580b32a3
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49812999"
---
# <a name="analyzing-threshold-rule-violations-in-load-tests-using-the-load-test-analyzer"></a>ロード テスト アナライザーを使用したロード テストのしきい値規則違反の分析

しきい値規則は、特定のパフォーマンス カウンターに関連付けられます。違反とは、パフォーマンス カウンターが設定値を上回るか下回ったことを示します。 ロード テストの実行では、あらかじめ設定したしきい値規則に対する違反を分析できます。

違反が発生すると、**[しきい値の違反です]** というハイパーリンクが**ロード テスト アナライザー**のステータス バーに表示され、発生した違反の数が示されます。 このハイパーリンクを選択すると、しきい値違反テーブルが表示されます。 しきい値違反は、**[カウンター]** ウィンドウやグラフ上でも表示できます。

## <a name="view-threshold-violations-in-the-table"></a>しきい値違反テーブルの表示

 しきい値違反テーブルには、最初の 1,000 個の違反が表示されます。 次の表は、表示される列を示しています。

|Column|説明|既定で表示|
|-|-|-|
|時刻|ロード テスト中に違反が発生した時刻。|[はい]|
|コンピューター|違反が発生した、テスト中のコンピューター名。 **注:** この情報は、リモート テスト マシン群でロード テストを実行する場合に重要です。|[はい]|
|カテゴリ|違反が発生したパフォーマンス カウンターのカテゴリ。|[はい]|
|カウンター|違反が発生したパフォーマンス カウンターの名前。|[はい]|
|[インスタンス]|違反が発生したパフォーマンス カウンター インスタンス。|[はい]|
|メッセージ|しきい値違反について説明するメッセージ。 たとえば、**値 5 は重大なしきい値 0 を超えています**。|[はい]|

> [!NOTE]
> テーブルは、列ヘッダーを選択することによって並べ替えることができます。

 詳細については、[テーブル ビューでのロード テスト結果とエラーの分析](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)に関するページを参照してください。

## <a name="view-threshold-violations-in-the-counters-panel"></a>カウンター パネルでのしきい値違反の表示

 しきい値違反は、**[カウンター]** パネルで、ロード テストのパフォーマンス カウンターを一覧表示するツリーに表示できます。 **[カウンター]** パネルのアイコンがしきい値違反を通知します。 アイコンは以下のいずれかです。

 アイコンは以下のいずれかです。

 ![しきい値違反なし](../test/media/icon_ltest_1.gif) しきい値違反がない。

 ![最後の間隔における重大なしきい値違反](../test/media/icon_ltest_2.gif) 重大なしきい値違反が最後の間隔で発生した。

 ![以前の間隔における重大なしきい値違反](../test/media/icon_ltest_3.gif) 重大なしきい値違反が以前の間隔で発生した。

 ![最後の間隔における警告しきい値違反](../test/media/icon_ltest_4.gif) 警告しきい値違反が最後の間隔で発生した。

 ![以前の間隔における警告しきい値違反](../test/media/icon_ltest_5.gif) 警告しきい値違反が前の間隔で発生した。

 必要に応じて、しきい値違反をグラフに表示することもできます。 しきい値アイコンは、グラフ上のしきい値違反が発生したデータ ポイントの隣に表示されます。

 カウンター ツリーでは、しきい値違反を示すアイコンは、該当するカウンター ノードからルート ノードにまで反映されます。 これにより、ツリーが閉じていて表示されないカウンターでの違反も通知されます。

 詳細については、「[グラフ ビューおよびテーブル ビューでのカウンター パネルの使用](../test/counters-panel-in-load-test-analyzer.md)」を参照してください。

## <a name="view-threshold-violations-on-the-graph"></a>しきい値違反のグラフでの表示

 しきい値違反はグラフにも表示できます。 **[カウンター]** パネルの場合と同様に、しきい値違反はアイコンでグラフに表示されます。 アイコンは、グラフ上でしきい値違反が発生したデータ ポイントの隣に表示されます。 グラフに表示されていないカウンターでしきい値違反が発生した場合は、それを **[カウンター]** パネルからグラフにドラッグすることで、グラフに追加できます。

 詳細については、「[グラフ ビューでのロード テスト結果の分析](../test/analyze-load-test-results-in-the-graphs-view.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [ロード テストでのコンピューターのカウンター セットとしきい値規則の指定](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
- [ロード テストの結果の分析](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [テーブル ビューでのロード テスト結果とエラーの分析](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)