---
title: "DA0013: String.Split/String.Substring が頻繁に使用されています。 | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vs.performance.13
- vs.performance.rules.DAAvoidStringSubstr
- vs.performance.DA0013
- vs.performance.rules.DA0013
helpviewer_keywords:
- vs.performance.13
- vs.performance.rules.DA0013
ms.assetid: f501f423-bef9-4e08-bf96-c9ac9957e5a2
caps.latest.revision: "14"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1101457388b5ba54752f47014c9c389fcb2cb073
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2017
---
# <a name="da0013-high-usage-of-stringsplit-or-stringsubstring"></a>DA0013: String.Split/String.Substring が頻繁に使用されています
|||  
|-|-|  
|規則 ID|DA0013|  
|カテゴリ|.NET Framework の使用ガイド|  
|プロファイル方法|サンプリング|  
|メッセージ|String.Split 関数と String.Substring 関数の使用回数を少なくすることを検討してください。|  
|規則の種類|警告|  
  
## <a name="cause"></a>原因  
 System.String.Split メソッドまたは System.String.Substring メソッドの呼び出しがプロファイル データの大きな割合を占めています。 文字列内に部分文字列が存在することをテストする場合は、System.String.IndexOf または System.String.IndexOfAny を使用することを検討してください。  
  
## <a name="rule-description"></a>規則の説明  
 Split メソッドは、String オブジェクトを操作し、元の文字列の部分文字列を含む文字列の新しい配列を返します。 関数は、返された配列オブジェクトにメモリを割り当て、検出された配列要素ごとに新しい String オブジェクトを割り当てます。 同様に、Substr メソッドは String オブジェクトを操作し、要求された部分文字列と等しい新しい文字列を返します。  
  
 メモリの割り当ての管理がアプリケーションで重要な場合、String.Split メソッドと String.Substr メソッドとは別のものを使用することを検討してください。 たとえば、IndexOf メソッドまたは IndexOfAny メソッドを使用すると、String クラスの新しいインスタンスを作成しなくても、文字列内の特定の部分文字列を見つけることができます。  
  
## <a name="how-to-investigate-a-warning"></a>警告の調査方法  
 [エラー一覧] ウィンドウに表示されたメッセージをダブルクリックして、サンプリング プロファイル データの[関数の詳細ビュー](../profiling/function-details-view.md)に移動します。 呼び出し関数を調べ、System.String.Split メソッドまたは System.String.Substr メソッドを最も頻繁に使用するプログラムのセクションを見つけます。 可能な場合は、IndexOf メソッドまたは IndexOfAny メソッドを使用して、String クラスの新しいインスタンスを作成せずに、文字列内の特定の部分文字列を見つけます。