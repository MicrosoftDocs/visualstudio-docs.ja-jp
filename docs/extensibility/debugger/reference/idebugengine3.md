---
description: 1 つ以上のモジュールのデバッグを制御する単一のデバッグ エンジン (DE) を表します。
title: IDebugEngine3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3
helpviewer_keywords:
- IDebugEngine3 interface
ms.assetid: 8bdf4bb7-3b5d-4991-8981-772d4f6bb656
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3a10f439ba344b71cd31fd990928b7804b6c11d4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066191"
---
# <a name="idebugengine3"></a>IDebugEngine3
1 つ以上のモジュールのデバッグを制御する単一のデバッグ エンジン (DE) を表します。

## <a name="syntax"></a>構文

```
IDebugEngine3 : IDebugEngine2
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、JustMyCode 状態を有効にするために、(シンボルをサポートしている場合の) カスタム DE によって実装されます。 DE がシンボルと JustMyCode をサポートしている場合、このインターフェイスは DE によって実装される必要があります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、シンボルの読み込み元の場所に関するユーザー オプションを渡すために、セッション デバッグ マネージャー (SDM) によって呼び出されます。 また、エンジンがインスタンス化されるときにエンジンの GUID を設定するためにも呼び出されます (この GUID は、エンジン登録時のメトリックに基づいています)。 さらに SDM では、このインターフェイスを呼び出して、JustMyCode 状態を設定したり、デバッガーにとって既知であるすべての例外を指定された状態に設定したりします。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 `IDebugEngine3` インターフェイスでは、[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) から継承されたメソッドに加えて以下のメソッドが公開されます。

|メソッド|説明|
|------------|-----------------|
|[SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)|デバッグ シンボルの検索に DE が使用する 1 つ以上のパスを設定します。|
|[LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)|まだシンボルが読み込まれていないすべてのモジュールのシンボルを読み込みます。|
|[SetJustMyCodeState](../../../extensibility/debugger/reference/idebugengine3-setjustmycodestate.md)|JustMyCode 情報について DE に通知します。|
|[SetEngineGuid](../../../extensibility/debugger/reference/idebugengine3-setengineguid.md)|メトリックから DE の GUID を設定します。|
|[SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md)|現在未処理のすべての例外を指定された状態に設定します。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
