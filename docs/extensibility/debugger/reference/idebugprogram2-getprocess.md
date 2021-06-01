---
description: このプログラムが実行されているプロセスを取得します。
title: IDebugProgram2::GetProcess | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetProcess
helpviewer_keywords:
- IDebugProgram2::GetProcess
ms.assetid: 1d602485-ebaf-451c-9165-f2e226f20a90
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1d87d863b954a9865ff3960f2f2cdd45ac40ce58
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065399"
---
# <a name="idebugprogram2getprocess"></a>IDebugProgram2::GetProcess
このプログラムが実行されているプロセスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetProcess(
   IDebugProcess2** ppProcess
);
```

```csharp
int GetProcess(
   out IDebugProcess2 ppProcess
);
```

## <a name="parameters"></a>パラメーター
`ppProcess`\
[出力] プロセスを表す [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) インターフェイスを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 デバッグ エンジン (DE) が [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md) インターフェイスを実装している場合を除き、DE のこのメソッドの実装は常に `E_NOTIMPL` を返すはずです。なぜなら、DE は、実行されているプロセスを特定できないため、このメソッドの実装を満たすことができないからです。

 `IDebugEngineLaunch2` インターフェイスを実装することは、DE がプロセスの作成方法を知っている必要があるということであり、したがって、DE の [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスの実装は、実行されているプロセスを知ることができます。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
