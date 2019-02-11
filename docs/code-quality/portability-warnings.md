---
title: 移植性に関する警告
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.PortabilityRules
helpviewer_keywords:
- portability warnings
- managed code analysis warnings, portability warnings
- warnings, portability
ms.assetid: 902e859a-2153-4970-baaa-8a5b4a11806f
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a6a3557cffec60de91da46f60040ec675c866cbf
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55946603"
---
# <a name="portability-warnings"></a>移植性に関する警告
移植性に関する警告は、さまざまなオペレーティング システムでの移植性をサポートします。

## <a name="in-this-section"></a>このセクションの内容

|ルール|説明|
|----------|-----------------|
|[CA 1900:値型フィールドはポータブルでなければなりません](../code-quality/ca1900-value-type-fields-should-be-portable.md)|このルールは、明示的なレイアウト属性を使用して宣言された構造体が、64 ビット オペレーティング システムのアンマネージ コードにマーシャ リングするときに、適切にアライメントされるかを確認します。|
|[CA1901:P/invoke 宣言はポータブルでなければなりません](../code-quality/ca1901-p-invoke-declarations-should-be-portable.md)|このルールでは、各パラメーターのサイズと、P/invoke の戻り値が評価され、サイズが 32 ビットと 64 ビットのオペレーティング システムのアンマネージ コードにマーシャ リングするときに正しいことを確認します。|
|[CA1903:対象のフレームワークから API のみを使用します。](../code-quality/ca1903-use-only-api-from-targeted-framework.md)|メンバーまたは型が、プロジェクトの対象のフレームワークに含まれていない Service Pack で導入されたメンバーまたは型を使用しています。|