---
title: インストルメンテーションを使用した詳細なタイミング データの収集 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools,instrumentation method
- instrumentation profiling method
ms.assetid: e9deb370-c459-45ac-84d3-14d646590d05
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c129ddf016e02fe6c29d5cf63fe57ba07fbd4e95
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60087977"
---
# <a name="collecting-detailed-timing-data-by-using-instrumentation"></a>インストルメンテーションを使用した詳細なタイミング データの収集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロファイリング ツールのインストルメンテーション メソッド (方式) では、モジュールのコピーにプロファイリング コードが挿入されます。 このコードでは、プロファイリングの実行中に、モジュール内の各関数の開始、終了、および関数の呼び出しをそれぞれ記録します。 このインストルメンテーション メソッドは、コード セクションに関する詳細なタイミング情報を収集し、アプリケーションのパフォーマンスに対する入出力操作の影響を理解するために役立ちます。  
  
 インストルメンテーション メソッドは、次のいずれかの手順を使用して指定できます。  
  
- プロファイリング ウィザードの最初のページで **[インストルメンテーション]** を選択します。  
  
- **パフォーマンス エクスプローラー** のツールバーで、 **[メソッド]** 一覧の **[インストルメンテーション]** をクリックします。  
  
- パフォーマンス セッションの [プロパティ] ダイアログ ボックスの **[全般]** ページで、 **[インストルメンテーション]** をクリックします。  
  
## <a name="common-tasks"></a>よく使う機能  
 追加のオプションを、パフォーマンス セッションの [ _パフォーマンス セッション]_**[プロパティ ページ]** ダイアログ ボックスで指定できます。 このダイアログ ボックスを開くには:  
  
- **パフォーマンス エクスプローラー**で、パフォーマンス セッション名を右クリックして **[プロパティ]** をクリックします。  
  
  次の表の各タスクでは、インストルメンテーション メソッドを使用してプロファイリングを実行する際に、[ _パフォーマンス セッション]_**[プロパティ ページ]** ダイアログ ボックスで指定できるオプションについて説明しています。  
  
|タスク|関連するコンテンツ|  
|----------|---------------------|  
|**[全般]** ページで、.NET のメモリ割り当ておよび有効期間データを追加し、生成されるプロファイリング データ (.vsp) ファイルの名前付けの詳細を指定します。|-   [.NET メモリの割り当ておよび有効期間データの収集](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)<br />-   [方法: パフォーマンス データ ファイル名のオプションを設定する](../profiling/how-to-set-performance-data-file-name-options.md)|  
|ソリューション内に複数の .exe プロジェクトがある場合は、 **[起動]** ページで、開始するアプリケーションおよび開始順序を指定します。|-   [方法: 開始するバイナリを指定する](../profiling/how-to-specify-the-binary-to-start.md)|  
|**[バイナリ]** ページで、モジュールのインストルメント化されたコピーの場所を指定します。 既定では、元のバイナリはバックアップ フォルダーに移動されます。|-   [方法: インストルメント化されたバイナリの再配置](../profiling/how-to-relocate-instrumented-binaries.md)|  
|**[階層の相互作用]** ページで、プロファイリング実行に ADO.NET 呼び出しデータを追加します。|-   [階層相互作用データの収集](../profiling/collecting-tier-interaction-data.md)|  
|**[インストルメンテーション]** ページで、プロファイリングのオーバーヘッドを低減するために小規模関数を除外し、ASP.NET Web ページで JavaScript コードをプロファイルし、インストルメンテーション処理の前と後にコマンド プロンプトで実行するコマンドを指定します。|-   [方法: インストルメンテーションで短い関数を除外または含める](../profiling/how-to-exclude-or-include-short-functions-from-instrumentation.md)<br />-   [方法: Web ページ内の JavaScript コードをプロファイリングする](../profiling/how-to-profile-javascript-code-in-web-pages.md)<br />-   [方法: インストルメント前のコマンドおよびインストルメント後のコマンドを指定する](../profiling/how-to-specify-pre-and-post-instrument-commands.md)|  
|**[CPU カウンター]** ページで、プロファイリング データを追加するプロセッサのパフォーマンス カウンターを 1 つ以上指定します。|-   [方法: CPU カウンター データを収集する](../profiling/how-to-collect-cpu-counter-data.md)|  
|**[Windows イベント]** ページで、サンプリング データと共に収集する 1 つ以上の ETW (Windows イベント トレーシング) イベントを選択します。|-   [方法: ETW (Event Tracing for Windows) データを収集する](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md)|  
|**[Windows カウンター]** ページで、プロファイリング データをマークとして追加するオペレーティング システムのパフォーマンス カウンターを 1 つ以上指定します。|-   [方法: Windows カウンター データを収集する](../profiling/how-to-collect-windows-counter-data.md)|  
|**[詳細]** ページで、VSInstr インストルメンテーション プログラムに渡す追加のオプションをすべて指定します (特定の関数を含めるオプションや特定の関数を除外するオプションなど)。|-   [方法: 追加のインストルメンテーション オプションを指定する](../profiling/how-to-specify-additional-instrumentation-options.md)<br />-   [方法: インストルメンテーションを特定の関数に制限する](../profiling/how-to-limit-instrumentation-to-specific-functions.md)<br />-   [VSInstr](../profiling/vsinstr.md)|
