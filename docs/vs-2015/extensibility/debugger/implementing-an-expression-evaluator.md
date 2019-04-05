---
title: 式エバリュエーターの実装 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators
- debugging [Debugging SDK], expression evaluators
ms.assetid: e9ada7be-845e-4baa-bf8f-e4890e7ba490
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b075a674d56dc7f1e79fdd03b31601b79f0b3f6e
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58973623"
---
# <a name="implementing-an-expression-evaluator"></a>式エバリュエーターの実装
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
>  Visual Studio 2015 での式エバリュエーターの実装には、この方法は非推奨とされます。 CLR 式エバリュエーターの実装方法の詳細についてを参照してください[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)します。  
  
 デバッグ エンジン (DE)、シンボル プロバイダー (SP)、バインダー オブジェクト、および、式エバリュエーター自体 (EE) の間で複雑な相互作用は、式を評価します。 これら 4 つのコンポーネントは、1 つのコンポーネントによって実装され、別で使用されるインターフェイスで接続されます。  
  
 EE は、文字列の形式で DE から式を取得および解析または評価します。 EE は、DE によって使用される次のインターフェイスを実装します。  
  
- [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)  
  
- [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)  
  
  EE は、シンボルとオブジェクトの値を取得する、DE、によって提供されるバインダー オブジェクトを呼び出します。 EE、DE によって実装される次のインターフェイスを使用します。  
  
- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)  
  
- [IDebugArrayObject](../../extensibility/debugger/reference/idebugarrayobject.md)  
  
- [IDebugFunctionObject](../../extensibility/debugger/reference/idebugfunctionobject.md)  
  
- [IDebugPointerObject](../../extensibility/debugger/reference/idebugpointerobject.md)  
  
- [IDebugManagedObject](../../extensibility/debugger/reference/idebugmanagedobject.md)  
  
- [IEnumDebugObjects](../../extensibility/debugger/reference/ienumdebugobjects.md)  
  
- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)  
  
  EE 実装[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)します。 `IDebugProperty2` ローカル変数、プリミティブ型、型の適切な情報が表示されますが、Visual Studio に、オブジェクトなど、式の評価の結果を記述するためのメカニズムを提供、**ローカル**、 **ウォッチ**、または**イミディ エイト**ウィンドウ。  
  
  SP は、情報の入力を求められたらときに、DE、EE に付与されます。 SP は、アドレスと、次のインターフェイスおよびその派生物などのフィールドを記述するインターフェイスを実装します。  
  
- [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)  
  
- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)  
  
- [IDebugField](../../extensibility/debugger/reference/idebugfield.md)  
  
  EE は、これらのインターフェイスのすべてを使用します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [式エバリュエーターの実装方法](../../extensibility/debugger/expression-evaluator-implementation-strategy.md)  
 式エバリュエーター (EE) の実装方法の 3 つの手順を定義します。  
  
## <a name="see-also"></a>関連項目  
 [CLR 式エバリュエーターの書き込み](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
