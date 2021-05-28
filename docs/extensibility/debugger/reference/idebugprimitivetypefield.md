---
description: IDebugField インターフェイスからのプリミティブ型の列挙値を表します。
title: IDebugPrimitiveTypeField | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPrimitiveTypeField interface
ms.assetid: 73a428fd-797e-4ceb-8392-ba16f1c5226b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 28abe0cb35074025263c684f9d9006fbfa7071c3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071728"
---
# <a name="idebugprimitivetypefield"></a>IDebugPrimitiveTypeField
[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスからのプリミティブ型の列挙値を表します。

## <a name="syntax"></a>構文

```
IDebugPrimitiveTypeField : IDebugField
```

## <a name="methods"></a>メソッド
 このインターフェイスには、[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスのメソッドに加えて、次のメソッドが実装されています。

|Method|説明|
|------------|-----------------|
|[GetPrimitiveType](../../../extensibility/debugger/reference/idebugprimitivetypefield-getprimitivetype.md)|このフィールドに関連付けられているプリミティブ型を取得します。|

## <a name="requirements"></a>要件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
