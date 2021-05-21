---
description: このインターフェイスは変数の型を表します。
title: IDebugDynamicField | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDynamicField
helpviewer_keywords:
- IDebugDynamicField interface
ms.assetid: caffbd95-7596-4714-84b1-b964e89a78bb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bf1d72bfa38e6af0419e696b267699d10340cc68
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094082"
---
# <a name="idebugdynamicfield"></a>IDebugDynamicField
このインターフェイスは変数の型を表します。

## <a name="syntax"></a>構文

```
IDebugDynamicField : IDebugField
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、実行時に決定できる任意の型の基底クラスとしてシンボル プロバイダーによって実装されます。 これはマネージド コード専用です。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、より特殊化されたインターフェイスを派生できる基底クラスを表します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスでは、`IDebugField` から継承されたメソッド以外のものは提供されません。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
