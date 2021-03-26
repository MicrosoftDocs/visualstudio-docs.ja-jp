---
description: プログラムをホストしているプロセスのシステムプロセス識別子を取得します。
title: 'IDebugProgramNode2:: GetHostPid |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::GetHostPid
helpviewer_keywords:
- IDebugProgramNode2::GetHostPid
ms.assetid: e65b4b15-46d8-4ca7-9456-2b4c078f7cf9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4e3fa384bc22c864f6438fb3c54e044d9fff7368
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087250"
---
# <a name="idebugprogramnode2gethostpid"></a>IDebugProgramNode2::GetHostPid
プログラムをホストしているプロセスのシステムプロセス識別子を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetHostPid ( 
   AD_PROCESS_ID * pdwHostPid
);
```

```csharp
int GetHostPid ( 
   out AD_PROCESS_ID pdwHostPid
);
```

## <a name="parameters"></a>パラメーター
`pdwHostPid`\
入出力ホストプロセスのシステムプロセス識別子を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="example"></a>例
 次の例は、IDebugProgramNode2 インターフェイスを実装する単純なオブジェクトに対してこのメソッドを実装する方法を示して `CProgram` います。 [](../../../extensibility/debugger/reference/idebugprogramnode2.md)

```cpp
HRESULT CProgram::GetHostPid(AD_PROCESS_ID* pdwHostPid) {
   // Check for valid argument.
   if (pdwHostPid == NULL)
     return E_INVALIDARG;

   // Get the process identifier of the calling process.
   pdwHostPid->ProcessIdType = AD_PROCESS_ID_SYSTEM;
   pdwHostPid->ProcessId.dwProcessId = GetCurrentProcessId();
   return S_OK;
}
```

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
