---
title: IDebugProgramHost2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramHost2
helpviewer_keywords:
- IDebugProgramHost2 interface
ms.assetid: 2c37b3aa-97a9-4665-8709-edd917f18cb1
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dadbd74480c990c4e7317244ec225d775347a6c2
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56692802"
---
# <a name="idebugprogramhost2"></a>IDebugProgramHost2
このインターフェイスは、プログラムのホスト (プロセス) の情報を提供します。

## <a name="syntax"></a>構文

```
IDebugProgramHost2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 デバッグ エンジンと同じオブジェクトでこのインターフェイスを実装する、 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)ホスティング プロセスに関する情報を提供するインターフェイス。 これは、省略可能なインターフェイスです。

## <a name="notes-for-callers"></a>呼び出し元のノート
 呼び出す[QueryInterface](/cpp/atl/queryinterface)上、`IDebugProgram2`をこのインターフェイスを取得するインターフェイス。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、メソッドの`IDebugProgramHost2`します。

|メソッド|説明|
|------------|-----------------|
|[GetHostName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostname.md)|タイトル、フレンドリ名、またはこのプログラムのホスト プロセスのファイル名を取得します。|
|[GetHostId](../../../extensibility/debugger/reference/idebugprogramhost2-gethostid.md)|このプログラムのホスト プロセスのプロセス id を取得します。|
|[GetHostMachineName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostmachinename.md)|このプログラムのホスト プロセスが実行されているマシンの名前を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)