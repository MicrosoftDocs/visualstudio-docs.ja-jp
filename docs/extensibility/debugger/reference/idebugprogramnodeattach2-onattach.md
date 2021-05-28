---
description: 関連付けられているプログラムにアタッチするか、Attach メソッドまでアタッチ プロセスを延期します。
title: IDebugProgramNodeAttach2::OnAttach | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNodeAttach2::OnAttach
helpviewer_keywords:
- IDebugProgramNodeAttach2::OnAttach
ms.assetid: 5fe52761-a508-4ab5-abdb-334fb6590334
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 334a8e4bdf559e2d39d52a03dcf1a849f73af3e8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087263"
---
# <a name="idebugprogramnodeattach2onattach"></a>IDebugProgramNodeAttach2::OnAttach
関連付けられているプログラムにアタッチするか、[Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドまでアタッチ プロセスを延期します。

## <a name="syntax"></a>構文

```cpp
HRESULT OnAttach(
   [in] REFGUID guidProgramId
);
```

```csharp
int OnAttach(
   ref Guid guidProgramId
};
```

## <a name="parameters"></a>パラメーター
`guidProgramId`\
[入力] 関連付けられているプログラムに割り当てる `GUID`。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドを呼び出すことができない場合は、`S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドが呼び出される前に、アタッチ処理中にこのメソッドが呼び出されます。 `OnAttach` メソッドではアタッチ プロセス自体を実行したり (この場合は、このメソッドから `S_FALSE` が返されます)、`IDebugEngine2::Attach` メソッドまでアタッチ プロセスを延期したりすることができます (`OnAttach` メソッドから `S_OK` が返されます)。 いずれの場合も、`OnAttach` メソッドでは、デバッグされているプログラムの `GUID` を指定された `GUID` に設定できます。

## <a name="see-also"></a>関連項目
- [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [[アタッチ]](../../../extensibility/debugger/reference/idebugengine2-attach.md)
