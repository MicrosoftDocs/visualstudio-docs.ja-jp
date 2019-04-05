---
title: CA2003:ファイバーをスレッドとして扱いません |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2003
- DoNotTreatFibersAsThreads
helpviewer_keywords:
- CA2003
- DoNotTreatFibersAsThreads
ms.assetid: 15398fb1-f384-4bcc-ad93-00e1c0fa9ddf
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 0a1683c8cb9b9c6dc856f40ddbc7864d773f2101
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58975864"
---
# <a name="ca2003-do-not-treat-fibers-as-threads"></a>CA2003:ファイバーをスレッドとして扱いません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotTreatFibersAsThreads|
|CheckId|CA2003|
|カテゴリ|Microsoft.Reliability|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 マネージ スレッドが Win32 スレッドとして扱われています。

## <a name="rule-description"></a>規則の説明
 マネージ スレッドが Win32 スレッドとは限りません。 ファイバーになります。 共通言語ランタイム (CLR) は、SQL によって所有されている実際のスレッドのコンテキストでファイバーとしてマネージ スレッドが実行されます。 これらのスレッドは、SQL Server プロセスで、Appdomain とデータベース間で共有できます。 マネージ スレッド ローカル ストレージは機能しますが、アンマネージ スレッド ローカル ストレージを使用したり、コードが現在の OS スレッドで再度実行が前提としています。 なりません。 スレッドのロケールなどの設定は変更されません。 ロックに入るスレッドがロックを終了する必要がありますも必要なためは、ロケールなどの createmutex に P/invoke を使用してを呼び出していません。 これができないため、ケース ファイバーを使用するときに、Win32 のクリティカル セクションおよびミュー テックスは SQL では使用できません。 System.Thread のマネージ オブジェクトのほとんどの状態を安全に使用可能性があります。 これには、マネージ スレッド ローカル ストレージと、スレッドの現在のユーザー インターフェイス (UI) カルチャが含まれます。 ただし、モデルの理由から、プログラミングをするできなく SQL; を使用すると、スレッドの現在のカルチャを変更するにはこれは、新しいアクセス許可を通じて適用されます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 スレッドの使用状況を確認し、それに応じてコードを変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 このルールを抑制する必要があります。
