---
title: 'CA1504: 紛らわしいフィールド名を確認してください。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ReviewMisleadingFieldNames
- CA1504
helpviewer_keywords:
- CA1504
- ReviewMisleadingFieldNames
ms.assetid: 94136ff1-4aaf-4dc2-9170-48c171ab7499
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: c3f1cca5dd33047a4d19c78013dd535e0e9dd6f2
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72607757"
---
# <a name="ca1504-review-misleading-field-names"></a>CA1504: 紛らわしいフィールド名を確認します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ReviewMisleadingFieldNames|
|CheckId|CA1504|
|カテゴリ|Microsoft の保守容易性|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 インスタンスフィールドの名前が "s_" で始まるか、または `static` ([!INCLUDE[vbprvb](../includes/vbprvb-md.md)] の `Shared`) フィールドの名前が "m_" で始まる。

## <a name="rule-description"></a>規則の説明
 "S_" で始まるフィールド名は、多くのユーザーによって静的データに関連付けられています。 同様に、"m_" で始まるフィールド名は、インスタンス (メンバー) データに関連付けられています。 コードを保守しやすくするために、一般的に使用される規則に従う必要があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、適切なプレフィックスを使用してフィールドの名前を変更します。 または、`static` 修飾子を追加または削除して、フィールドが現在のサフィックスに一致するようにします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。
