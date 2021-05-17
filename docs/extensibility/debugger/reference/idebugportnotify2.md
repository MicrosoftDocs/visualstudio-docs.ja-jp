---
description: このインターフェイスは、実行中のポートでデバッグできるプログラムを登録または登録解除します。
title: IDebugPortNotify2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortNotify2
helpviewer_keywords:
- IDebugPortNotify2 interface
ms.assetid: 43278b79-bf16-4c08-bcf1-6f7f7a17feab
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a4000426b72472d57b589f26543dd1547f8dc982
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072391"
---
# <a name="idebugportnotify2"></a>IDebugPortNotify2
このインターフェイスは、実行中のポートでデバッグできるプログラムを登録または登録解除します。

## <a name="syntax"></a>構文

```
IDebugPortNotify2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 カスタム ポート サプライヤーは、このインターフェイスを実装して、ポートからのプログラムの追加と削除をサポートします。 通常、[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) インターフェイスを実装するのと同じオブジェクトに実装されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 `IDebugPort2` インターフェイスで [QueryInterface](/cpp/atl/queryinterface) を呼び出すと、このインターフェイスが返されます。 また、[Getportnotify](../../../extensibility/debugger/reference/idebugdefaultport2-getportnotify.md) を呼び出すと、このインターフェイスが返されます。 デバッグ エンジンでは、[WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md) のパラメーターとしてこのインターフェイスを参照できます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugPortNotify2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[AddProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)|デバッグ可能なプログラムを、実行中のポートに登録します。|
|[RemoveProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md)|デバッグ可能なプログラムを、実行中のポートから登録解除します。|

## <a name="remarks"></a>解説
 プログラムがロードまたはアンロードされるタイミングをデバッグ ポートで認識する方法がない限り、カスタム ポート サプライヤーではこのインターフェイスを実装する必要があります。 特定のポートを介してデバッグするために読み込まれるすべてのプログラムは、このインターフェイスを使用して追跡されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
