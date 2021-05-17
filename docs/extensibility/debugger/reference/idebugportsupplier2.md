---
description: このインターフェイスは、セッション デバッグ マネージャー (SDM) にポートを提供します。
title: IDebugPortSupplier2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2
helpviewer_keywords:
- IDebugPortSupplier2 interface
ms.assetid: 37067324-2ea6-4a01-8829-a6e9c7a70068
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bd28e261c9c74601bd88f2d84e1296a1ed508f37
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072027"
---
# <a name="idebugportsupplier2"></a>IDebugPortSupplier2
このインターフェイスは、セッション デバッグ マネージャー (SDM) にポートを提供します。

## <a name="syntax"></a>構文

```
IDebugPortSupplier2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
カスタム ポート サプライヤーは、このインターフェイスを実装してポート サプライヤーを表します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
ポート サプライヤーの `GUID` で `CoCreateInstance` を呼び出すと、このインターフェイスが返されます (これは、このインターフェイスを取得するための一般的な方法です)。 次に例を示します。

```cpp
IDebugPortSupplier2 *GetPortSupplier(GUID *pPortSupplierGuid)
{
    IDebugPortSupplier2 *pPS = NULL;
    if (pPortSupplierGuid != NULL) {
        CComPtr<IDebugPortSupplier2> spPortSupplier;
        spPortSupplier.CoCreateInstance(*pPortSupplierGuid);
        if (spPortSupplier != NULL) {
            pPS = spPortSupplier.Detach();
        }
    }
    return (pPS);
}
```

[GetPortSupplier](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md) を呼び出すと、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] によって使用されている現在のポート サプライヤーを表す、このインターフェイスが返され ます。

- [GetportSupplier](../../../extensibility/debugger/reference/idebugport2-getportsupplier.md) は、ポートを作成したポート サプライヤーを表す、このインターフェイスを返します。

- [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md) は、`IDebugPortSupplier` インターフェイスの一覧を表します (`IEnumDebugPortSuppliers`インターフェイスは、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] に登録されているすべてのポート サプライヤーを表す [EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md) から取得されます)。

デバッグ エンジンは、通常、ポート サプライヤーとは連携しません。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表に、`IDebugPortSupplier2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetPortSupplierName](../../../extensibility/debugger/reference/idebugportsupplier2-getportsuppliername.md)|ポート サプライヤー名を取得します。|
|[GetPortSupplierId](../../../extensibility/debugger/reference/idebugportsupplier2-getportsupplierid.md)|ポート サプライヤー識別子を取得します。|
|[GetPort](../../../extensibility/debugger/reference/idebugportsupplier2-getport.md)|ポート サプライヤーからポートを取得します。|
|[EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)|既に存在するポートを列挙します。|
|[CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)|新しいポートの追加をポート サプライヤーがサポートしていることを確認します。|
|[AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)|ポートを追加します。|
|[RemovePort](../../../extensibility/debugger/reference/idebugportsupplier2-removeport.md)|ポートを削除します。|

## <a name="remarks"></a>解説
ポート サプライヤーは、名前と ID で自身を識別したり、ポートの追加と削除を行ったり、ポート サプライヤーが提供するすべてのポートを列挙したりできます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetPortSupplier](../../../extensibility/debugger/reference/idebugport2-getportsupplier.md)
- [GetPortSupplier](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)
- [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md)
