---
title: .NET メモリのデータ ビュー | Microsoft Docs
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
- .NET memory profiling method views
- profiling tools,.NET memory profiling views
ms.assetid: 79184d8e-769b-4ace-be2b-521147772081
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7a3734552871d171ff592640f131b4257421a4b6
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2018
ms.locfileid: "49292280"
---
# <a name="net-memory-data-views"></a>.NET メモリのデータ ビュー
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ここでは、.NET メモリ プロファイル データが格納されるプロファイラー データ ファイルのビューとレポートに関するリファレンス情報を示します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [概要 ビュー](../profiling/summary-view-dotnet-memory-data.md)  
 最も多くのメモリを割り当てた関数と型が一覧で示されます。  
  
 [割り当て ビュー](../profiling/dotnet-memory-allocations-view.md)  
 プロファイリング実行で割り当てられた型、および型の割り当ての結果として生成されたコール ツリー (実行パス) が一覧で表示されます。  
  
 [オブジェクトの有効期間ビュー](../profiling/object-lifetime-view.md)  
 プロファイリング実行で割り当てられた型、およびその型のインスタンスの数、バイト単位のサイズ、ガベージ コレクション ジェネレーションが一覧で表示されます。  
  
 [コール ツリー ビュー - サンプリング](../profiling/call-tree-view-dotnet-memory-sampling-data.md)  
 プロファイリング実行の実行パスおよび関数のメモリ割り当てデータを表す階層ツリーが表示されます。  
  
 [モジュール ビュー - サンプリング](../profiling/modules-view-dotnet-memory-sampling-data.md)  
 .NET メモリ割り当てデータがモジュールごとに整理され、メモリの割り当て時に実行された関数、ソース コードの行、および命令が一覧で表示されます。  
  
 [呼び出し元/呼び出し先ビュー - .NET メモリ サンプリング データ](../profiling/caller-callee-view-dotnet-memory-sampling-data.md)  
 選択した関数のメモリ割り当てデータ、選択した関数を呼び出した関数、および選択した関数によって呼び出された関数が一覧で表示されます。  
  
 [関数ビュー - サンプリング](../profiling/functions-view-dotnet-memory-sampling-data.md)  
 プロファイリング実行での関数に対するメモリ割り当てデータが一覧で表示されます。  
  
 [行ビュー - サンプリング](../profiling/lines-view-dotnet-memory-sampling-data.md)  
 プロファイリング実行での関数のソース コード行に対するメモリ割り当てデータが一覧で表示されます。  
  
 [命令ポインター (IP) ビュー - サンプリング](../profiling/instruction-pointers-ips-view-dotnet-memory-sampling-data.md)  
 プロファイリング実行での関数の命令に対するメモリ割り当てデータが一覧で表示されます。  
  
 [コール ツリー ビュー - インストルメンテーション](../profiling/call-tree-view-dotnet-memory-instrumentation-data.md)  
 実行パス、メモリ割り当てデータ、およびプロファイリング実行でインストルメント化された関数の詳細なタイミング データを表す階層ツリーが表示されます。  
  
 [モジュール ビュー - インストルメンテーション](../profiling/modules-view-dotnet-memory-instrumentation-data.md)  
 プロファイル データがモジュール別に整理され、関数、メモリ割り当てデータ、およびモジュールの詳細なタイミング情報が一覧で表示されます。  
  
 [呼び出し元/呼び出し先ビュー - プロファイラーの .NET メモリ インストルメンテーション データ](../profiling/caller-callee-view-net-memory-instrumentation-data.md)  
 選択したインストルメント化された関数のメモリ割り当てデータおよび詳細なタイミング情報、選択した関数を呼び出した関数、および選択した関数によって呼び出された関数が一覧で表示されます。  
  
 [関数ビュー - インストルメンテーション](../profiling/functions-view-dotnet-memory-instrumentation-data.md)  
 プロファイリング実行でのインストルメント化された関数に対するメモリ割り当てデータが一覧で表示されます。  
  
## <a name="reference"></a>参照  
 [関数の詳細ビュー](../profiling/function-details-view.md)  
 選択した関数と、選択した関数を呼び出した関数および選択した関数によって呼び出された関数の関係がグラフィカルな図で表示されます。  
  
 [プロセス ビュー](../profiling/process-view.md)  
 プロセスおよびスレッドの開始時刻と終了時刻が一覧表示されます。  
  
 [マーク ビュー](../profiling/marks-view.md)  
 プロファイル データ ファイルに挿入された ETW およびサンプリング イベントが一覧表示されます。  
  
## <a name="related-sections"></a>関連項目  
 [サンプリング メソッドのデータ ビュー](../profiling/profiler-sampling-method-data-views.md)  
 サンプリング メソッドを使用して生成されたプロファイラー データ ファイルのビューとレポートに関するリファレンス情報。  
  
 [インストルメンテーション メソッドのデータ ビュー](../profiling/instrumentation-method-data-views.md)  
 インストルメンテーション メソッドを使用して生成されたプロファイラー データ ファイルのビューとレポートに関するリファレンス情報。



