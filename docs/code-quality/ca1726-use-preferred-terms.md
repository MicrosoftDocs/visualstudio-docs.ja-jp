---
title: CA1726:適切な用語を使用します
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- UsePreferredTerms
- CA1726
helpviewer_keywords:
- UsePreferredTerms
ms.assetid: 642b2acd-3a33-4d1f-b0a7-67073ae73be2
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e4e068fee014d767b7afcdf8183ac6611b299f36
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921581"
---
# <a name="ca1726-use-preferred-terms"></a>CA1726:適切な用語を使用します

|||
|-|-|
|TypeName|UsePreferredTerms|
|CheckId|CA1726|
|Category|Microsoft.Naming|
|互換性に影響する変更点|中断-アセンブリで発生した場合<br /><br /> 中断なし-型パラメーターで発生した場合|

## <a name="cause"></a>原因

外部から参照可能な識別子の名前に含まれている用語に対応する、別の推奨される用語があります。 または、名前に、フラグまたはフラグが含まれています。

## <a name="rule-description"></a>規則の説明

このルールは、識別子をトークンに解析します。 各トークンと連続するデュアルトークンの組み合わせは、ルールに組み込まれている用語と、カスタム辞書の非推奨のセクションに比較されます。 次の表に、ルールに組み込まれている用語と、その優先順位を示します。

|廃止された用語|優先する用語|
|-------------------|--------------------|
|`Arent`|`AreNot`|
|`Cancelled`|`Canceled`|
|`Cant`|`Cannot`|
|`ComPlus`|`EnterpriseServices`|
|`Couldnt`|`CouldNot`|
|`Didnt`|`DidNot`|
|`Doesnt`|`DoesNot`|
|`Dont`|`DoNot`|
|`Flag` または `Flags`|置換語句はありません。 使わないでください。|
|`Hadnt`|`HadNot`|
|`Hasnt`|`HasNot`|
|`Havent`|`HaveNot`|
|`Indices`|`Indexes`|
|`Isnt`|`IsNot`|
|`LogIn`|`LogOn`|
|`LogOut`|`LogOff`|
|`Shouldnt`|`ShouldNot`|
|`SignOn`|`SignIn`|
|`SignOff`|`SignOut`|
|`Wasnt`|`WasNot`|
|`Werent`|`WereNot`|
|`Wont`|`WillNot`|
|`Wouldnt`|`WouldNot`|
|`Writeable`|`Writable`|

## <a name="how-to-fix-violations"></a>違反の修正方法
この規則違反を修正するには、用語を適切な代替用語で置き換えます。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合
識別子の名前が意図的なものであり、特に優先用語ではなく元の用語に関連付けられている場合にのみ、この規則からの警告を非表示にします。

## <a name="related-rules"></a>関連するルール
[名前付けに関する警告](../code-quality/naming-warnings.md)