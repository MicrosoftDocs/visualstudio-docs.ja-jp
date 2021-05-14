---
description: デバッグ エンジン (DE) をプログラムからデタッチできるかどうかを決定します。
title: IDebugProgram2::CanDetach | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::CanDetach
helpviewer_keywords:
- IDebugProgram2::CanDetach
ms.assetid: dcd9ab6c-49e5-447e-aa7c-89f571f4a052
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9e751429fe26060a515f94aa3d402954ff598d39
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076174"
---
# <a name="idebugprogram2candetach"></a>IDebugProgram2::CanDetach
デバッグ エンジン (DE) をプログラムからデタッチできるかどうかを決定します。

## <a name="syntax"></a>構文

```cpp
HRESULT CanDetach(
   void
);
```

```csharp
int CanDetach();
```

## <a name="return-value"></a>戻り値
 デタッチできる場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 DE をプログラムからデタッチできない場合は `S_FALSE` を返します。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
