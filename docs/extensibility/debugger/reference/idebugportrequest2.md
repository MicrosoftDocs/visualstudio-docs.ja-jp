---
description: このインターフェイスによってポートが記述されます。
title: IDebugPortRequest2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortRequest2
helpviewer_keywords:
- IDebugPortRequest2 interface
ms.assetid: 556e610d-7c4b-44a8-965a-76a9d02b601a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 035b6364b3a1dea400c96bcf179d57d6b4808ad5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072222"
---
# <a name="idebugportrequest2"></a>IDebugPortRequest2
このインターフェイスによってポートが記述されます。 この説明を使用してポートがポート サプライヤーに追加されます。

## <a name="syntax"></a>構文

```
IDebugPortRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 通常、Visual Studio は、ポート サプライヤーからデバッグ ポートを取得するプロセスで、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスが [Addport](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md) に渡され、デバッグ ポートが作成されます。 [GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md) を呼び出すと、このインターフェイスが返されます。このインターフェイスは、最初にポートの作成に使用された要求を表します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugPortRequest2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetPortName](../../../extensibility/debugger/reference/idebugportrequest2-getportname.md)|作成するポートの名前を取得します。|

## <a name="remarks"></a>解説
 通常、デバッグ エンジンは、ポート サプライヤーとは連携しないため、このインターフェイスを使用することはありません。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
- [GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)
