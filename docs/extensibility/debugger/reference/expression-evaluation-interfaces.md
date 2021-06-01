---
description: 次に示すのは、Visual Studio デバッグ SDK の式の評価のインターフェイスです。
title: 式の評価のインターフェイス | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- expression evaluation, interfaces
ms.assetid: 2d259f60-2cd7-460e-b02d-24a8fb202850
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 563e66f7aa7c2f8cf1e5573487690edc703ae5d8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059458"
---
# <a name="expression-evaluation-interfaces"></a>式の評価のインターフェイス
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 次に示すのは、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] デバッグ SDK の式の評価のインターフェイスです。

## <a name="discussion"></a>ディスカッション
 これらのインターフェイスは、中断モード中に呼び出し履歴の式を評価するために使用されます。 これらは共通言語ランタイム式エバリュエーター (EE) に対してのみ実装されます。

 この表の各インターフェイスには、それぞれを実装できる次の一覧のコンポーネントが示されます。

- デバッグ エンジン (DE)

- 式エバリュエーター (EE)

- Visual Studio (VS)

|インターフェイス|実装元|説明|
|---------------|--------------------|-----------------|
|[IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)|EE|変数の数値の別名を表します。|
|[IDebugAlias2](../../../extensibility/debugger/reference/idebugalias2.md)|EE|変数の数値の別名を表し、式エバリュエーター (EE) で別名のアプリケーション ドメインを取得できるようにします。|
|[IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)|EE|配列オブジェクトを表します。|
|[IDebugArrayObject2](../../../extensibility/debugger/reference/idebugarrayobject2.md)|EE|マネージド配列オブジェクトを表し、式エバリュエーター (EE) で配列のベース インデックス (下限) を決定できるようにします。|
|[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)|DE|デバッグ シンボルをメモリ内の実際のアドレスにバインドするバインダーを表します。|
|[IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)|DE|[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) インターフェイスと同じですが、型、別名およびカスタム ビジュアライザーへのアクセスが提供されます。|
|[IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)|EE|式エバリュエーターを表します。|
|[IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)|EE|式エバリュエーター (EE) の拡張バージョンを表します。|
|[IDebugExpressionEvaluator3](../../../extensibility/debugger/reference/idebugexpressionevaluator3.md)|EE|パーサー ツリーが拡張された式エバリュエーター (EE) を表します。|
|[IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)|EE|関数を表します。|
|[IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)|EE|関数を表し、[IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) インターフェイスを拡張します。|
|[IDebugIDECallback](../../../extensibility/debugger/reference/idebugidecallback.md)|DE|式エバリュエーター (EE) でデバッガーの出力ウィンドウにメッセージを表示できるようにします。|
|[IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)|EE|マネージド コード オブジェクトを表します。|
|[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)|EE|メモリ アドレスにバインドされている任意のシンボルを表す基底インターフェイス。|
|[IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)|EE|[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) インターフェイスと同じですが、追加情報へのアクセスが提供されます。|
|[IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)|EE|評価の準備ができている解析済みの式を表します。|
|[IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)|EE|ポインターを表します。|
|[IDebugPointerObject3](../../../extensibility/debugger/reference/idebugpointerobject3.md)|EE|解析ツリー内のポインターを表し、**IDebugPointerObject** インターフェイスを拡張します。|
|[IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)|EE|型ビジュアライザーを使用して型の値を変更する機能を提供します。|
|[IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)|VS|カスタム ビューアーおよび型ビジュアライザーへのアクセスを提供します。|
|[IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)|VS|[IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md) オブジェクトを作成する機能を提供します。|
|[IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md)|EE|[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトのコレクションを表します。|

## <a name="see-also"></a>こちらもご覧ください
- [API リファレンス](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
- [CLR 式エバリュエーターの書き込み](../../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [型のビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
