---
title: ローカルの値の変更 | Microsoft Docs
description: '[ローカル] ウィンドウの [値] フィールドに新しい値が入力されたときにローカルの値を変更するプロセスについて説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, changing values programmatically
ms.assetid: 8407d3df-d38a-4328-82d1-98084bef43ec
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d8baac2f0e288e9bde1288ed72e43d7f1d150d04
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055077"
---
# <a name="change-the-value-of-a-local"></a>ローカルの値を変更する
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 デバッグ パッケージでは、 **[ローカル]** ウィンドウの [値] フィールドに新しい値が入力されたときに、入力された文字列を式エバリュエーター (EE) に渡します。 EE では、単純な値と式のいずれかを含むこの文字列を評価し、結果の値を関連付けられたローカルに格納します。

 ここでは、ローカルの値を変更するプロセスの概要を示します。

1. ユーザーが新しい値を入力すると、Visual Studio で、ローカルに関連付けられた [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトの [SetValueAsString](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md) が呼び出されます。

2. `IDebugProperty2::SetValueAsString` では次のタスクを実行します。

   1. 文字列を評価して値を生成します。

   2. 関連付けられた [IDebugField](../../extensibility/debugger/reference/idebugfield.md) オブジェクトをバインドして、[IDebugObject](../../extensibility/debugger/reference/idebugobject.md) オブジェクトを取得します。

   3. 値を一連のバイトに変換します。

   4. [SetValue](../../extensibility/debugger/reference/idebugobject-setvalue.md) を呼び出して値のバイトをメモリに格納し、デバッグ中のプログラムからアクセスできるようにします。

3. Visual Studio の **[ローカル]** の表示が更新されます (詳細については、「[ローカルの表示](../../extensibility/debugger/displaying-locals.md)」を参照してください)。

   この手順は、 **[ウォッチ]** ウィンドウの変数の値を変更する場合にも使用されます。ただし、ローカル自体に関連付けられた `IDebugProperty2` オブジェクトではなく、使用されるローカルの値に関連付けられた `IDebugProperty2` オブジェクトである点が異なります。

## <a name="in-this-section"></a>このセクションの内容
 [値の変更の実装例](../../extensibility/debugger/sample-implementation-of-changing-values.md)では、MyCEE サンプルを使用して、値を変更するプロセスを段階的に実行します。

## <a name="see-also"></a>関連項目
- [CLR 式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [ローカルの表示](../../extensibility/debugger/displaying-locals.md)
