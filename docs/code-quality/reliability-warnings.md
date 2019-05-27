---
title: 信頼性に関する警告
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.reliabilityrules
helpviewer_keywords:
- warnings, reliability
- reliability warnings
- managed code analysis warnings, reliability warnings
ms.assetid: 77886846-10a2-4585-968a-7eb60ebe07e8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 009422eaf9ac81af6e8f9d48732655b2528c85a0
ms.sourcegitcommit: 92a04c57ac0a49f304fa2ea5043436f30068c3cd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65976144"
---
# <a name="reliability-warnings"></a>信頼性に関する警告

信頼性に関する警告は、メモリやスレッドの正しい使用法などのライブラリとアプリケーションの信頼性をサポートします。 信頼性の規則は次のとおりです。

|ルール|説明|
|----------|-----------------|
|[CA 2000:スコープが失われる前にオブジェクトを破棄します。](../code-quality/ca2000-dispose-objects-before-losing-scope.md)|例外的なイベントが発生するとオブジェクトのファイナライザーを実行できないため、オブジェクトに対するすべての参照がスコープ外になる前に、オブジェクトを明示的に破棄する必要があります。|
|[CA 2001:問題のあるメソッドは呼び出しません](../code-quality/ca2001-avoid-calling-problematic-methods.md)|メンバーが危険性または問題のあるメソッドを呼び出します。|
|[CA 2002:Id が不十分なオブジェクトをロックしないでください。](../code-quality/ca2002-do-not-lock-on-objects-with-weak-identity.md)|アプリケーション ドメインの境界を越えてオブジェクトに直接アクセスできる場合、そのオブジェクトの ID は不十分と表現されます。 スレッドで ID が不十分なオブジェクトをロックしようとすると、ブロックされることがあります。たとえば、異なるアプリケーション ドメインの別スレッドで、既に同じオブジェクトがロックされている場合です。|
|[CA 2003:ファイバーをスレッドとして処理しません](../code-quality/ca2003-do-not-treat-fibers-as-threads.md)|マネージ スレッドが Win32 スレッドとして扱われています。|
|[CA 2004:GC への呼び出しを削除します。KeepAlive](../code-quality/ca2004-remove-calls-to-gc-keepalive.md)|SafeHandle の使用に変換する場合は、GC にすべての呼び出しを削除します。KeepAlive (オブジェクト)。 ここでは、クラスでは、GC している必要があります。ファイナライザーはありませんが、OS の最終処理に SafeHandle に依存するいると仮定した場合、KeepAlive は、それらの処理です。|
|[CA2006:SafeHandle を使用して、ネイティブ リソースをカプセル化するには](../code-quality/ca2006-use-safehandle-to-encapsulate-native-resources.md)|マネージド コードで IntPtr を使用すると、セキュリティ上の問題および信頼性の問題が発生する可能性があります。 すべての IntPtr の使用状況をチェックして、SafeHandle または類似のテクノロジに置き換える必要があるかどうかを判断してください。|
|[CA2007:タスクを直接待機しません](../code-quality/ca2007-do-not-directly-await-task.md)|非同期メソッド[待機](/dotnet/csharp/language-reference/keywords/await)、<xref:System.Threading.Tasks.Task>直接します。|