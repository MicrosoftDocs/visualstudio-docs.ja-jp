---
title: IDebugProgramNode2::GetHostMachineName_V7 | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugProgramNode2::GetHostMachineName
helpviewer_keywords:
- IDebugProgramNode2::GetHostMachineName_V7
- IDebugProgramNode2::GetHostMachineNameIDebugProgramNode2::GetHostMachineName
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload:
- vssdk
ms.openlocfilehash: ef26af92dd50d4d79dc2f48e8cd7e32c03e86702
ms.sourcegitcommit: 8cbe6b38b810529a6c364d0f1918e5c71dee2c68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2018
---
# <a name="idebugprogramnode2gethostmachinenamev7"></a>IDebugProgramNode2::GetHostMachineName_V7

> [!Note]
> 推奨されなくなりました。 使用しないでください。

## <a name="syntax"></a>構文

```cpp
HRESULT GetHostMachineName_V7 (
   BSTR* pbstrHostMachineName
);
```

```csharp
int GetHostMachineName_V7 (
   out string pbstrHostMachineName
);
```

#### <a name="parameters"></a>パラメーター

`pbstrHostMachineName`  
[out]プログラムが実行されているコンピューターの名前を返します。

## <a name="return-value"></a>戻り値

実装を常に返します`E_NOTIMPL`です。

## <a name="remarks"></a>コメント

> [!WARNING]
> Visual Studio 2005 の時点でこのメソッドは使用されなくを常に返す必要があります`E_NOTIMPL`です。

## <a name="see-also"></a>参照

[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)