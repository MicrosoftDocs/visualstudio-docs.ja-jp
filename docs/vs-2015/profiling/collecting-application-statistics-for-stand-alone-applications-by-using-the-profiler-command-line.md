---
title: プロファイラーのコマンド ラインを使用したスタンドアロン アプリケーションのアプリケーション統計情報の収集 | Microsoft Docs
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
- sampling profiling method
- profilng tools,sampling method
ms.assetid: be2dbdd0-fc88-45f9-a1d5-bcb4f64e17ad
caps.latest.revision: 24
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9841911dbb1fc9bb97eb995534af3eaec73d10e9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51756959"
---
# <a name="collecting-application-statistics-for-stand-alone-applications-by-using-the-profiler-command-line"></a>プロファイラーのコマンド ラインを使用したスタンドアロン アプリケーションのアプリケーション統計情報の収集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このセクションでは、コマンド ラインからサンプリング メソッドを使用して、クライアント (スタンドアロン) アプリケーションのパフォーマンスの統計情報を収集する手順とオプションについて説明します。  
  
> [!NOTE]
>  Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 Windows ストア アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。  
  
## <a name="common-tasks"></a>一般的なタスク  
  
|タスク|関連コンテンツ|  
|----------|---------------------|  
|**プロファイリングを使用してアプリケーションを起動する**|-   [方法: スタンドアロン アプリケーションを起動し、アプリケーション統計情報を収集する](../profiling/how-to-launch-a-stand-alone-application-with-the-profiler-and-collect-application-statistics-by-using-the-command-line.md)|  
|**実行中の .NET Framework アプリケーションにプロファイラーをアタッチする**|-   [方法: .NET Framework のアプリケーションにプロファイラーをアタッチし、アプリケーションの統計情報を収集する](../profiling/how-to-attach-the-profiler-to-a-dotnet-framework-stand-alone-application-and-collect-application-statistics-by-using-the-command-line.md)|  
|**実行中の C/C++ アプリケーションにプロファイラーをアタッチする**|-   [方法: プロファイラーをネイティブ アプリケーションにアタッチし、アプリケーション統計情報を収集する](../profiling/how-to-attach-the-profiler-to-a-native-stand-alone-application-and-collect-application-statistics-by-using-the-command-line.md)|  
|**階層の相互作用データを追加する**|-   [階層相互作用データの収集](../profiling/adding-tier-interaction-data-from-the-command-line.md)|  
  
## <a name="related-tasks"></a>関連タスク  
  
### <a name="profiling-stand-alone-applications"></a>スタンドアロン アプリケーションのプロファイリング  
  
|タスク|関連コンテンツ|  
|----------|---------------------|  
|**アプリケーションをインストルメント化する**|-   [インストルメンテーションを使用した詳細なタイミング データの収集](../profiling/collecting-detailed-timing-data-for-a-stand-alone-application-by-using-the-profiler-command-line.md)|  
|**.NET のメモリ割り当てとガベージ コレクション データの収集**|-   [.NET Framework メモリ データの収集](../profiling/collecting-dotnet-framework-memory-data-for-stand-alone-applications-by-using-the-profiler-command-line.md)|  
|**リソース競合とスレッド実行データの収集**|-   [コンカレンシー データの収集](../profiling/collecting-concurrency-data-for-stand-alone-applications-by-using-the-profiler-command-line.md)|  
  
### <a name="profiling-by-using-the-sampling-method"></a>サンプリング方式を使用したプロファイリング  
  
|タスク|関連コンテンツ|  
|----------|---------------------|  
|**ASP.NET Web アプリケーションのプロファイリング**|-   [サンプリングを使用したアプリケーション統計情報の収集](../profiling/collecting-application-statistics-for-aspnet-web-applications-using-the-profiler-sampling-method-from-the-command-line.md)|  
|**サービスのプロファイリング**|-   [サンプリングを使用したアプリケーション統計情報の収集](../profiling/collecting-application-statistics-for-services-by-using-the-profiler-sampling-method.md)。 サンプリング メソッドを使用して Windows サービスからパフォーマンスの統計情報を収集する方法について説明します。|  
  
### <a name="analyzing-sampling-data-views-and-reports"></a>サンプリング データ ビューとレポートの分析  
 [サンプリング メソッドのデータ ビュー](../profiling/profiler-sampling-method-data-views.md)



