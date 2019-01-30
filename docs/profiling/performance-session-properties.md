---
title: パフォーマンス セッションのプロパティ | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools,properties
- property pages,Profiling Tools
- performance tools, performance session properties
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 76e2d85cd1417d7700841b3d035255317f2581a0
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "54959422"
---
# <a name="performance-session-properties"></a>パフォーマンス セッションのプロパティ

**パフォーマンス セッション**により、アプリケーションのプロファイリング方法を決定する設定を構成できます。 また、プロファイル セッションに関するレポートが生成されて格納されます。

**パフォーマンス セッション**を作成するには、**パフォーマンス ウィザード**を実行するか、または手動でセッションを作成します。 **パフォーマンス セッション**が作成されると、**パフォーマンス セッション**は**パフォーマンス エクスプローラー**に表示されます。

**パフォーマンス セッション**のプロパティを表示するには、**パフォーマンス エクスプローラー**でセッション名を選択し、右クリックして **[プロパティ]** を選択します。

パフォーマンス セッションには、次のプロパティ ページがあります。

## <a name="general"></a>全般

この設定では、プロファイリング メソッドを選択したり、.NET オブジェクト コレクションや有効期間データを追加したり、既定のレポートの場所や名前付け規則を指定したりできます。

詳細については次を参照してください:

[方法: 収集方法を選択する](../profiling/how-to-choose-collection-methods.md)

[.NET メモリの割り当てと有効期間データの収集](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)

 [方法: パフォーマンス データ ファイル名のオプションを設定する](../profiling/how-to-set-performance-data-file-name-options.md)

## <a name="launch"></a>Launch

この設定では、バイナリの一覧から選択したり、バイナリの開始順序を指定したりできます。

詳細については、「[方法 :開始するバイナリを指定する](../profiling/how-to-specify-the-binary-to-start.md)」を参照してください

## <a name="sampling"></a>サンプリング

この設定では、プロファイリング メソッドとしてサンプリングを使用するときのサンプル イベントとサンプリング間隔を選択できます。 サンプル イベントは、指定した間隔でプロファイリング データを収集するために使用します。 たとえば、サンプル イベントとしてクロック サイクルを選択し、サンプリング間隔を 10,000,000 に設定した場合、プロファイリング データは 1,000 万クロック サイクルごとに収集されます。 次の 4 種類のサンプル イベントを使用できます。

- クロック サイクル - CPU バインドの問題
- ページ フォールト - メモリ関連の問題
- システム コール - I/O 関連の問題
- パフォーマンス カウンター - 低レベルのパフォーマンスの問題
- 使用できるパフォーマンス カウンターに基づいて、その他のサンプル イベントを指定できます

詳細については、「[方法 :サンプリング イベントを選択する](../profiling/how-to-choose-sampling-events.md)

## <a name="binary"></a>2 項
この設定では、インストルメント化されたバイナリを別の位置に再配置するかどうかを指定できます。 たとえば、*My.DLL* のプロファイリングを行っていて、インストルメント化されたバイナリを再配置しないことを選択した場合、*My.DLL* のバックアップ コピーが *My.Orig.DLL* という名前で作成されます。 その後、*My.DLL* にデータ収集用のプローブが挿入されて変更されます。 インストルメント化されたバイナリを再配置することにした場合、元のバイナリの名前は変更されず、インストルメント化されたバイナリは指定された位置にコピーされ、インストルメンテーション時に使用されます。

詳細については、「[方法 :開始するバイナリを指定する](../profiling/how-to-specify-the-binary-to-start.md)」を参照してください

## <a name="tier-interactions"></a>階層の相互作用

詳細については、「[階層相互作用データの収集](../profiling/collecting-tier-interaction-data.md)」を参照してください。

## <a name="instrumentation"></a>インストルメンテーション

この設定では、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web ページで JScript コードのパフォーマンス データを収集し、インストルメンテーション プロセスの前後に発生させる**インストルメント前の**イベントと**インストルメント後の**イベントを指定できます。

詳細については次を参照してください:

[方法: Web ページ内の JavaScript コードをプロファイリングする](../profiling/how-to-profile-javascript-code-in-web-pages.md)

[方法: インストルメント前のコマンドおよびインストルメント後のコマンドを指定する](../profiling/how-to-specify-pre-and-post-instrument-commands.md)

## <a name="cpu-counters"></a>CPU カウンター

この設定では、インストルメンテーション プロファイリング メソッドを使用しているときの CPU パフォーマンス カウンターに関するデータを収集できます。 汎用性のあるパフォーマンス カウンターは、CPU の設計やメーカーにかかわらず使用できます。 プラットフォーム イベントは、CPU の設計やメーカーに固有です。 オンチップ パフォーマンス カウンターの詳細については、該当するプロセッサのマニュアルを参照してください。

詳細については、「[方法 :CPU カウンター データを収集する](../profiling/how-to-collect-cpu-counter-data.md)

## <a name="windows-events"></a>Windows イベント

プロファイリング中は、イベント トレース プロバイダーからデータを収集できます。 データは、*VSPerfReport.exe* コマンド ライン ツールの `/calltrace` オプションを使用して表示できます。 Windows イベント トレーシング (ETW) の詳細については、[イベント トレーシング](http://go.microsoft.com/fwlink/?linkid=90752)に関する記事を参照してください。

詳細については次を参照してください:

[方法: ETW (Event Tracing for Windows) データを収集する](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md)

[VSPerfReport](../profiling/vsperfreport.md)

## <a name="windows-counters"></a>Windows カウンター

このオプションを使用すると、Windows パフォーマンス モニターのカウンターからデータを収集できます。 このデータを収集するには、**[Windows カウンターの収集]** チェック ボックスをオンにします。 収集の間隔は、**[収集間隔]** ボックスで設定します。 **[カウンター カテゴリ]** と **[インスタンス]** も使用できます。 既定の Windows パフォーマンス モニターのカウンターの一部が有効になります。

 詳細については、「[方法 :Windows カウンター データを収集する](../profiling/how-to-collect-windows-counter-data.md)」を参照してください。

## <a name="advanced"></a>詳細設定

この設定では、[VSInstr](../profiling/vsinstr.md) コマンド ライン プロファイリング ツールの 1 つ以上のオプションを指定して、インストルメンテーション プロセスにオプションを追加できます。 また、アプリケーションが複数バージョンの共通ランタイムを使用している場合に、プロファイリングする共通ランタイムのバージョンを指定できます。

詳細については次を参照してください:

[方法: .NET Framework ランタイムを指定する](../profiling/how-to-specify-the-dotnet-framework-runtime.md)

[方法: 追加のインストルメンテーション オプションを指定する](../profiling/how-to-specify-additional-instrumentation-options.md)

## <a name="see-also"></a>関連項目

[概要](../profiling/overviews-performance-tools.md)  
[パフォーマンス セッションの構成](../profiling/configuring-performance-sessions.md)  
[データ収集の制御](../profiling/controlling-data-collection.md)