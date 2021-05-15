---
description: 型を表すフィールドを作成する機能を表します。
title: IDebugTypeFieldBuilder | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugTypeFieldBuilder interface
ms.assetid: 2dfed0be-6972-4bec-baec-f0b78df9ef97
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8bf2199766cd0e78940c38e8441fe9fb0ab3c320
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083493"
---
# <a name="idebugtypefieldbuilder"></a>IDebugTypeFieldBuilder
型を表すフィールドを作成する機能を表します。

## <a name="syntax"></a>構文

```
IDebugTypeFieldBuilder : IUnknown
```

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、シンボル プロバイダーから取得されます。

## <a name="methods"></a>メソッド
 このインターフェイスには、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[CreatePrimitive](../../../extensibility/debugger/reference/idebugtypefieldbuilder-createprimitive.md)|プリミティブ型を表すオブジェクトを作成します。|
|[CreatePointerToType](../../../extensibility/debugger/reference/idebugtypefieldbuilder-createpointertotype.md)|指定した型へのポインターを作成します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
