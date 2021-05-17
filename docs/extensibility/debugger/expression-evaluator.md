---
title: 式エバリュエーター | Microsoft Docs
description: 中断モードでの実行時に言語の構文を調べ、変数と式を解析して評価する式エバリュエーターについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expressions [Debugging SDK]
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: f9381b2f-99aa-426c-aea0-d9c15f3c859b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6876bea4174df7f5ac293ea0d470f5922d7492d8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055025"
---
# <a name="expression-evaluator"></a>式エバリュエーター
式エバリュエーター (EE) によって実行時に言語の構文を調べ、変数と式を解析して評価すると、IDE が中断モードのときにユーザーがこれらを確認できるようになります。

## <a name="use-expression-evaluators"></a>式エバリュエーターを使用する
 式は、次のように [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) メソッドを使用して作成されます。

1. デバッグ エンジン (DE) で、[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) インターフェイスを実装します。

2. デバッグ パッケージで、[IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) インターフェイスから `IDebugExpressionContext2` オブジェクトを取得した後、その `IDebugStackFrame2::ParseText` メソッドを呼び出して [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) オブジェクトを取得します。

3. デバッグ パッケージで、[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) メソッドまたは [EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) メソッドを呼び出して、式の値を取得します。 `IDebugExpression2::EvaluateAsync` は、[コマンド] または [イミディエイト] ウィンドウから呼び出されます。 他のすべての UI コンポーネントでは、`IDebugExpression2::EvaluateSync` が呼び出されます。

4. 式の評価結果は [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトです。これには、式の評価結果の名前、型、値が含まれています。

   EE では、式の評価時にシンボル プロバイダー コンポーネントからの情報が必要です。 シンボル プロバイダーによって、解析された式を識別して理解するために使用されるシンボリック情報が提供されます。

   非同期の式の評価が完了すると、DE からセッション デバッグ マネージャー (SDM) を介して非同期イベントが送信され、式の評価が完了したことが IDE に通知されます。 また、その後、評価の結果が `IDebugExpression2::EvaluateSync` メソッドの呼び出しから返されます。

## <a name="implementation-notes"></a>実装に関するメモ
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッグ エンジンでは、共通言語ランタイム (CLR) インターフェイスを使用して式エバリュエーターと通信することが想定されています。 その結果、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッグ エンジンと連携する式エバリュエーターでは、CLR をサポートする必要があります (すべての CLR デバッグ インターフェイスの完全な一覧については、[!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)] の一部である debugref.doc を参照してください)。

## <a name="see-also"></a>関連項目
- [デバッガー コンポーネント](../../extensibility/debugger/debugger-components.md)
