---
title: 型ビジュアライザーおよびカスタム ビューアーの実装 | Microsoft Docs
description: 型ビジュアライザーとカスタム ビューアーを実装する方法について説明します。これにより、ユーザーは大量の数値よりも意味のある方法でデータを表示できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], custom viewer
- debugging [Debugging SDK], type visualizer
ms.assetid: abef18c0-8272-4451-b82a-b4624edaba7d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 79df5f6c7bf11c791f8de415f7cf1532321ed57a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059783"
---
# <a name="implement-type-visualizers-and-custom-viewers"></a>型ビジュアライザーおよびカスタム ビューアーの実装
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 型ビジュアライザーおよびカスタム ビューアーを使用すると、特定の型のデータを、単純な大量の 16 進数の数値よりもわかりやすい方法で表示できます。 式エバリュエーター (EE) では、カスタム ビューアーを特定の種類のデータまたは変数に関連付けることができます。 これらのカスタム ビューアーは、EE によって実装されます。 EE では外部型ビジュアライザーもサポートされていますが、これは別のサードパーティ ベンダーまたはエンド ユーザーのものである可能性があります。

## <a name="discussion"></a>ディスカッション

### <a name="type-visualizers"></a>型ビジュアライザー
 Visual Studio では、ウォッチ ウィンドウに表示するすべてのオブジェクトについて、型ビジュアライザーとカスタム ビューアーの一覧が要求されます。 式エバリュエーター (EE) から、型ビジュアライザーおよびカスタム ビューアーをサポートするために必要なすべての型のリストが提供されます。 [GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md) と [GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) を呼び出すと、型ビジュアライザーとカスタム ビューアーにアクセスするプロセス全体が開始されます (「呼び出しシーケンスの詳細については、「[データの視覚化と表示](../../extensibility/debugger/visualizing-and-viewing-data.md)」を参照してください)。

### <a name="custom-viewers"></a>カスタム ビューアー
 カスタム ビューアーは、特定のデータ型に対して EE で実装され、[IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md) インターフェイスによって表されます。 カスタム ビューアーは、その特定のカスタム ビューアーを実装する EE が実行されている場合にのみ使用できるため、型ビジュアライザーほど柔軟ではありません。 カスタム ビューアーの実装は、型ビジュアライザーのサポートを実装するよりも簡単です。 ただし、型ビジュアライザーをサポートすると、エンド ユーザーがデータを視覚化するための柔軟性が最大限に高まります。 この説明の残りの部分では、型ビジュアライザーのみを考慮します。

## <a name="interfaces"></a>インターフェイス
 EE により、Visual Studio で使用される型ビジュアライザーをサポートするために、次のインターフェイスが実装されます。

- [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)

- [IPropertyProxyEESide](../../extensibility/debugger/reference/ipropertyproxyeeside.md)

- [IPropertyProxyProvider](../../extensibility/debugger/reference/ipropertyproxyprovider.md)

- [IEEDataStorage](../../extensibility/debugger/reference/ieedatastorage.md)

- [IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md)

- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)

  EE では、型ビジュアライザーをサポートするために次のインターフェイスが使用されます。

- [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)

- [IEEVisualizerServiceProvider](../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)

- [IDebugBinder3](../../extensibility/debugger/reference/idebugbinder3.md)

## <a name="see-also"></a>関連項目
- [CLR 式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [データの視覚化と表示](../../extensibility/debugger/visualizing-and-viewing-data.md)
- [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)
