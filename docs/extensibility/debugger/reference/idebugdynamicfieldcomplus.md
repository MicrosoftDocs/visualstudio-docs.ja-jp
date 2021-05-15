---
description: IDebugBinder オブジェクトの動的フィールドを表します。
title: IDebugDynamicFieldCOMPlus | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDynamicFieldCOMPlus interface
ms.assetid: c3a25f27-327a-4bdb-b026-27d436ddcd0c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f365bcadba5349ae43e1b75683ec100fdabbf338
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094017"
---
# <a name="idebugdynamicfieldcomplus"></a>IDebugDynamicFieldCOMPlus
[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) オブジェクトの動的フィールドを表します。

## <a name="syntax"></a>構文

```
IDebugDynamicFieldCOMPlus : IDebugDynamicField
```

## <a name="methods"></a>メソッド
 このインターフェイスでは、[IDebugDynamicField](../../../extensibility/debugger/reference/idebugdynamicfield.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[GetTypeFromPrimitive](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus-gettypefromprimitive.md)|プリミティブ型を指定して型を取得します。|
|[GetTypeFromTypeDef](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus-gettypefromtypedef.md)|トークンを指定して型を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
