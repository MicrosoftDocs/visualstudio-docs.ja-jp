---
description: このプログラムのホスト プロセスのタイトル、フレンドリ名、またはファイル名を取得します。
title: IDebugProgramHost2::GetHostName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramHost2::GetHostName
helpviewer_keywords:
- IDebugProgramHost2::GetHostName
ms.assetid: 48bbb089-e59a-471a-9965-24b42a8dabf3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 53b4d69be1ea24f5c240b6247539f499c9fb00fb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084013"
---
# <a name="idebugprogramhost2gethostname"></a>IDebugProgramHost2::GetHostName
このプログラムのホスト プロセスのタイトル、フレンドリ名、またはファイル名を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetHostName( 
   DWORD dwType,
   BSTR* pbstrHostName
);
```

```csharp
int GetHostName( 
   uint dwType,
   out string pbstrHostName
);
```

## <a name="parameters"></a>パラメーター
`dwType`\
[入力] [GETHOSTNAME_TYPE](../../../extensibility/debugger/reference/gethostname-type.md) 列挙型の値。

`pbstrHostName`\
[出力] 要求されたホスト プロセスの名前を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドの一般的な実装では、`dwType` パラメーターは無視され、ホスト コンピューターのフレンドリ名が返されます。 もう 1 つの可能な実装は、`dwType` パラメーターを [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md) メソッドの呼び出しに渡して、名前を取得することです。

## <a name="see-also"></a>関連項目
- [IDebugProgramHost2](../../../extensibility/debugger/reference/idebugprogramhost2.md)
- [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)
