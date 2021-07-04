---
title: 型ビジュアライザーとカスタム ビューアー |Microsoft Docs
description: 型ビジュアライザー コンポーネントとカスタム ビューアーについて説明します。このビューアーには、データが特定の形式で表示され、それらの違いが表示されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], custom viewer
- debugging [Debugging SDK], type visualizer
ms.assetid: fd3691e6-9c78-4767-846f-43f85ada4375
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c18bb49c740362d42a4a54bf52f6998629acb0c0
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904423"
---
# <a name="type-visualizer-and-custom-viewer"></a>型ビジュアライザーとカスタム ビューアー
型ビジュアライザーは、特定の形式でデータを表示するコンポーネントです。 この形式は、エンドユーザーまたはビジュアライザーのサードパーティ サプライヤーなど、ビジュアライザーを実装しているユーザー次第です。

 カスタム ビューアーは、特定の形式でデータを表示するカスタム式エバリュエーターの一部です。 この形式は、完全にカスタム ビューアーの実装者次第です。つまり、形式は式エバリュエーター (EE) の実装者次第です。

## <a name="support-for-type-visualizers-in-an-expression-evaluator"></a>式エバリュエーターでの型ビジュアライザーのサポート
 EE では、ビジュアライザーからアクセスできるインターフェイスのセット ([IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md) や [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md) などのインターフェイス) をサポートすることで、型ビジュアライザーをサポートしています。 ただし、EE では型ビジュアライザー自体を実装する責任を負いません。 EE は、外部ビジュアライザーから型情報にアクセスすることを許可するだけです。 このようなビジュアライザーは、EE と共に出荷され、別のサードパーティ ベンダーまたはエンド ユーザーが提供する Visual Studio の適切な場所にインストールされる場合があります。

## <a name="support-for-custom-viewers-in-an-expression-evaluator"></a>式エバリュエーターでのカスタム ビューアーのサポート
 EE では、データ型を表示するためのコードを提供するカスタム ビューアーをサポートすることもできます。 カスタム ビューアーは、必要な形式でデータを表示するすべての作業を処理する [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md) インターフェイスを実装します。ビューアーから表示を完全に制御でき、またデータを変更することもできます。 EE によって提供されるカスタム ビューアーには、製品の出荷時に EE が付属しています。

## <a name="see-also"></a>関連項目
- [デバッガー コンポーネント](../../extensibility/debugger/debugger-components.md)
- [式エバリュエーター](../../extensibility/debugger/expression-evaluator.md)
- [デバッグ エンジン](../../extensibility/debugger/debug-engine.md)
- [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)
- [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)
- [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
