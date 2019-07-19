---
title: '方法: 収集方法を選択する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- performance tools, choosing collection method
- profiling tools, choosing collection method
- performance collection methods
ms.assetid: c87cfd3a-0fc7-49ae-9c05-d8480891cc63
caps.latest.revision: 39
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 33ff14ce88f2032b998214ed11310a15550321dc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68199802"
---
# <a name="how-to-choose-collection-methods"></a>方法: 収集方法を選択する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロファイリング ツールでは、サンプリング、インストルメンテーション、コンカレンシーという 3 種類のパフォーマンス データ収集方法をサポートしています。 また、.NET メモリ割り当てと有効期間データの収集には、サンプリングまたはインストルメンテーションの方式を使用できます。  
  
 **必要条件**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]、 [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]、 [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
  パフォーマンス セッションの **[メソッド]** プロパティを使用すると、アプリケーションに最適の収集方法を指定できます。 収集方法はパフォーマンス ウィザード、パフォーマンス エクスプローラー、またはパフォーマンス セッションのプロパティ ページから設定することができます。 コマンド ライン ツールを使用する場合、詳細については「[コマンド ラインからのプロファイリング](../profiling/using-the-profiling-tools-from-the-command-line.md)」を参照してください。  
  
## <a name="performance-wizard"></a>パフォーマンス ウィザード  
  
#### <a name="to-select-a-collection-method-using-the-performance-wizard"></a>パフォーマンス ウィザードを使用して収集方法を選択するには  
  
- ウィザードの最初のページで、次のいずれかのオプションを選択します。  
  
|オプション|説明|  
|------------|-----------------|  
|**CPU サンプリング**|初期の分析と CPU 使用率の問題の分析に役立つアプリケーション統計情報を収集します。|  
|**インストルメンテーション**|焦点を絞った分析、および入出力パフォーマンスの問題分析に役立つ詳しいタイミング データを収集します。|  
|**.NET メモリ割り当て**|サンプリング プロファイリング方式を使用して [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] メモリ割り当てデータを収集します。|  
|**コンカレンシー**|数値のリソース競合データを収集します。|  
  
## <a name="performance-explorer"></a>パフォーマンス エクスプローラー  
  
#### <a name="to-select-a-collection-method-using-performance-explorer"></a>パフォーマンス エクスプローラーを使用して収集方法を選択するには  
  
1. **パフォーマンス エクスプローラー**のツール バーで、 **[メソッド]** ドロップダウン リストの横の矢印をクリックします。  
  
2. 必要な収集方法をクリックします。  
  
## <a name="performance-session-property-pages"></a>パフォーマンス セッションのプロパティ ページ  
  
#### <a name="to-select-the-sampling-or-instrumentation-method-using-performance-session-properties"></a>パフォーマンス セッションのプロパティを使用して、サンプリング方式またはインストルメンテーション方式を選択するには  
  
1. **パフォーマンス エクスプローラー**でパフォーマンス セッションを選択します。  
  
     パフォーマンス セッション ファイル名の拡張子は .psess です。  
  
2. パフォーマンス セッションを右クリックして、 **[プロパティ]** をクリックします。  
  
3. **[プロパティ ページ]** で **[全般]** をクリックします。  
  
4. 必要な収集方法をクリックします。  
  
    - サンプリング データの収集に使用できるその他のオプションについては、「[サンプリングを使用したパフォーマンス統計情報の収集](../profiling/collecting-performance-statistics-by-using-sampling.md)」を参照してください。  
  
    - サンプリング データの収集に使用できるその他のオプションについては、「[インストルメンテーションを使用した詳細なタイミング データの収集](../profiling/collecting-detailed-timing-data-by-using-instrumentation.md)」を参照してください。  
  
#### <a name="to-select-net-memory-data-collection-by-using-performance-session-properties"></a>パフォーマンス セッションのプロパティを使用して .NET メモリ データの収集を選択するには  
  
1. **パフォーマンス エクスプローラー**でパフォーマンス セッションを選択します。  
  
     パフォーマンス セッション ファイル名の拡張子は .psess です。  
  
2. パフォーマンス セッションを右クリックして、 **[プロパティ]** をクリックします。  
  
3. **[プロパティ ページ]** で **[全般]** をクリックします。  
  
4. **[サンプリング]** または **[インストルメンテーション]** をクリックします。  
  
5. **[.NET オブジェクトの割り当て情報を収集]** をクリックして [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] オブジェクト割り当てのサイズと数を収集します。  
  
6. (省略可能) **[.NET オブジェクトの有効期間情報も収集]** をクリックして、オブジェクト メモリが解放されたガベージ コレクションの生成に関するデータを収集します。  
  
     .NET メモリ データの収集に使用できるその他のオプションについては、「[.NET メモリの割り当ておよび有効期間データの収集](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)」を参照してください。  
  
#### <a name="to-select-concurrency-data-collection-by-using-performance-session-properties"></a>パフォーマンス セッションのプロパティを使用してコンカレンシー データの収集を選択するには  
  
1. **パフォーマンス エクスプローラー**で、パフォーマンス セッションを右クリックして、 **[プロパティ]** をクリックします。  
  
2. **[プロパティ ページ]** で **[全般]** をクリックします。  
  
3. **[コンカレンシー]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [パフォーマンス セッションの構成](../profiling/configuring-performance-sessions.md)   
 [サンプリング データ値について](../profiling/understanding-sampling-data-values.md)   
 [パフォーマンス セッションのプロパティ](../profiling/performance-session-properties.md)
