---
description: このメソッドは、プログラムをデバッグ エンジン (DE) とセッション デバッグ マネージャーで使用できるようにします。
title: IDebugProgramPublisher2::PublishProgram | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2::PublishProgram
helpviewer_keywords:
- IDebugProgramPublisher2::PublishProgram
ms.assetid: 92ff63f0-e869-4040-b3ae-b2c899e708ff
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ba1ac74813ea0c3ae5b7eadb26d540b7bfe20707
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065230"
---
# <a name="idebugprogrampublisher2publishprogram"></a>IDebugProgramPublisher2::PublishProgram
このメソッドは、プログラムをデバッグ エンジン (DE) とセッション デバッグ マネージャーで使用できるようにします。

## <a name="syntax"></a>構文

```cpp
HRESULT PublishProgram(
   CONST_GUID_ARRAY Engines,
   LPCOLESTR        szFriendlyName,
   IUnknown*        pDebuggeeInterface
);
```

```csharp
int PublishProgram(
   CONST_GUID_ARRAY Engines,
   string           szFriendlyName,
   object           pDebuggeeInterface
);
```

## <a name="parameters"></a>パラメーター
`Engines`\
[入力] このプログラムを起動またはアタッチできる DE の GUID の配列。

`szFriendlyName`\
[入力] プログラムのフレンドリ名 (これは、ユーザーに示されるメニューまたはダイアログに表示されます)。

`pDebuggeeInterface`\
[入力] プログラムの `IUnknown` インターフェイス (この値はプログラムを一意に識別するために Cookie として使用されます。この同じ値は、プログラムの "発行取り消し" に使用されます)

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 プログラムをデバッグに使用できないようにするには、[UnpublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogram.md) を呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)
- [UnpublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogram.md)
