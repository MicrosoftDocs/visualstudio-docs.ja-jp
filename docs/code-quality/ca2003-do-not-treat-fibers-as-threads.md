---
title: CA2003:ファイバーをスレッドとして扱いません
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2003
- DoNotTreatFibersAsThreads
helpviewer_keywords:
- CA2003
- DoNotTreatFibersAsThreads
ms.assetid: 15398fb1-f384-4bcc-ad93-00e1c0fa9ddf
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8faaf3c6557065188c795d75ea9bbe4e78998709
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62806989"
---
# <a name="ca2003-do-not-treat-fibers-as-threads"></a>CA2003:ファイバーをスレッドとして扱いません

|||
|-|-|
|TypeName|DoNotTreatFibersAsThreads|
|CheckId|CA2003|
|カテゴリ|Microsoft.Reliability|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因

マネージ スレッドが Win32 スレッドとして扱われています。

## <a name="rule-description"></a>規則の説明

マネージ スレッドが Win32 スレッド; と見なさないでください。ファイバーになります。 共通言語ランタイム (CLR) では、SQL によって所有されている実際のスレッドのコンテキストでファイバーとしてマネージ スレッドが実行されます。 これらのスレッドは、SQL Server プロセスで、Appdomain とデータベース間で共有できます。 スレッド ローカル ストレージの機能を使用して管理されているが、アンマネージ スレッド ローカル ストレージを使用して、または、コードが現在の OS スレッドで再度実行が前提としています。 しない可能性があります。 スレッドのロケールなどの設定は変更されません。 ロックに入るスレッドがロックを終了する必要がありますも必要なためは、ロケールなどの createmutex に P/invoke を使用してを呼び出していません。 ファイバーを使用するが、ロックに入るスレッドはロックを終了しない、ため、Win32 のクリティカル セクションおよびミュー テックスは SQL で役に立ちません。 安全に、マネージのほとんどの状態を使用することがあります<xref:System.Threading.Thread>マネージ スレッド ローカル ストレージと、スレッドの現在のユーザー インターフェイス (UI) カルチャを含むオブジェクト。 ただし、モデルの理由から、プログラミングをすることはできません SQL を使用すると、スレッドの現在のカルチャを変更します。 新しいアクセス許可をこの制限が適用されます。

## <a name="how-to-fix-violations"></a>違反の修正方法

スレッドの使用状況を確認し、それに応じてコードを変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制します。

このルールを抑制しないでください。