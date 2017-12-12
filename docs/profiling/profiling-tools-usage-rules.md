---
title: "プロファイリング ツールの使用に関する規則 | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: afa7db3b-8c1d-473a-81ac-24ede112a17f
caps.latest.revision: "9"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f2660586ce2757f2aa1b58c6c7b0e4dc36a700bc
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2017
---
# <a name="profiling-tools-usage-rules"></a>プロファイリング ツールの使用に関する規則
プロファイリング ツールの使用カテゴリのパフォーマンス規則は、プロファイラーを使用してデータを最も効率よく収集する方法に関するガイダンスを提供します。  
  
|||  
|-|-|  
|[DA0002: VSPerfCorProf.dll がありません](../profiling/da0002-vsperfcorprof-dll-is-missing.md)|コマンド ライン プロファイリングに、[!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] バイナリに関する不完全なデータが含まれている可能性があります。 正しい環境変数が設定されていないことが原因である場合があります。|  
|[DA0003: カーネル サンプルが多数存在します](../profiling/da0003-many-kernel-samples.md)|対象バイナリの実行と無関係なプロファイリング サンプルが多数生成され、記録されました。 より正確なデータを収集するには、インストルメンテーション メソッドの使用をご検討ください。|  
|[DA0004: プロセッサ使用率が高くなっています](../profiling/da0004-high-processor-usage.md)|プロファイル データは、プロファイリングの実行中にプロセッサが常にビジー状態であったことを示しています。 より正確なデータを収集するには、サンプリング メソッドの使用をご検討ください。|  
|[DA0008: 少数のサンプルしか収集されていません](../profiling/da0008-few-samples-collected.md)|プロファイリングの実行時に収集されたサンプルの数が、統計的に有意な数には足りませんでした。 もう一度プロファイリングを実行し、これまでよりも長い時間アプリケーションを実行することをご検討ください。 インストルメンテーション メソッドを使用してデータを収集することも検討できます。|  
|[DA0026: 過剰なカーネル CPU 処理時間。](../profiling/da0026-excessive-kernel-cpu-time-processing.md)|プロセッサのカーネル モードで、プロファイリングの実行に非常に時間がかかりました。 サンプリングで、時間をメトリックとして使用するのではなく、システム コールをメトリックとして使用することをご検討ください。|  
|[DA0029: サポートされていない CLR バージョンです。](../profiling/da0029-unsupported-clr-version.md)|プロファイリングされるバイナリが、プロファイラーでサポートされないバージョンの [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] を使用しています。 プロファイラー レポートはシンボル名を解決できません。|  
|[DA0030: データベース プロジェクトの階層の相互作用の測定を収集します](../profiling/da0030-gather-tier-interaction-measurements-for-database-projects.md)|<xref:System.Data?displayProperty=fullName> 名前空間で多数のメソッドの呼び出しが収集されました。 データベース呼び出しに関するデータを含めるには、プロファイリングの実行時に階層相互作用データを収集することをご検討ください。|