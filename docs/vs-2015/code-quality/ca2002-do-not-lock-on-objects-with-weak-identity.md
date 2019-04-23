---
title: CA2002:Id が不十分なオブジェクトをロックしないでください |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotLockOnObjectsWithWeakIdentity
- CA2002
helpviewer_keywords:
- CA2002
- DoNotLockOnObjectsWithWeakIdentity
ms.assetid: 16100b39-c6fc-452b-8fca-8b459a26c286
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 631979309d9ad42a25b244e8806e5a6849f8b81d
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60081490"
---
# <a name="ca2002-do-not-lock-on-objects-with-weak-identity"></a>CA2002:弱い ID を伴うオブジェクト上でロックしません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotLockOnObjectsWithWeakIdentity|
|CheckId|CA2002|
|カテゴリ|Microsoft.Reliability|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 スレッドは、弱い id を持つオブジェクトのロックを取得しようとします。

## <a name="rule-description"></a>規則の説明
 アプリケーション ドメインの境界を越えてオブジェクトに直接アクセスできる場合、そのオブジェクトの ID は不十分と表現されます。 スレッドで ID が不十分なオブジェクトをロックしようとすると、ブロックされることがあります。たとえば、異なるアプリケーション ドメインの別スレッドで、既に同じオブジェクトがロックされている場合です。 次の種類は、id が不十分なと、ルールによってフラグが設定されます。

- <xref:System.MarshalByRefObject>

- <xref:System.ExecutionEngineException>

- <xref:System.OutOfMemoryException>

- <xref:System.StackOverflowException>

- <xref:System.String>

- <xref:System.Reflection.MemberInfo>

- <xref:System.Reflection.ParameterInfo>

- <xref:System.Threading.Thread>

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、[説明] セクションに一覧されていない型からオブジェクトを使用します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="related-rules"></a>関連規則
 [CA2213: 破棄可能なフィールドは破棄されなければなりません](../code-quality/ca2213-disposable-fields-should-be-disposed.md)

## <a name="example"></a>例
 次の例では、ルールに違反しているオブジェクトのロックを示します。

 [!code-csharp[FxCop.Reliability.LockWeakObjects#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Reliability.LockWeakObjects/cs/FxCop.Reliability.LockWeakObjects.cs#1)]
 [!code-vb[FxCop.Reliability.LockWeakObjects#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Reliability.LockWeakObjects/vb/FxCop.Reliability.LockWeakObjects.vb#1)]

## <a name="see-also"></a>関連項目
 <xref:System.Threading.Monitor> <xref:System.AppDomain>
 [lock ステートメント](http://msdn.microsoft.com/library/656da1a4-707e-4ef6-9c6e-6d13b646af42) [SyncLock ステートメント](http://msdn.microsoft.com/library/14501703-298f-4d43-b139-c4b6366af176)
