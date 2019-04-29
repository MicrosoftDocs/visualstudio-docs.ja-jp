---
title: IDebugPortSupplierLocale2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierLocale2 interface
ms.assetid: 910e7220-da2a-4339-9fff-9fb1bad3c28c
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 252c1e39af112b305b66a92fcfc3f329b743eae0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62917908"
---
# <a name="idebugportsupplierlocale2"></a>IDebugPortSupplierLocale2
ポート サプライヤーのロケールのサポートを提供します。

## <a name="syntax"></a>構文

```
IDebugPortSupplierLocale2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 カスタム ポート サプライヤーは、ロケールを設定するには、このインターフェイスを実装します。

## <a name="methods"></a>メソッド
 次の表は、メソッドの**IDebugPortSupplierLocale2**します。

|メソッド|説明|
|------------|-----------------|
|[SetLocale](../../../extensibility/debugger/reference/idebugportsupplierlocale2-setlocale.md)|ポート サプライヤーのロケールを設定します。|

## <a name="requirements"></a>必要条件
 ヘッダー:Portpriv.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)