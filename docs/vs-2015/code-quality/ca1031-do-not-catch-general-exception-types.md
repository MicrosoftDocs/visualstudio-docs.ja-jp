---
title: CA1031:一般的な例外の種類はキャッチしません |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1031
- DoNotCatchGeneralExceptionTypes
helpviewer_keywords:
- CA1031
- DoNotCatchGeneralExceptionTypes
ms.assetid: cbc283ae-2a46-4ec0-940e-85aa189b118f
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 4588a949b4b6439c3f76270b0bcdab9cd52c23d9
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63431226"
---
# <a name="ca1031-do-not-catch-general-exception-types"></a>CA1031:一般的な例外の種類はキャッチしません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotCatchGeneralExceptionTypes|
|CheckId|CA1031|
|カテゴリ|Microsoft.Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 などの一般的な例外<xref:System.Exception?displayProperty=fullName>または<xref:System.SystemException?displayProperty=fullName>でキャッチされます、`catch`ステートメント、またはなどの一般的な catch 句`catch()`使用されます。

## <a name="rule-description"></a>規則の説明
 汎用的な例外はキャッチしないでください。

## <a name="how-to-fix-violations"></a>違反の修正方法
 このルールの違反を修正するより具体的な例外をキャッチまたは最後のステートメントとして一般的な例外を再スロー、`catch`ブロックします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。 一般的な例外の種類をキャッチして、ライブラリ ユーザーから、実行時の問題を非表示にすることができます、指定するとデバッグはより難しくなります。

> [!NOTE]
> 以降では、 [!INCLUDE[net_v40_long](../includes/net-v40-long-md.md)]、共通言語ランタイム (CLR) は、オペレーティング システムとでアクセス違反などのマネージ コードで発生する破損状態例外を提供できなく[!INCLUDE[TLA#tla_mswin](../includes/tlasharptla-mswin-md.md)]、マネージ コードで処理されます。 アプリケーションをコンパイルする場合、[!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)]以降のバージョンの管理と適用できる破損状態例外の処理、<xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute>属性を破損状態例外を処理するメソッド。

## <a name="example"></a>例
 次の例は、この規則に違反する型と正しく実装する型、`catch`ブロックします。

 [!code-cpp[FxCop.Design.ExceptionAndSystemException#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionAndSystemException/cpp/FxCop.Design.ExceptionAndSystemException.cpp#1)]
 [!code-csharp[FxCop.Design.ExceptionAndSystemException#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionAndSystemException/cs/FxCop.Design.ExceptionAndSystemException.cs#1)]
 [!code-vb[FxCop.Design.ExceptionAndSystemException#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionAndSystemException/vb/FxCop.Design.ExceptionAndSystemException.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA 2200:スタックの詳細を保持するために再スローします。](../code-quality/ca2200-rethrow-to-preserve-stack-details.md)
