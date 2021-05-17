---
description: このインターフェイスは、特定のドキュメントに関連付けられているプロパティを作成するときに、デバッグ エンジン (DE) によってセッション デバッグ マネージャー (SDM) に送信されます。
title: IDebugPropertyCreateEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPropertyCreateEvent2
helpviewer_keywords:
- IDebugPropertyCreateEvent2 interface
ms.assetid: 33b3082b-a42e-488a-a1e4-dadf506f922c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6197420428bf07cecf2bfe891e06ddb7a830ea30
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083883"
---
# <a name="idebugpropertycreateevent2"></a>IDebugPropertyCreateEvent2
このインターフェイスは、特定のドキュメントに関連付けられているプロパティを作成するときに、デバッグ エンジン (DE) によってセッション デバッグ マネージャー (SDM) に送信されます。

## <a name="syntax"></a>構文

```
IDebugPropertyCreateEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、プロパティが作成されたことを報告するために DE によって実装されます。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 `IDebugEvent2` インターフェイスにアクセスするために SDM によって [QueryInterface](/cpp/atl/queryinterface) が使用されます。 このインターフェイスは、読み込みまたは作成されたスクリプトに関連付けられたプロパティを DE で作成した場合、およびそのスクリプトを IDE に表示する必要がある場合に実装されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このイベント オブジェクトは、プロパティが作成されたことを報告するために、DE によって作成および送信されます。 このイベントは、SDM がデバッグ中のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 `IDebugPropertyCreateEvent2` インターフェイストのメソッドを次の表に示します。

|メソッド|説明|
|------------|-----------------|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugpropertycreateevent2-getdebugproperty.md)|新しいプロパティを取得します。|

## <a name="remarks"></a>解説
 プロパティに特定のドキュメントまたはスクリプトが関連付けられている場合、DE では、 **[スクリプト ドキュメント]** ウィンドウをドキュメントの名前で更新するために、このイベントを SDM に送信することができます。 SDM では、引数 `guidDocument` を指定して [GetExtendedInfo](../../../extensibility/debugger/reference/idebugproperty2-getextendedinfo.md) を呼び出して、[IUnknown](/cpp/atl/iunknown) ポインターを含む `VARIANT` を取得します。 SDM では、このポインターの [QueryInterface](/cpp/atl/queryinterface) を呼び出して、 **[スクリプト ドキュメント]** ウィンドウの更新に使用される [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) インターフェイスを取得します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
