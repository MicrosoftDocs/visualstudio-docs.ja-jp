---
title: プロファイラーのコマンド ラインを使用したスタンドアロン アプリケーションのアプリケーション統計情報の収集 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- sampling profiling method
- profilng tools,sampling method
ms.assetid: be2dbdd0-fc88-45f9-a1d5-bcb4f64e17ad
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 951c65672f3b5aa6bb9555ace4622cfb60b04fc6
ms.sourcegitcommit: 209c2c068ff0975994ed892b62aa9b834a7f6077
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2018
---
# <a name="collect-application-statistics-for-stand-alone-applications-by-using-the-profiler-command-line"></a>プロファイラーのコマンド ラインを使用したスタンドアロン アプリケーションのアプリケーション統計情報の収集
このセクションでは、コマンド ラインからサンプリング メソッドを使用して、クライアント (スタンドアロン) アプリケーションのパフォーマンスの統計情報を収集する手順とオプションについて説明します。  
  
> [!NOTE]
>  Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。  
  
## <a name="common-tasks"></a>一般的なタスク  
  
|タスク|関連コンテンツ|  
|----------|---------------------|  
|**プロファイリングを使用してアプリケーションを起動する**|-   [方法: スタンドアロン アプリケーションを起動し、アプリケーション統計情報を収集する](../profiling/how-to-launch-a-stand-alone-application-with-the-profiler-and-collect-application-statistics-by-using-the-command-line.md)|  
|**実行中の .NET Framework アプリケーションにプロファイラーをアタッチする**|-   [方法: .NET Framework のアプリケーションにプロファイラーをアタッチし、アプリケーションの統計情報を収集する](../profiling/how-to-attach-the-profiler-to-a-dotnet-app-and-collect-application-statistics.md)|  
|**実行中の C/C++ アプリケーションにプロファイラーをアタッチする**|-   [方法: プロファイラーをネイティブ アプリケーションにアタッチし、アプリケーション統計情報を収集する](../profiling/how-to-attach-the-profiler-to-a-native-stand-alone-application-and-collect-application-statistics-by-using-the-command-line.md)|  
|**階層の相互作用データを追加する**|-   [階層相互作用データの収集](../profiling/adding-tier-interaction-data-from-the-command-line.md)|  
  
## <a name="related-tasks"></a>関連するタスク  
  
### <a name="profile-stand-alone-applications"></a>スタンドアロン アプリケーションのプロファイリング  
  
|タスク|関連コンテンツ|  
|----------|---------------------|  
|**アプリケーションをインストルメント化する**|-   [インストルメンテーションを使用した詳細なタイミング データの収集](../profiling/collecting-detailed-timing-data-for-a-stand-alone-application.md)|  
|**.NET のメモリ割り当てとガベージ コレクション データの収集**|-   [.NET Framework メモリ データの収集](../profiling/collecting-dotnet-framework-memory-data-for-stand-alone-applications.md)|  
|**リソース競合とスレッド実行データの収集**|-   [同時実行データの収集](../profiling/collecting-concurrency-data-for-stand-alone-applications.md)|  
  
### <a name="profile-by-using-the-sampling-method"></a>サンプリング メソッドを使用したプロファイリング  
  
|タスク|関連コンテンツ|  
|----------|---------------------|  
|**ASP.NET Web アプリケーションのプロファイリング**|-   [サンプリングを使用したアプリケーション統計情報の収集](../profiling/collecting-application-statistics-for-aspnet-using-the-profiler-sampling-method.md)|  
|**サービスのプロファイリング**|-   [サンプリングを使用したアプリケーション統計情報の収集](../profiling/collecting-application-statistics-for-services-by-using-the-profiler-sampling-method.md) サンプリング メソッドを使用して Windows サービスからパフォーマンスの統計情報を収集する方法について説明します。|  
  
### <a name="analyze-sampling-data-views-and-reports"></a>サンプリング データ ビューとレポートの分析  
 [サンプリング メソッドのデータ ビュー](../profiling/profiler-sampling-method-data-views.md)

