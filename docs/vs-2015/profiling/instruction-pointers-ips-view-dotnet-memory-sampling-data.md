---
title: 命令ポインター (IP) ビュー - .NET メモリ サンプリング データ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Instruction Pointers view
ms.assetid: 7d91cc14-e8e9-4ebb-b14f-b9f0da770508
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: dd06bc09114785c4359d05e3cda70c3ce7646c9e
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2019
ms.locfileid: "54804248"
---
# <a name="instruction-pointers-ips-view---net-memory-sampling-data"></a>命令ポインター (IP) ビュー - .NET メモリ サンプリング データ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

サンプリング メソッドを使用して収集された .NET メモリの割り当てプロファイル データの IP ビューには、プロファイル実行中にメモリを割り当てたアセンブリ命令が一覧表示されます。 ビューの列には、割り当てのサイズと数も一覧表示されます。  
  
 排他的な値のみが一覧表示されます。  
  
|Column|説明|  
|------------|-----------------|  
|**プロセス ID**|プロファイリング実行のプロセス ID (PID) です。|  
|**プロセス名**|プロセスの名前です。|  
|**モジュール名**|命令を含むモジュールの名前。|  
|**モジュール パス**|命令を含むモジュールのパスです。|  
|**ソース ファイル**|命令を含むソース ファイルです。|  
|**関数名**|関数の名前。|  
|**関数行番号**|ソース ファイルでのこの関数の開始行番号です。|  
|**関数アドレス**|関数の開始アドレスです。|  
|**ソース開始行**|割り当てが行われたソース ファイル内の開始行番号です。|  
|**ソース終了行**|割り当てが行われたソース ファイル内の終了行番号です。|  
|**ソース開始文字番号**|割り当てが行われたソース ファイル行内の開始文字のオフセットです。|  
|**ソース終了文字番号**|割り当てが行われたソース ファイル行内の終了文字のオフセットです。|  
|**命令ポインター アドレス**|命令のアドレス。|  
|**割り当て数 (関数のみ)**|命令によって作成されたオブジェクトの総数。|  
|**割り当て % (関数のみ)**|プロファイル実行中に作成されたすべてのオブジェクトのうち、命令によって割り当てられたオブジェクトの割合。|  
|**割り当てバイト数 (関数のみ)**|プロファイル実行中に割り当てられ、命令によって割り当てられたメモリのバイト数。|  
|**割り当てバイト数 % (関数のみ)**|プロファイル実行中に割り当てられたメモリの総バイト数のうち、命令によって割り当てられたバイト数の割合。|  
  
## <a name="see-also"></a>関連項目  
 [命令ポインター (IP) ビュー](../profiling/instruction-pointers-ips-view-sampling-data.md)
