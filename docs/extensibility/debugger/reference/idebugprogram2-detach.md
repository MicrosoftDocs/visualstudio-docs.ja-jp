---
description: プログラムからデバッグ エンジンをデタッチします。
title: IDebugProgram2::Detach | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Detach
helpviewer_keywords:
- IDebugProgram2::Detach
ms.assetid: 5e8d88b0-a8d4-4746-88c0-ad332ee73f33
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2e9e7527ee13c703bbf7e1ba5a15ae225cf87c0b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076096"
---
# <a name="idebugprogram2detach"></a>IDebugProgram2::Detach
プログラムからデバッグ エンジンをデタッチします。

## <a name="syntax"></a>構文

```cpp
HRESULT Detach( 
   void 
);
```

```csharp
int Detach();
```

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 デタッチされたプログラムは引き続き実行されますが、デバッグ セッションの一部ではなくなります。 デバッグ エンジンがデタッチされると、プログラム デバッグ イベントは送信されなくなります。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
