---
description: このメソッドを使用すると、指定されたデバッグ エンジン (DE) ごとにプログラム ノードを追加できます。
title: IDebugProcessEx2::AddImplicitProgramNodes | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessEx2::AddImplicitProgramNodes
helpviewer_keywords:
- IDebugProcessEx2::AddImplicitProgramNodes method
ms.assetid: 8b491b00-f9e7-45b3-9115-fe58c3464289
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 30e5943ca0326a05b98b9fb833004c0ba7e342d3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076395"
---
# <a name="idebugprocessex2addimplicitprogramnodes"></a>IDebugProcessEx2::AddImplicitProgramNodes
このメソッドを使用すると、指定されたデバッグ エンジン (DE) ごとにプログラム ノードを追加できます。

## <a name="syntax"></a>構文

```cpp
HRESULT AddImplicitProgramNodes(
   REFGUID guidLaunchingEngine,
   GUID*   rgguidSpecificEngines,
   DWORD   celtSpecificEngines
);
```

```csharp
int AddImplicitProgramNodes(
   ref Guid guidLaunchingEngine,
   Guid[]   rgguidSpecificEngines,
   uint     celtSpecificEngines
);
```

## <a name="parameters"></a>パラメーター
`guidLaunchingEngine`\
[入力] プログラムの起動に使用される (そして独自のプログラム ノードが追加されると想定される) DE の `GUID`。

`rgguidSpecificEngines`\
[入力] プログラム ノードが追加される DE の `GUID` の配列。

`celtSpecificEngines`\
[入力] `rgguidSpecificEngines` 配列内の `GUID` の数。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
- [プログラム ノード](../../../extensibility/debugger/program-nodes.md)は、`rgguidSpecificEngines` に列挙されている各 DE に追加されます。ただし、起動エンジン (`guidLaunchingEngine` で指定されています) を除きます。これにより、プログラムの起動時に独自のプログラム ノードが追加されると想定されています。

## <a name="see-also"></a>関連項目
- [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)
- [プログラム ノード](../../../extensibility/debugger/program-nodes.md)
