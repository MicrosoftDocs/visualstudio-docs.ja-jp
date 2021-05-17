---
description: このインターフェイスは、他のシンボルまたは型のコンテナーであるシンボルまたは型を表します。
title: IDebugContainerField | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugContainerField
helpviewer_keywords:
- IDebugContainerField interface
ms.assetid: a8bbe061-c382-4fe9-a193-3f7d12216041
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bb3a50db80dc2acb075d1c6ec1fe585000468285
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077903"
---
# <a name="idebugcontainerfield"></a>IDebugContainerField
このインターフェイスは、他のシンボルまたは型のコンテナーであるシンボルまたは型を表します。

## <a name="syntax"></a>構文

```
IDebugContainerField : IDebugField
```

## <a name="notes-for-implementers"></a>実装側の注意
 シンボル プロバイダーでは、[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスを実装するのと同じオブジェクトにこのインターフェイスを実装します。 このインターフェイスは、コンテナーを表すすべてのインターフェイスの基本クラスでもあります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 多くのインターフェイスでは、多くのメソッドからこのインターフェイスを返します。 これはすべてのコンテナーの基本クラスであるため、[QueryInterface](/cpp/atl/queryinterface) を使用して、このインターフェイスからより特殊なインターフェイスを取得できます。 そのようなインターフェイスには、[IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)、[IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)、[IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)、および [IDebugPropertyField](../../../extensibility/debugger/reference/idebugpropertyfield.md) があります。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスには、[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスのメソッドに加えて、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[EnumFields](../../../extensibility/debugger/reference/idebugcontainerfield-enumfields.md)|コンテナーのフィールドの列挙子を作成します。|

## <a name="remarks"></a>解説
 配列 (変数のコンテナー)、クラス (メソッドと変数のコンテナー)、およびメソッド (パラメーターとローカル変数のコンテナー) はすべて、コンテナーの例です。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
