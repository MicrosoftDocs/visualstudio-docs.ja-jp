---
description: 他のすべてのプロパティとの間で一意性を保証するために、このプロパティの一意の ID を作成します。
title: IDebugProperty3::CreateObjectID | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::CreateObjectID
helpviewer_keywords:
- IDebugProperty3::CreateObjectID
ms.assetid: f2fa81e7-822f-456e-8729-a96a18eea771
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: af90f360e59e04cc5d55017c5d986e6682bab2ed
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064814"
---
# <a name="idebugproperty3createobjectid"></a>IDebugProperty3::CreateObjectID
他のすべてのプロパティとの間で一意性を保証するために、このプロパティの一意の ID を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreateObjectID(
   void
);
```

```csharp
int CreateObjectID();
```

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドは、このプロパティが他のすべてのプロパティとは異なるものとして一意に識別されていることをセッション デバッグ マネージャーで確認したい場合に呼び出されます。 デバッグ エンジン (DE) では、DE で扱うプロパティが既に一意に識別されている場合を除いて、このメソッドをサポートします。 このメソッドをサポートしていない場合、DE は `E_NOTIMPL` を返します。

 `CreateObjectID` を使用して作成された一意の ID は、[DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md) メソッドが呼び出されると破棄されます。これは、このプロパティを一意に識別する必要がなくなったというシグナルでもあります。

> [!NOTE]
> この一意の ID を取得するメソッドはありません。したがって DE では、`CreateObjectID` メソッドが呼び出されたときに一意の ID をどのように処理してもかまいません。

## <a name="see-also"></a>関連項目
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)
