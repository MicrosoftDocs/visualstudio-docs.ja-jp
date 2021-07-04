---
title: 式の評価のコンテキスト | Microsoft Docs
description: 式の評価のコンテキストについて説明します。これは、式の評価のコンテキストを表し、プログラムがブレークポイントで停止したときに存在します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- expression evaluation, context
ms.assetid: a2fd3758-09bd-45ae-8ecc-2d276c0036ba
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 73eeafb95c7e4d52f69109c5eb7c06eb48bd8d88
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901215"
---
# <a name="expression-evaluation-context"></a>式の評価のコンテキスト
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のデバッグでの **式の評価のコンテキスト** は:

- 式の評価のコンテキストを表します。 一般に、評価のコンテキストは、変数、パラメーター、関数、およびメソッドを評価する構文のスコープに対応します。 たとえば、スタック フレームに関連付けられた式の評価のコンテキストでは、ローカル変数、メソッド パラメーター、およびクラス メンバー (該当する場合) を評価するためのコンテキストが提供されます。

- プログラムがブレークポイントで停止したときに存在します。 式自体は、指定されたコンテキスト内でバインドおよび評価するための準備ができている解析済みの式を表すデータ構造体です。

     もっと詳しく言うと、式は [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) メソッドを使用して作成されます。 式が評価されると、変数または引数の名前と型、およびその値を含む出力可能な文字列が生成されます。 この文字列は、ウォッチ ウィンドウまたは IDE のローカル ウィンドウに表示されます。

     `BSTR` と [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) インターフェイスが指定されている場合、デバッグ エンジン (DE) では、式を解析することによって、[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスを作成できます。 `IDebugExpression2` インターフェイスが指定されている場合、DE では、同期または非同期の式の評価によって値を取得できます。 この値は、変数または引数の名前と型と共に、IDE に送信され、表示されます。

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [デバッガー コンテキスト](../../extensibility/debugger/debugger-contexts.md)
