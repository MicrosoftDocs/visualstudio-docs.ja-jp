---
description: IDebugPortEx2::TerminateProcess はプロセスを終了します。
title: IDebugPortEx2::TerminateProcess | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEx2::TerminateProcess
helpviewer_keywords:
- IDebugPortEx2::TerminateProcess
ms.assetid: bf8fa94c-6d9d-4e4f-ac08-3b44ba5ace68
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fb783615ae50f8a3bb346e7d6aa281124104253e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072469"
---
# <a name="idebugportex2terminateprocess"></a>IDebugPortEx2::TerminateProcess
プロセスを終了します。

## <a name="syntax"></a>構文

```cpp
HRESULT TerminateProcess( 
   IDebugProcess2* pPortProcess
);
```

```csharp
int TerminateProcess( 
   IDebugProcess2 pPortProcess
);
```

## <a name="parameters"></a>パラメーター
`pPortProcess`\
[入力] 終了するプロセスを表す [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
