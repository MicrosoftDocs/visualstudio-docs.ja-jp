---
title: ローカルの実装のサンプル | Microsoft Docs
description: この記事では、Visual Studio がメソッドのローカルを式エバリュエーターから取得する方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], local variables
- expression evaluation, local variables
ms.assetid: 66a2e00a-f558-4e87-96b8-5ecf5509e04c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4bf07dc6f47391af14c878021c742c2cb461bc85
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070415"
---
# <a name="sample-implementation-of-locals"></a>ローカルの実装のサンプル
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 Visual Studio がメソッドのローカルを式エバリュエーター (EE) から取得する方法の概要を、以下に示します。

1. Visual Studio は、デバッグ エンジン (DE) の [GetDebugProperty](../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) を呼び出して、ローカルを含むスタック フレームのすべてのプロパティを表す [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトを取得します。

2. `IDebugStackFrame2::GetDebugProperty` は、[Getmethodproperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) を呼び出して、ブレークポイントが内部で発生したメソッドを説明するオブジェクトを取得します。 DE は、シンボル プロバイダー ([IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md))、アドレス ([IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md))、バインダー ([IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)) を提供します。

3. `IDebugExpressionEvaluator::GetMethodProperty` は、提供された `IDebugAddress` オブジェクトで [GetContainerField](../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md) を呼び出し、指定されたアドレスを含むメソッドを表す [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md) を取得します。

4. `IDebugContainerField` インターフェイスは、[IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) インターフェイスについて照会されます。 このインターフェイスが、メソッドのローカルへのアクセスを提供します。

5. `IDebugExpressionEvaluator::GetMethodProperty` は、メソッドのローカルを表す `IDebugProperty2` インターフェイスを実行するクラス (サンプルでは `CFieldProperty` と呼ばれます) をインスタンス化します。 `IDebugMethodField` オブジェクトは、`IDebugSymbolProvider`、`IDebugAddress`、および `IDebugBinder` の各オブジェクトと共に、この `CFieldProperty` オブジェクトに配置されます。

6. `CFieldProperty` オブジェクトが初期化されると、`IDebugMethodField` オブジェクトで [GetInfo](../../extensibility/debugger/reference/idebugfield-getinfo.md) が呼び出されて、メソッド自体に関する表示可能なすべての情報を含む [FIELD_INFO](../../extensibility/debugger/reference/field-info.md) 構造が取得されます。

7. `IDebugExpressionEvaluator::GetMethodProperty` は、`CFieldProperty` オブジェクトを `IDebugProperty2` オブジェクトとして返します。

8. Visual Studio は、`guidFilterLocalsPlusArgs` フィルターを使用して、返された `IDebugProperty2` オブジェクトで [Enumchildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) を呼び出し、メソッドのローカルを含む [IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) オブジェクトが返されます。 この列挙体は、[Enumlocals](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md) と [EnumArguments](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md) への呼び出しによって入力されます。

9. Visual Studio は、 [Next](../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md) を呼び出して、各ローカルの [DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md) 構造を取得します。 この構造には、ローカルの `IDebugProperty2` インターフェイスへのポインターが含まれています。

10. Visual Studio は、各ローカルの [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) を呼び出して、ローカルの名前、値、および型を取得します。 この情報は、 **[ローカル]** ウィンドウに表示されます。

## <a name="in-this-section"></a>このセクションの内容
 「[GetMethodProperty を実装する](../../extensibility/debugger/implementing-getmethodproperty.md)」では、[GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) の実装について説明します。

 「[ローカルを列挙する](../../extensibility/debugger/enumerating-locals.md)」では、デバッグ エンジン (DE) が呼び出しを行って、ローカルの変数または引数を列挙する方法を説明します。

 「[ローカル プロパティを取得する](../../extensibility/debugger/getting-local-properties.md)」では、DE が呼び出しを行って、1 つ以上のローカルの名前、型、および値を取得する方法を説明します。

 「[ローカル値を取得する](../../extensibility/debugger/getting-local-values.md)」では、評価コンテキストで指定されたバインダー オブジェクトのサービスを必要とするローカルの値を取得する方法を説明します。

 「[ローカルを評価する](../../extensibility/debugger/evaluating-locals.md)」では、ローカルの評価方法を説明します。

## <a name="related-sections"></a>関連項目
 「[評価コンテキスト](../../extensibility/debugger/evaluation-context.md)」では、DE が式エバリュエーター (EE) を呼び出すときに渡される引数を示します。

 「[MyCEE のサンプル](/previous-versions/)」では、MyC 言語の式エバリュエーターを作成するための 1 つの実装方法を示します。

## <a name="see-also"></a>関連項目
- [ローカルの表示](../../extensibility/debugger/displaying-locals.md)