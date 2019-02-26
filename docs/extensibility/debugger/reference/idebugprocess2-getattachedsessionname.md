---
title: IDebugProcess2::GetAttachedSessionName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::GetAttachedSessionName
helpviewer_keywords:
- IDebugProcess2::GetAttachedSessionName
ms.assetid: 7e5e116f-2c0c-4bc8-ad3f-e9fd2318a7e4
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aa932817c796249803558ad1eb877f620198b3e4
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56703546"
---
# <a name="idebugprocess2getattachedsessionname"></a>IDebugProcess2::GetAttachedSessionName
このプロセスがデバッグ セッションの名前を取得します。 IDE では、特定のコンピューターの特定のプロセスのデバッグは、ユーザーにこの情報を表示できます。

> [!NOTE]
>  このメソッドは廃止され、その実装を常に返します`E_NOTIMPL`します。

## <a name="syntax"></a>構文

```
HRESULT GetAttachedSessionName(
   BSTR* pbstrSessionName
);
```

#### <a name="parameters"></a>パラメーター
 `pbstrSessionName`

## <a name="return-value"></a>戻り値
 このメソッドは常に返します`E_NOTIMPL`します。

## <a name="see-also"></a>関連項目
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)