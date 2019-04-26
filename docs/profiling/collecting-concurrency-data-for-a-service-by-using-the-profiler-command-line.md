---
title: プロファイラーのコマンド ラインを使用したサービスのコンカレンシー データの収集 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 275aacba-b2af-4d34-8931-ee30d777a256
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5df8fa1b0e0d9c76595c29958641de628e5e8b78
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440220"
---
# <a name="collect-concurrency-data-for-a-service-by-using-the-profiler-command-line"></a>プロファイラーのコマンド ラインを使用したサービスのコンカレンシー データの収集
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイリング ツールのコンカレンシー メソッドを使用すると、リソース競合データとスレッド アクティビティ データを収集し、CPU 使用率、スレッド競合、スレッドの移行、同期の遅延、重複 I/O の領域などのシステム イベントを表示できます。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。

## <a name="common-tasks"></a>一般的なタスク

|タスク|関連するコンテンツ|
|----------|---------------------|
|**実行中の .NET サービスにアタッチする**|-   [方法: プロファイラーを .NET サービスにアタッチし、コンカレンシー データを収集する](../profiling/how-to-attach-the-profiler-to-a-dotnet-service-to-collect-concurrency-data-by-using-the-command-line.md)|
|**階層の相互作用データを追加する**|-   [階層相互作用データを収集する](../profiling/adding-tier-interaction-data-from-the-command-line.md)|
|**実行中の C/C++ サービスにアタッチする**|-   [方法: プロファイラーをネイティブ サービスにアタッチし、コンカレンシー データを収集する](../profiling/how-to-attach-the-profiler-to-a-native-service-to-collect-concurrency-data-by-using-the-command-line.md)|

## <a name="related-tasks"></a>関連するタスク

### <a name="profile-windows-services"></a>Windows サービスのプロファイリング

|タスク|関連するコンテンツ|
|----------|---------------------|
|**サンプリング メソッドを使用したプロファイリング**|-   [サンプリングを使用したアプリケーション統計情報の収集](../profiling/collecting-application-statistics-for-services-by-using-the-profiler-sampling-method.md)|
|**インストルメンテーション方式を使用したプロファイリング**|-   [インストルメンテーションを使用した詳細なタイミング データの収集](../profiling/collecting-detailed-timing-data-for-services-by-using-the-instrumentation-method.md)|
|**.NET のメモリ割り当てとガベージ コレクションのプロファイリング**|-   [.NET メモリ データの収集](../profiling/collecting-memory-data-from-dotnet-framework-services-by-using-the-profiler-command-line.md)|

### <a name="profile-concurrency-data"></a>コンカレンシー データのプロファイリング

|タスク|関連するコンテンツ|
|----------|---------------------|
|**スタンドアロン アプリケーションのプロファイリング**|-   [コンカレンシー データの収集](../profiling/collecting-concurrency-data-for-stand-alone-applications.md)|
|**ASP.NET Web アプリケーションのプロファイリング**|-   [コンカレンシー データの収集](../profiling/collecting-concurrency-data-for-an-aspnet-web-application.md)|

### <a name="analyze-concurrency-data-views-and-reports"></a>コンカレンシー データ ビューとレポートの分析
- [リソース競合データのビュー](../profiling/resource-contention-data-views.md)

- [コンカレンシー ビジュアライザー](../profiling/concurrency-visualizer.md)

## <a name="reference"></a>関連項目
- [コマンド ライン プロファイリング ツール リファレンス](../profiling/command-line-profiling-tools-reference.md)