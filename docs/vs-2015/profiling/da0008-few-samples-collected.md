---
title: DA0008:少数のサンプルしか収集されていません | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.rules.DATooFewSamples
- vs.performance.8
- vs.performance.DA0008
- vs.performance.rules.DA0008
ms.assetid: 8a5b78aa-7b3d-476c-a47d-abfaff3fae7c
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 03fd9b6fd794320faf76119616900b79d5bf4333
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68187854"
---
# <a name="da0008-few-samples-collected"></a>DA0008:少数のサンプルしか収集されていません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

規則 Id |DA0008 |  
|カテゴリ |プロファイリング ツールの使用 |  
|プロファイル方法 |サンプリング |  
|メッセージ |サンプルをいくつかのみが収集されませんでした。 収集されるサンプル数を増やすには、実行時間を長くするか、サンプリング速度を上げてください。|  
|規則の種類 |情報 |  
  
## <a name="cause"></a>原因  
 プロファイリング実行で少数のサンプルしか収集されませんでした。  
  
## <a name="rule-description"></a>規則の説明  
 サンプリング メソッドを使用するときは、実際のプログラムの動作を表すようなデータを確実に得るために、統計的に有意な数のサンプルを収集する必要があります。 サンプリング エラーを最小限に抑えるには、プログラム命令の実行動作のサンプルを少なくとも 1000 個収集するようにしてください。 十分なサンプルを収集しない場合、プロファイル データを分析したときに誤った結果が得られる可能性があります。  
  
## <a name="how-to-fix-violations"></a>違反の修正方法  
 統計的に有意な結果を得るために、プロファイリングするアプリケーションの実行時間を長くするか、サンプリング速度を上げることを検討してください。 Visual Studio IDE でサンプル速度を変更する方法については、「[方法:サンプリング イベントを選択](../profiling/how-to-choose-sampling-events.md)します。 コマンド ラインからプロファイリング ツールを使用してサンプル速度を変更する方法の詳細については、「[VSPerfCmd](../profiling/vsperfcmd.md)」リファレンスの「[Timer](../profiling/timer.md)」を参照してください。
