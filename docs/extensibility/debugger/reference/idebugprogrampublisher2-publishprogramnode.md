---
title: IDebugProgramPublisher2::PublishProgramNode |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2::PublishProgramNode
helpviewer_keywords:
- IDebugProgramPublisher2::PublishProgramNode
ms.assetid: d4b72e04-f726-46cf-8e56-5203ff205b12
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e1b0611b723b649fd8d899af427c6b41fb5db1e1
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66343296"
---
# <a name="idebugprogrampublisher2publishprogramnode"></a>IDebugProgramPublisher2::PublishProgramNode
プログラム ノード使用できるようにデバッグ エンジン (DEs) を使用して、セッション デバッグ マネージャー (SDM)。

## <a name="syntax"></a>構文

```cpp
HRESULT PublishProgramNode(
   IDebugProgramNode2 *pProgramNode
);
```

```csharp
int PublishProgramNode(
   IDebugProgramNode2 pProgramNode
);
```

## <a name="parameters"></a>パラメーター
`pProgramNode`\
[in][IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)使用できるようにするプログラムのノードを表すオブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドを選択して、デバッグ用の起動前に、情報のクエリを実行するプログラムを使用します。

 可用性から、[プログラム] ノードを削除するには、呼び出し、 [UnpublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogramnode.md)メソッド。

## <a name="see-also"></a>関連項目
- [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [UnpublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogramnode.md)