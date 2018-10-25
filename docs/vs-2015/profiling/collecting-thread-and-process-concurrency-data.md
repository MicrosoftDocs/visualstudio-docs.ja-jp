---
title: スレッドおよびプロセスのコンカレンシー データの収集 | Microsoft Docs
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
- concurrency profiling method
- Profiling Tools, concurrency method
ms.assetid: fa03d381-a9ee-408c-876d-05111e29225b
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2956d5f5ce4cf8f210466f7b7006a158eee6ce43
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49885058"
---
# <a name="collecting-thread-and-process-concurrency-data"></a>スレッドおよびプロセスのコンカレンシー データの収集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロファイリング ツールのコンカレンシー プロファイル メソッドを使用すると、プロファイリング対象のアプリケーションの機能がリソースへのアクセスを待機するすべての同期イベントに関する情報を含むリソース競合データを収集できます。  
  
 **必要条件**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]、 [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]、 [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
  コンカレンシー プロファイル メソッドは、次のいずれかの手順を使用して指定できます。  
  
- プロファイリング ウィザードの最初のページで **[コンカレンシー]** をクリックします  
  
- パフォーマンス セッションの [プロパティ] ダイアログ ボックスの **[全般]** ページで、**[コンカレンシー]** をクリックします。  
  
- **パフォーマンス エクスプローラー**のツールバーで、**[メソッド]** 一覧の **[コンカレンシー]** をクリックします。  
  
## <a name="common-tasks"></a>一般的なタスク  
 追加のオプションを、パフォーマンス セッションの [ _パフォーマンス セッション]_**[プロパティ ページ]** ダイアログ ボックスで指定できます。 このダイアログ ボックスを開くには:  
  
- **パフォーマンス エクスプローラー**で、パフォーマンス セッション名を右クリックして **[プロパティ]** をクリックします。  
  
  次の表の各タスクでは、コンカレンシー メソッドを使用してプロファイリングを実行する際に、_[パフォーマンス セッション]_**[プロパティ ページ]** ダイアログ ボックスで指定できるオプションについて説明しています。  
  
|タスク|関連するコンテンツ|  
|----------|---------------------|  
|**[全般]** ページで、生成されるプロファイリング データ (.vsp) ファイルの名前付けの詳細を指定します。|-   [方法: パフォーマンス データ ファイル名のオプションを設定する](../profiling/how-to-set-performance-data-file-name-options.md)|  
|コード ソリューション内に複数の .exe プロジェクトがある場合は、**[起動]** ページで、開始するアプリケーションを指定します。|-   [方法 : 開始するバイナリを指定する](../profiling/how-to-specify-the-binary-to-start.md)|  
|**[階層の相互作用]** ページで、プロファイリング実行に ADO.NET 呼び出しデータを追加します。|-   [階層相互作用データの収集](../profiling/collecting-tier-interaction-data.md)|  
|**[Windows カウンター]** ページで、プロファイリング データをマークとして追加するオペレーティング システムのパフォーマンス カウンターを 1 つ以上指定します。|-   [方法 : Windows カウンター データを収集する](../profiling/how-to-collect-windows-counter-data.md)|  
|アプリケーション モジュールで複数のバージョンを使用する場合は、**[詳細]** ページで、プロファイリングする .NET Framework ランタイムのバージョンを指定します。 既定では、最初に読み込まれたバージョンがプロファイリングされます。|-   [方法: side-by-side 実行でプロファイリングするように .NET Framework ランタイムを指定する](../profiling/how-to-specify-the-dotnet-framework-runtime.md)|



