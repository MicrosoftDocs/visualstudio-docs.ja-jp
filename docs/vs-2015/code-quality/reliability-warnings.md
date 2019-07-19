---
title: 信頼性に関する警告 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.reliabilityrules
helpviewer_keywords:
- warnings, reliability
- reliability warnings
- managed code analysis warnings, reliability warnings
ms.assetid: 77886846-10a2-4585-968a-7eb60ebe07e8
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 328e374a12b45c4a139d5e59c33be3a7bd74ac3d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68142194"
---
# <a name="reliability-warnings"></a>信頼性に関する警告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

信頼性に関する警告は、メモリやスレッドの正しい使用法などのライブラリとアプリケーションの信頼性をサポートします。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|ルール|説明|  
|----------|-----------------|  
|[CA 2000:スコープが失われる前にオブジェクトを破棄します。](../code-quality/ca2000-dispose-objects-before-losing-scope.md)|例外的なイベントが発生するとオブジェクトのファイナライザーを実行できないため、オブジェクトに対するすべての参照がスコープ外になる前に、オブジェクトを明示的に破棄する必要があります。|  
|[CA 2001:問題のあるメソッドは呼び出しません](../code-quality/ca2001-avoid-calling-problematic-methods.md)|メンバーが危険性または問題のあるメソッドを呼び出します。|  
|[CA 2002:Id が不十分なオブジェクトをロックしないでください。](../code-quality/ca2002-do-not-lock-on-objects-with-weak-identity.md)|アプリケーション ドメインの境界を越えてオブジェクトに直接アクセスできる場合、そのオブジェクトの ID は不十分と表現されます。 スレッドで ID が不十分なオブジェクトをロックしようとすると、ブロックされることがあります。たとえば、異なるアプリケーション ドメインの別スレッドで、既に同じオブジェクトがロックされている場合です。|  
|[CA 2003:ファイバーをスレッドとして処理しません](../code-quality/ca2003-do-not-treat-fibers-as-threads.md)|マネージ スレッドが Win32 スレッドとして扱われています。|  
|[CA 2004:GC への呼び出しを削除します。KeepAlive](../code-quality/ca2004-remove-calls-to-gc-keepalive.md)|SafeHandle の使用に変換する場合は、GC にすべての呼び出しを削除します。KeepAlive (オブジェクト)。 ここでは、クラスでは、GC している必要があります。ファイナライザーはありませんが、OS の最終処理に SafeHandle に依存するいると仮定した場合、KeepAlive は、それらの処理です。|  
|[CA2006:SafeHandle を使用して、ネイティブ リソースをカプセル化するには](../code-quality/ca2006-use-safehandle-to-encapsulate-native-resources.md)|マネージド コードで IntPtr を使用すると、セキュリティ上の問題および信頼性の問題が発生する可能性があります。 すべての IntPtr の使用状況をチェックして、SafeHandle または類似のテクノロジに置き換える必要があるかどうかを判断してください。|
