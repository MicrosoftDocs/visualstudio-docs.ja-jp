---
title: 'DA0026: 過剰なカーネル CPU 処理時間。 | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.rules.DA0026
- vs.performance.DA0026
- vs.performance.26
ms.assetid: 4cfc8a29-b29b-4a72-b386-03d8856fdf8a
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 9043b1dddcacc797c640252691d6bf393189cc4d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49876608"
---
# <a name="da0026-excessive-kernel-cpu-time-processing"></a>DA0026: 過剰なカーネル CPU 処理時間。

|||  
|-|-|  
|規則 ID|TODO|  
|カテゴリ|プロファイリング ツールの使用|  
|プロファイル方法|サンプリング|  
|メッセージ|比較的高いカーネル モード CPU 時間が計測されました。 SysCall サンプリングを有効にし、原因を調査することを検討してください。|  
|規則の種類|情報|  

 サンプリング、.NET メモリ、またはリソース競合メソッドを使用してプロファイリングを行うときは、この規則を呼び出すためのサンプルを少なくとも 10 個収集する必要があります。  

## <a name="cause"></a>原因  
 カーネル モードで実行された CPU 時間の割合が、ユーザー モードで費やされた時間数を超えました。 カーネル モードの実行時間が長い原因を判断するために、プロファイリングを再度実行し、システム コール (syscalls) の数をサンプリングすることを検討してください。  

## <a name="rule-description"></a>規則の説明  
 カーネル モードでの実行中にアプリケーションの処理時間が比較的長くなっている場合は、さらに調査が必要になることがあります。 ユーザー モードのアプリケーションは、I/O 操作の実行、スレッドまたはプロセスの同期プリミティブの待機、またはシステム コールを実行するために、カーネル モードに遷移します。 システム コールに基づいてサンプルの呼び出し履歴を収集するオプションを選択する際に、アプリケーションが実行するシステム コールの種類とそのシステム コールを処理する関数を調べることができます。  

## <a name="how-to-fix-violations"></a>違反の修正方法  
 アプリケーションが実行するシステム コールを調べるには、プロファイルを再度実行し、システム コールに基づいてサンプルを収集するオプションを選択します。 IDE 内でプロファイリング ツールを実行する場合の詳細については、「[方法 : サンプリング イベントを選択する](../profiling/how-to-choose-sampling-events.md)」を参照してください。 コマンド ラインからプロファイル ツールを実行する場合の詳細については、コマンド ライン プロファイル ツール リファレンスの記事、「[VSPerfCmd](../profiling/vsperfcmd.md)」の「**サンプリング間隔オプション**」のセクションを参照してください。