---
title: プロファイラーのコマンド ラインを使用したスタンドアロン アプリケーションのコンカレンシー データの収集 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- concurrency profiling method
- profiling tools,concurrency method
ms.assetid: 0a2c6d8a-50b3-48aa-b617-9137b049d21e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c02802fa9a32c3ae973108ed2622dc0aa9e0f262
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62960345"
---
# <a name="collect-concurrency-data-for-stand-alone-applications-by-using-the-profiler-command-line"></a>プロファイラーのコマンド ラインを使用したスタンドアロン アプリケーションのコンカレンシー データの収集
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイリング ツールのコンカレンシー メソッドを使用すると、リソース競合データとスレッド アクティビティ データを収集し、CPU 使用率、スレッド競合、スレッドの移行、同期の遅延、重複 I/O の領域などのシステム イベントを表示できます。

## <a name="common-tasks"></a>一般的なタスク

|タスク|関連コンテンツ|
|----------|---------------------|
|**.NET Framework アプリケーションとプロファイルコンカレンシー データの起動**|-   [方法: .NET Framework アプリケーションを起動し、コンカレンシー データを収集する](../profiling/how-to-launch-a-stand-alone-dotnet-framework-app-to-collect-concurrency-data.md)|
|**C/C++ アプリケーションとプロファイル コンカレンシー データの起動**|-   [方法: ネイティブ アプリケーションを起動し、コンカレンシー データを収集する](../profiling/how-to-launch-a-stand-alone-native-application-to-collect-concurrency-data.md)|
|**実行中の .NET Framework アプリケーションにプロファイラーをアタッチする**|-   [方法: プロファイラーを .NET Framework アプリケーションにアタッチし、コンカレンシー データを収集する](../profiling/how-to-attach-the-profiler-to-a-dotnet-app-and-collect-concurrency-data.md)|
|**実行中の C/C++ アプリケーションにプロファイラーをアタッチする**|-   [方法: プロファイラーをネイティブ アプリケーションにアタッチし、コンカレンシー データを収集する](../profiling/how-to-attach-the-profiler-to-a-native-app-and-collect-concurrency-data.md)|

## <a name="related-tasks"></a>関連するタスク

### <a name="profile-stand-alone-applications"></a>スタンドアロン アプリケーションのプロファイリング

|タスク|関連コンテンツ|
|----------|---------------------|
|**サンプリング メソッドを使用したプロファイリング**|-   [サンプリングを使用したアプリケーション統計情報の収集](../profiling/collecting-application-statistics-for-stand-alone-applications.md)|
|**インストルメンテーション方式を使用したプロファイリング**|-   [インストルメンテーションを使用した詳細なタイミング データの収集](../profiling/collecting-detailed-timing-data-for-a-stand-alone-application.md)|
|**.NET のメモリ割り当てとガベージ コレクションのプロファイリング**|-   [.NET Framework メモリ データの収集](../profiling/collecting-dotnet-framework-memory-data-for-stand-alone-applications.md)|
|**階層の相互作用データを追加する**|-   [階層相互作用データを収集する](../profiling/adding-tier-interaction-data-from-the-command-line.md)|

### <a name="profile-concurrency-issues"></a>コンカレンシーの問題のプロファイリング

|タスク|関連コンテンツ|
|----------|---------------------|
|**ASP.NET アプリケーションのプロファイリング**|-   [コンカレンシー データの収集](../profiling/collecting-concurrency-data-for-an-aspnet-web-application.md)|
|**サービスのプロファイリング**|-   [コンカレンシー データの収集](../profiling/collecting-concurrency-data-for-a-service-by-using-the-profiler-command-line.md)|

### <a name="analyze-concurrency-data-views-and-reports"></a>コンカレンシー データ ビューとレポートの分析
- [リソース競合データのビュー](../profiling/resource-contention-data-views.md)

- [コンカレンシー ビジュアライザー](../profiling/concurrency-visualizer.md)

## <a name="reference"></a>関連項目
- [コマンド ライン プロファイリング ツール リファレンス](../profiling/command-line-profiling-tools-reference.md)