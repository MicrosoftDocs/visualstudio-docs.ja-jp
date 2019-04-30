---
title: IDebugPortEvents2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEvents2
helpviewer_keywords:
- IDebugPortEvents2 interface
ms.assetid: 2c017094-3ba2-4067-83f9-147df1d96bce
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fb6a13b47013153de284ad1997a484efb3be1c98
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62918328"
---
# <a name="idebugportevents2"></a>IDebugPortEvents2
このインターフェイスは、プロセスとプログラムの作成と破棄を特定のポートでのリスナー (通常、セッション デバッグ マネージャー [SDM] またはデバッグ エンジン) を通知します。 この情報は、ポートで実行されるプログラム、プロセスのリアルタイム ビューに表示できます。

## <a name="syntax"></a>構文

```
IDebugPortEvents2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 Visual Studio は、通常、プログラムの作成と破棄に関する通知を受信するには、このインターフェイスを実装します。 デバッグ エンジンは、このようなポート イベントをリッスンするには、このインターフェイスを実装もできます。

## <a name="notes-for-callers"></a>呼び出し元のノート
 すべて[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)のインターフェイスを照会できます、<xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer>インターフェイス。 次に、<xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer.FindConnectionPoint%2A>メソッドの`IDebugPortEvents2`で呼び出される、<xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer>インターフェイスを取得する、<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint>インターフェイス。 最後に、<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint.Advise%2A>メソッドで、<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint>インターフェイスが呼び出され、イベントを送信して、[イベント](../../../extensibility/debugger/reference/idebugportevents2-event.md)メソッド。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、メソッドの`IDebugPortEvents2`します。

|メソッド|説明|
|------------|-----------------|
|[Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)|作成とプロセスと、ポート上のプログラムの破棄を記述するイベントを送信します。|

## <a name="remarks"></a>Remarks
 `IDebugPortEvents2` 既にデバッグ中のプロセスで実行されるプログラムをデバッグする、SDM によってもに使用します。

 ポート イベントは、このインターフェイスによって、SDM に渡されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)