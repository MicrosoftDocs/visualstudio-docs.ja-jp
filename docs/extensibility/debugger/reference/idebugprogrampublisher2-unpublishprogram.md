---
description: プログラムをデバッグできないようにします。
title: IDebugProgramPublisher2::UnpublishProgram | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2::UnpublishProgram
helpviewer_keywords:
- IDebugProgramPublisher2::UnpublishProgram
ms.assetid: 627e7d38-b2ac-4873-9a40-37ff7f47cd1d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fc00a6339ba6e0b4405a4ebdbecd97fa34ad0e3b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065113"
---
# <a name="idebugprogrampublisher2unpublishprogram"></a>IDebugProgramPublisher2::UnpublishProgram
プログラムをデバッグできないようにします。

## <a name="syntax"></a>構文

```cpp
HRESULT UnpublishProgram(
   IUnknown* pDebuggeeInterface
);
```

```csharp
int UnpublishProgram(
   object pDebuggeeInterface
);
```

## <a name="parameters"></a>パラメーター
`pDebuggeeInterface`\
[in] プログラムへの `IUnknown` インターフェイス。 これは、[PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md) メソッドに指定された値と同じであり、除外される (つまり、Cookie として使用される) プログラムを一意に識別します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 プログラムをデバッグ エンジンとセッション デバッグ マネージャーで使用できるようにするには、[PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md) メソッドを使用します。

## <a name="see-also"></a>関連項目
- [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)
- [PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md)
