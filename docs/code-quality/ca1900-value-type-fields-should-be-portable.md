---
title: CA1900:値型フィールドはポータブルでなければなりません
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1900
- ValueTypeFieldsShouldBePortable
helpviewer_keywords:
- ValueTypeFieldsShouldBePortable
- CA1900
ms.assetid: 1787d371-389f-4d39-b305-12b53bc0dfb9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e823a58d7a2be45c43305320bd32175de7a3fad6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62545395"
---
# <a name="ca1900-value-type-fields-should-be-portable"></a>CA1900:値型フィールドはポータブルでなければなりません

|||
|-|-|
|TypeName|ValueTypeFieldsShouldBePortable|
|CheckId|CA1900|
|カテゴリ|Microsoft.Portability|
|互換性に影響する変更点|– 場合、アセンブリの外側にフィールドを確認できます。<br /><br /> 改行のフィールドが、アセンブリの外部に表示されない場合。|

## <a name="cause"></a>原因
 このルールは、明示的なレイアウトで宣言された構造体が、64 ビット オペレーティング システムのアンマネージ コードにマーシャ リングするときに、適切にアライメントされるかを確認します。 Ia-64 では、アラインされていないメモリにアクセスし、この違反が固定されていない場合、プロセスがクラッシュは許可されません。

## <a name="rule-description"></a>規則の説明
 構造体で明示的なレイアウトを含む 64 ビット オペレーティング システムでクラッシュするフィールドの不整合が発生します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 詳細はオフセットが 8 の倍数である必要があります。 または 8 バイト未満であるすべてのフィールドはオフセット、サイズの倍数である、および 8 バイトであるフィールドにあります。 別のソリューションは、使用する`LayoutKind.Sequential`の代わりに`LayoutKind.Explicit`妥当な場合は、します。

## <a name="when-to-suppress-warnings"></a>警告を抑制します。
 エラーが発生した場合にのみ、この警告を抑制する必要があります。