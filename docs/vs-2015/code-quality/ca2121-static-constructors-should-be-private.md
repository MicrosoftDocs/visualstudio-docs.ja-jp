---
title: 'CA2121: 静的コンストラクターは private | である必要があります。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2121
- StaticConstructorsShouldBePrivate
helpviewer_keywords:
- CA2121
- StaticConstructorsShouldBePrivate
ms.assetid: ee93c620-8fc1-4e47-866c-d389c3ca9f2e
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 9f28c1dadaef2dc88a3d728322dee1053ccdd69c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663071"
---
# <a name="ca2121-static-constructors-should-be-private"></a>CA2121: 静的コンストラクターはプライベートでなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|StaticConstructorsShouldBePrivate|
|CheckId|CA2121|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 型に、プライベートでない静的コンストラクターがあります。

## <a name="rule-description"></a>規則の説明
 静的コンストラクターは、クラスコンストラクターとも呼ばれ、型を初期化するために使用されます。 システムで静的コンストラクターが呼び出されてから、型の最初のインスタンスが作成されるか、静的メンバーが参照されます。 静的コンストラクターが呼び出されるタイミングは、ユーザーが制御できません。 静的コンストラクターがプライベートである場合、システム以外のコードから呼び出すことができます。 コンストラクターで実行される操作によっては、これによって予期しない動作が発生することがあります。

 この規則は、 C#および Visual Basic .net コンパイラによって適用されます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 通常、違反は次のいずれかの操作によって発生します。

- 型の静的コンストラクターを定義しましたが、それをプライベートに設定しませんでした。

- プログラミング言語コンパイラにより、既定の静的コンストラクターが型に追加され、プライベートに設定されませんでした。

  最初の種類の違反を修正するには、静的コンストラクターをプライベートにします。 2番目の種類を修正するには、プライベートな静的コンストラクターを型に追加します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 これらの違反を抑制しないでください。 ソフトウェア設計で静的コンストラクターへの明示的な呼び出しが必要な場合は、設計に重大な欠陥が含まれている可能性があるため、確認する必要があります。
