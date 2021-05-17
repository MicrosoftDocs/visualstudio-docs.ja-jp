---
description: このインターフェイスから、プログラムに関するホスト (プロセス) 情報が提供されます。
title: IDebugProgramHost2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramHost2
helpviewer_keywords:
- IDebugProgramHost2 interface
ms.assetid: 2c37b3aa-97a9-4665-8709-edd917f18cb1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6b58eb61a65ff8ed0a6455d81128539ad5e6d00a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058249"
---
# <a name="idebugprogramhost2"></a>IDebugProgramHost2
このインターフェイスから、プログラムに関するホスト (プロセス) 情報が提供されます。

## <a name="syntax"></a>構文

```
IDebugProgramHost2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 ホスト プロセスに関する情報を提供するため、デバッグ エンジンにより [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスと同じオブジェクトにこのインターフェイスが実装されます。 これは、省略可能なインターフェイスです。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 `IDebugProgram2` インターフェイスを取得するには、このインターフェイスの [QueryInterface](/cpp/atl/queryinterface) を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugProgramHost2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetHostName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostname.md)|このプログラムのホスト プロセスのタイトル、フレンドリ名、またはファイル名を取得します。|
|[GetHostId](../../../extensibility/debugger/reference/idebugprogramhost2-gethostid.md)|このプログラムをホストしているプロセスのプロセス識別子を取得します。|
|[GetHostMachineName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostmachinename.md)|このプログラムのホスト プロセスが実行されているマシンの名前を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
