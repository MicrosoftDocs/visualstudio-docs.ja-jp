---
title: 'DA0006: 値の型で Equals() をオーバーライドしてください | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.rules.DAOverrideEquals
- vs.performance.6
- vs.performance.DA0006
- vs.performance.rules.DA0006
ms.assetid: 4d85bdd6-b571-47e0-afd6-ba3764e4eed5
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b360c97e64842d46fe2b121e8505ac0f9cafebed
ms.sourcegitcommit: 42ea834b446ac65c679fa1043f853bea5f1c9c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/19/2018
---
# <a name="da0006-override-equals-for-value-types"></a>DA0006: 値の型で Equals() をオーバーライドしてください
|||  
|-|-|  
|規則 ID|DA0006|  
|カテゴリ|.NET Framework の使用|  
|プロファイル方法|サンプリング|  
|メッセージ|値の型で Equals と等値演算子をオーバーライドしてください。|  
|メッセージの種類|警告|  
  
## <a name="cause"></a>原因  
 パブリック値型の Equals メソッドまたは等値演算子の呼び出しが、プロファイリング データの大きな割合を占めています。 さらに効率的な方法を実装することを検討してください。  
  
## <a name="rule-description"></a>規則の説明  
 値型の場合、Equals を継承した実装が <xref:System.Reflection> ライブラリを使用して、この種類のすべてのフィールドの内容を比較します。 Reflection は計算コストが高いため、場合によってはすべてのフィールドで等値性を比較する必要はありません。 ユーザーがインスタンスの比較または並べ替えを行うことや、ハッシュ テーブル キーとしてインスタンスを使用することが予想される場合には、値型に Equals を実装する必要があります。 お使いのプログラミング言語が演算子のオーバーロードに対応している場合、等値演算子と非等値演算子も実装してください。  
  
 Equals と等値演算子をオーバーライドする方法については、[Equals および等値演算子 (==) 実装のガイドライン](http://go.microsoft.com/fwlink/?LinkId=177818)を参照してください。  
  
## <a name="how-to-investigate-a-warning"></a>警告の調査方法  
 Equals と等値演算子の実装例については、コード分析ルールの「[CA1815: equals および operator equals を値型でオーバーライドします](../code-quality/ca1815-override-equals-and-operator-equals-on-value-types.md)」を参照してください。