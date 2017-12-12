---
title: "コール ツリー ビュー - サンプリング データ | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sampling profiling method,Call Tree view
- Call Tree view
ms.assetid: 5c4e8ec3-d0d3-485a-93bd-9060df4eb739
caps.latest.revision: "16"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 82c34ef71777c42b2fa743817d731a66b2b8bee9
ms.sourcegitcommit: 26419ab0cccdc30d279c32d6a841758cfa903806
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2017
---
# <a name="call-tree-view---sampling-data"></a>コール ツリー ビュー - サンプリング データ
コール ツリー ビューには、プロファイル対象アプリケーションで走査された関数の実行パスが表示されます。  
  
> [!NOTE]
>  Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 ｢[Performance Tools on Windows 8 and Windows Server 2012 applications](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md) (Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール)」をご覧ください。  
  
 ツリーのルートは、アプリケーションまたはコンポーネントへのエントリ ポイントです。 各関数ノードは、呼び出したすべての関数と、その関数呼び出しに関するパフォーマンス データを表示します。  
  
 コール ツリー ビュー内の値は、コール ツリー内の親関数から呼び出された関数のインスタンスに対応します。 割合の値を計算するには、関数インスタンスの値と、プロファイル実行のサンプルの総数を比較します。  
  
## <a name="highlighting-the-execution-hot-path"></a>実行ホット パスの強調表示  
 コール ツリー ビューでは、最も頻繁にサンプリングされたプロセスまたは関数の実行パスを展開および強調表示することもできます。 最もアクティブなパスを表示するには、プロセスまたは関数を右クリックし、**[ホット パスの展開]** をクリックします。  
  
## <a name="setting-the-call-tree-root-node"></a>コール ツリーのルート ノードの設定  
 プロファイル実行の各プロセスは、ルート ノードとして表示されます。 コール ツリー ビューの開始ノードを設定するには、開始ノードとして設定するノードを右クリックし、**[ルートの設定]** をクリックします。  
  
 ルート ノードを設定すると、選択したノードのサブツリーを除く他のすべてのエントリはビューから除外されます。 ルート ノードを元のノードに戻すには、[コール ツリー] ウィンドウ内の任意の場所で右クリックし、**[ルートのリセット]** をクリックします。  
  
|列|説明|  
|------------|-----------------|  
|**プロセス ID**|プロファイリング実行のプロセス ID (PID) です。|  
|**プロセス名**|プロセスの名前です。|  
|**モジュール名**|関数を含むモジュールの名前です。|  
|**モジュール パス**|関数を含むモジュールのパスです。|  
|**ソース ファイル**|この関数の定義を含むソース ファイルです。|  
|**関数名**|関数の完全修飾名です。|  
|**関数行番号**|ソース ファイルでのこの関数の開始行番号です。|  
|**関数アドレス**|関数のアドレス。|  
|**レベル**|コール ツリーにおけるこの関数の深度。 [VSPerfReport](../profiling/vsperfreport.md) コマンド ライン レポートでのみ有効です。|  
|**サンプル数 (関数のみ)**|この関数がコール ツリー内の親関数から呼び出されたときに、この関数で収集されたサンプルの数。 この数値には、この関数によって呼び出された関数で収集されたサンプルは含まれません。|  
|**サンプル % (関数のみ)**|この関数がコール ツリーの親関数から呼び出されたときの、プロファイル実行のすべてのサンプル数に対する、この関数 (子関数を含まない) のサンプル数の割合。|  
|**サンプル数 (子を含む)**|この関数がコール ツリー内の親関数から呼び出されたときに、この関数で収集されたサンプルの数。 この数値には、この関数によって呼び出された関数で収集されたサンプルが含まれます。|  
|**サンプル % (子を含む)**|この関数がコール ツリーの親関数から呼び出されたときの、プロファイル実行のすべてのサンプル数に対する、この関数およびその子関数のサンプル数の割合。|  
  
## <a name="see-also"></a>関連項目  
 [方法: レポート ビューの列をカスタマイズする](../profiling/how-to-customize-report-view-columns.md)   
 [コール ツリー ビュー - プロファイラー サンプリング データ](../profiling/call-tree-view-sampling-data.md)   
 [コール ツリー ビュー - サンプリング](../profiling/call-tree-view-dotnet-memory-sampling-data.md)   
 [コール ツリー ビュー - インストルメンテーション](../profiling/call-tree-view-dotnet-memory-instrumentation-data.md)   
 [コール ツリー ビュー](../profiling/call-tree-view-instrumentation-data.md)