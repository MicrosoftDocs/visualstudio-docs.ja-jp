---
title: 'CA1713: イベントは、before または after プレフィックスを含むことはできません'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- EventsShouldNotHaveBeforeOrAfterPrefix
- CA1713
helpviewer_keywords:
- CA1713
- EventsShouldNotHaveBeforeOrAfterPrefix
ms.assetid: 855772a4-aa9e-410b-88c1-c5fba1ca63da
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: dc6d8b78ff1b00d1c5e5a6c6a597855243ea12fb
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/13/2018
ms.locfileid: "45550726"
---
# <a name="ca1713-events-should-not-have-before-or-after-prefix"></a>CA1713: イベントは、before または after プレフィックスを含むことはできません
|||
|-|-|
|TypeName|EventsShouldNotHaveBeforeOrAfterPrefix|
|CheckId|CA1713|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 イベントの名前は、'Before' または 'After' で開始します。

## <a name="rule-description"></a>規則の説明
 イベント名は、イベントを発生させるアクションを示す必要があります。 特定のシーケンスで発生する関連イベントに名前を付ける場合、現在時制または過去時制を使用して、アクション シーケンスの相対的な位置を示します。 たとえば、リソースを閉じるときに発生するイベントのペアの名前付け、ときに名前を付けますが '終了' と 'BeforeClose' および 'AfterClose' ではなく ' Closed'。

 名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、新しいソフトウェア ライブラリを習得するまでの時間を短縮でき、マネージド コード開発の専門家によってライブラリが開発されたという信頼を顧客に与えることができます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 イベントの名前から、プレフィックスを削除して、現在または過去時制の動詞を使用する名前の変更を検討してください。

## <a name="when-to-suppress-warnings"></a>警告を抑制します。
 この規則による警告は抑制しないでください。