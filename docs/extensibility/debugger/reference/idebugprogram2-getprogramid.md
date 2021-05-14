---
description: このプログラムの GUID を取得します。
title: IDebugProgram2::GetProgramId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetProgramId
helpviewer_keywords:
- IDebugProgram2::GetProgramId
ms.assetid: 2c31c0aa-2b71-46c7-849c-356e237d26f8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ad0b5c8af1723414e6805e362312f167f995fbe4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084507"
---
# <a name="idebugprogram2getprogramid"></a>IDebugProgram2::GetProgramId
このプログラムの GUID を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetProgramId( 
   GUID* pguidProgramId
);
```

```csharp
int GetProgramId( 
   out Guid pguidProgramId
);
```

## <a name="parameters"></a>パラメーター
`pguidProgramId`\
[out] このプログラムの `GUID` を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 デバッグ エンジン (DE) からは、[OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) または [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドに最初に渡されたプログラム ID が返される必要があります。 これにより、デバッガー コンポーネント間でプログラムを識別できます。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)
- [[アタッチ]](../../../extensibility/debugger/reference/idebugengine2-attach.md)
