---
title: 'CA2205: マネージドに相当する Win32 API | を使用します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UseManagedEquivalentsOfWin32Api
- CA2205
helpviewer_keywords:
- UseManagedEquivalentsOfWin32Api
- CA2205
ms.assetid: 1c65ab59-3e50-4488-a727-3969c7f6cbe4
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 931b1e5099bf221fefc7a8f4a19524d2531a4418
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72609484"
---
# <a name="ca2205-use-managed-equivalents-of-win32-api"></a>CA2205: Win32 API に相当するマネージド API を使用します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|UseManagedEquivalentsOfWin32Api|
|CheckId|CA2205|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 プラットフォーム呼び出しメソッドが定義されていますが、それと同等の機能を持つメソッドが [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] クラスライブラリに存在します。

## <a name="rule-description"></a>規則の説明
 Platform invoke メソッドは、アンマネージ DLL 関数を呼び出すために使用され、<xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> 属性、または Visual Basic の `Declare` キーワードを使用して定義されます。 Platform invoke メソッドが正しく定義されていないと、misnamed 関数、パラメーターと戻り値のデータ型のマッピングが正しくない、または呼び出し規約や文字などの不適切なフィールドの指定などの問題が原因で、ランタイム例外が発生する可能性があります。一連. 使用可能な場合は、通常、アンマネージメソッドを直接定義して呼び出すよりも、通常はより単純でエラーが発生しやすくなります。 プラットフォーム呼び出しメソッドを呼び出すと、対処する必要がある追加のセキュリティ問題が発生する可能性もあります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、アンマネージ関数の呼び出しを、それと等価なマネージ関数の呼び出しに置き換えます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 推奨される置換方法によって必要な機能が提供されない場合は、この規則による警告を非表示にします。

## <a name="example"></a>例
 次の例は、規則に違反するプラットフォーム呼び出しメソッドの定義を示しています。 さらに、プラットフォーム呼び出しメソッドと同等のマネージメソッドの呼び出しが表示されます。

 [!code-csharp[FxCop.Usage.ManagedEquivalents#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.ManagedEquivalents/cs/FxCop.Usage.ManagedEquivalents.cs#1)]
 [!code-vb[FxCop.Usage.ManagedEquivalents#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.ManagedEquivalents/vb/FxCop.Usage.ManagedEquivalents.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1404: P/Invoke の直後に GetLastError を呼び出します](../code-quality/ca1404-call-getlasterror-immediately-after-p-invoke.md)

 [CA1060: P/Invoke を NativeMethods クラスに移動します](../code-quality/ca1060-move-p-invokes-to-nativemethods-class.md)

 [CA1400: P/Invoke エントリ ポイントは存在しなければなりません](../code-quality/ca1400-p-invoke-entry-points-should-exist.md)

 [CA1401: P/Invoke は参照可能になりません](../code-quality/ca1401-p-invokes-should-not-be-visible.md)

 [CA2101: P/Invoke 文字列引数に対してマーシャリングを指定します](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)
