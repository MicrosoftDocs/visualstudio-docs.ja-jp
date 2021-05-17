---
description: このインターフェイスを使用すると、呼び出し元が、デバッガーの呼び出しの間にポート サプライヤーがポートを (ディスクに書き込むことによって) 保持できるかどうかを判断し、保持されたポートの一覧を取得することができます。
title: IDebugPortSupplier3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier3
helpviewer_keywords:
- IDebugPortSupplier3 interface
ms.assetid: e458cd02-2370-4435-8953-17d7a60ce152
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fa17984c9b7f3e87d4a7118188ecc6ca79c5deef
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071936"
---
# <a name="idebugportsupplier3"></a>IDebugPortSupplier3
このインターフェイスを使用すると、呼び出し元が、デバッガーの呼び出しの間にポート サプライヤーがポートを (ディスクに書き込むことによって) 保持できるかどうかを判断し、保持されたポートの一覧を取得することができます。

## <a name="syntax"></a>構文

```
IDebugPortSupplier3 : IDebugPortSupplier2
```

## <a name="notes-for-implementers"></a>実装側の注意
 カスタム ポート サプライヤーは、このインターフェイスを実装して、ディスクへのポート情報の永続化または保存をサポートします。 このインターフェイスは、[IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md) インターフェイスと同じオブジェクトに実装する必要があります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスを取得するには、`IDebugPortSupplier2` インターフェイスの [QueryInterface](/cpp/atl/queryinterface) を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスは、 [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md) インターフェイスから継承したメソッドに加えて、次の機能をサポートしています。

|メソッド|説明|
|------------|-----------------|
|[CanPersistPorts](../../../extensibility/debugger/reference/idebugportsupplier3-canpersistports.md)|ポート サプライヤーが、デバッガーの呼び出しの間にポートを (ディスクに書き込むことによって) 永続化できるかどうかを返します。|
|[EnumPersistedPorts](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md)|このポート サプライヤーによってディスクに書き込まれたすべてのポートを列挙するために使用できるオブジェクトを返します。|

## <a name="remarks"></a>解説
 ポート サプライヤーは、呼び出しの間にポートを永続化できる場合は、このインターフェイスを実装する必要があります。 ポートは、ポート サプライヤーがインスタンス化されたときに読み込まれ、ポート サプライヤーが破棄されたときにディスクに書き込まれる必要があります。

 通常、デバッグ エンジンは、ポート サプライヤーとは連携しないため、このインターフェイスを使用することはありません。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
