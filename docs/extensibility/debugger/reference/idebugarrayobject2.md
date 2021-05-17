---
description: マネージド配列オブジェクトを表し、式エバリュエーター (EE) で配列のベース インデックス (下限) を決定できるようにします。
title: IDebugArrayObject2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugArrayObject2 interface
ms.assetid: be6e504d-4ab3-4141-a61b-0953ee0e038e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 169f4df61bcd4a58e74e0d83cee362b3926d2b36
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067570"
---
# <a name="idebugarrayobject2"></a>IDebugArrayObject2
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 マネージド配列オブジェクトを表し、式エバリュエーター (EE) で配列のベース インデックス (下限) を決定できるようにします。

## <a name="syntax"></a>構文

```
IDebugArrayObject2 : IDebugArrayObject
```

## <a name="notes-for-implementers"></a>実装側の注意
 これは、マネージド デバッグ エンジン (DE) によって実装されます。

## <a name="methods"></a>メソッド
 このインターフェイスは、[IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md) インターフェイスのメソッドに加えて、次のメソッドを実装しています。

|メソッド|説明|
|------------|-----------------|
|[GetBaseIndices](../../../extensibility/debugger/reference/idebugarrayobject2-getbaseindices.md)|配列の次元数を指定して、各インデックスのベース インデックス (下限) を取得します。|
|[HasBaseIndices](../../../extensibility/debugger/reference/idebugarrayobject2-hasbaseindices.md)|配列にベース インデックス (下限) が定義されているかどうかを判断します。|

## <a name="remarks"></a>解説
 式エバリュエーターでは、このインターフェイスを使用して、マネージド配列を解析ツリーに表現します。

## <a name="requirements"></a>必要条件
 ヘッダー: Ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
