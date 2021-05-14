---
description: マネージド コード ジェネリックをサポートするために使用できるフィールドの型を拡張します。
title: IDebugExtendedField | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugExtendedField interface
ms.assetid: b491499c-af57-47da-87d6-34b7398f6591
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d8214703fb1ffc05d3f58f8348870a8505cc8f59
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077188"
---
# <a name="idebugextendedfield"></a>IDebugExtendedField
マネージド コード ジェネリックをサポートするために使用できるフィールドの型を拡張します。

## <a name="syntax"></a>構文

```
IDebugExtendedField : IDebugField
```

## <a name="methods"></a>メソッド
 このインターフェイスには、[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスのメソッドに加えて、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[GetExtendedKind](../../../extensibility/debugger/reference/idebugextendedfield-getextendedkind.md)|指定された拡張フィールドの種類を取得します。|
|[IsClosedType](../../../extensibility/debugger/reference/idebugextendedfield-isclosedtype.md)|フィールドが終了型を表すかどうかを決定します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
