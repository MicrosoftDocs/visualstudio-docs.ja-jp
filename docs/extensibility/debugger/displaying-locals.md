---
title: ローカルの表示 | Microsoft Docs
description: ローカル変数と引数の一覧について説明します。これらは、実行が一時停止したときに表示される、メソッドのローカルと総称されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, displaying locals
ms.assetid: 62264cec-845b-4233-aed7-0b038fa79250
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 564b42a15e1420027b79cb5f00c70f61649ad4f9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097267"
---
# <a name="display-locals"></a>ローカルの表示
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 実行は常にメソッドのコンテキスト内で行われ、含むメソッドまたは現在のメソッドとも呼ばれます。 実行が一時停止すると、Visual Studio によって、デバッグ エンジン (DE) が呼び出され、ローカル変数と引数の一覧が取得されます。これらは、メソッドのローカルと総称されます。 Visual Studio で、これらのローカルとその値は、 **[ローカル]** ウィンドウに表示されます。

 ローカルを表示するために、DE によって、EE に属する [GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) メソッドが呼び出され、評価コンテキスト (つまり、シンボル プロバイダー (SP)、現在の実行アドレス、およびバインダー オブジェクト) が指定されます。 詳細については、「[評価コンテキスト](../../extensibility/debugger/evaluation-context.md)」を参照してください。 呼び出しが成功した場合、`IDebugExpressionEvaluator::GetMethodProperty` メソッドによって、現在の実行アドレスを含むメソッドを表す [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトが返されます。

 DE によって、[IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) オブジェクトを取得するために [EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) が呼び出されます。このオブジェクトは、ローカルのみを返すようにフィルター処理され、[DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md) 構造体のリストを生成するように列挙されます。 各構造体には、ローカルの名前、型、および値が含まれます。 型と値は、表示に適した書式設定された文字列として格納されます。 名前、型、および値は通常、 **[ローカル]** ウィンドウの 1 行にまとめて表示されます。

> [!NOTE]
> **[クイックウォッチ]** ウィンドウと **[ウォッチ]** ウィンドウにも、同じ形式の名前、値、および型で変数が表示されます。 ただし、それらの値を取得するには、`IDebugProperty2::EnumChildren` ではなく、[GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) を呼び出します。

## <a name="in-this-section"></a>このセクションの内容
 [ローカルのサンプル実装](../../extensibility/debugger/sample-implementation-of-locals.md) 例を使用して、ローカルを実装するプロセスをステップ実行します。

## <a name="related-sections"></a>関連項目
 [評価コンテキスト](../../extensibility/debugger/evaluation-context.md) デバッグエンジン (DE) によって式エバリュエーター (EE) が呼び出されるときに、3 つの引数が渡されることについて説明します。

## <a name="see-also"></a>関連項目
 [CLR 式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
