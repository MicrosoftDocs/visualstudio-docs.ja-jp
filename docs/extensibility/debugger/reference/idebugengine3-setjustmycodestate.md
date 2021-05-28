---
description: このメソッドは、JustMyCode 状態情報についてデバッグ エンジンに通知します。
title: IDebugEngine3::SetJustMyCodeState | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::SetJustMyCodeState
helpviewer_keywords:
- IDebugEngine3::SetJustMyCodeState
ms.assetid: 8ec17fbf-df93-424a-b2ed-fd1e5ee51256
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6e527dbaeb9c04171bf26ea00e550eac336ac6a8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066123"
---
# <a name="idebugengine3setjustmycodestate"></a>IDebugEngine3::SetJustMyCodeState
このメソッドは、JustMyCode 状態情報についてデバッグ エンジンに通知します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetJustMyCodeState(
   BOOL           fUpdate,
   DWORD          dwModules,
   JMC_CODE_SPEC* rgJMCSpec
);
```

```csharp
int SetJustMyCodeState(
   int             fUpdate,
   uint            dwModules,
   JMC_CODE_SPEC[] rgJMCSpec
);
```

## <a name="parameters"></a>パラメーター
`fUpdate`\
[入力] 現在の情報を更新する場合は 0 以外 (`TRUE`)、すべての情報をリセットする (以前に設定されたものをすべて無視する) 場合は 0 (`FALSE`)。

`dwModules`\
[入力] `rgJMCSpec.` 内の情報構造体の数。

`rgJMCSpec`\
[入力] 使用する [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md) 構造体の配列。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 JustMyCode とは、ユーザーに属するコードだけをデバッグし、システム コードなどの中間コードは、そのシステム コードのソース コードを利用できる場合でもすべて無視するという概念です。

## <a name="see-also"></a>関連項目
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
- [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md)
