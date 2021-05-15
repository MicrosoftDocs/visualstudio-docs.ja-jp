---
description: このプロセスが実行されているサーバーを取得します。
title: IDebugProcess2::GetServer | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::GetServer
helpviewer_keywords:
- IDebugProcess2::GetServer
ms.assetid: 8f73c530-cceb-4f1f-8c63-1cc0ccd4a310
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a2bf0528526e20fc3eae7acf46dfc2b706be94eb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081634"
---
# <a name="idebugprocess2getserver"></a>IDebugProcess2::GetServer
このプロセスが実行されているサーバーを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetServer( 
   IDebugCoreServer2** ppServer
);
```

```csharp
int GetServer( 
   out IDebugCoreServer2 ppServer
);
```

## <a name="parameters"></a>パラメーター
`ppServer`\
[out] このプロセスが実行されているサーバーを表す [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 1 台のコンピューターで複数のサーバーが実行されている可能性があります。

## <a name="see-also"></a>関連項目
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
