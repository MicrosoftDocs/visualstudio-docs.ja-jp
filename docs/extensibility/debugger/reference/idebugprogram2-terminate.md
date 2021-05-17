---
description: プログラムを終了します。
title: IDebugProgram2::Terminate | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Terminate
helpviewer_keywords:
- IDebugProgram2::Terminate
ms.assetid: 4d3127d3-b1e9-4b28-ac22-2f2eea255f86
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 404df2be6718ab691ec47081b6fd400a1ddc8891
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084468"
---
# <a name="idebugprogram2terminate"></a>IDebugProgram2::Terminate
プログラムを終了します。

## <a name="syntax"></a>構文

```cpp
HRESULT Terminate( 
   void 
);
```

```csharp
int Terminate();
```

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 可能な場合は、プログラムが終了し、プロセスからアンロードされます。それ以外の場合は、デバッグ エンジン (DE) によって必要なクリーンアップが実行されます。

 このメソッド ([Terminate](../../../extensibility/debugger/reference/idebugprocess2-terminate.md) メソッド) は、通常、ユーザーがすべてのデバッグを停止したときに、IDE によって呼び出されます。 このメソッドを実装した場合、プロセス内でプログラムが終了するのが理想的です。 これが可能ではない場合は、DE で、このプロセスでプログラムがそれ以上実行されないようにする (および必要なクリーンアップを実行する) 必要があります。 `IDebugProcess2::Terminate` メソッドが IDE によって呼び出された場合は、`IDebugProgram2::Terminate` メソッドが呼び出された後にプロセス全体が終了し ます。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [Terminate](../../../extensibility/debugger/reference/idebugprocess2-terminate.md)
