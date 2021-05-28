---
description: このプロパティに関連付けられている一意の ID を破棄して、呼び出し元が他のすべてのプロパティから一意にこのプロパティを識別しなくなったことを示します。
title: IDebugProperty3::DestroyObjectID | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::DestroyObjectID
helpviewer_keywords:
- IDebugProperty3::DestroyObjectID
ms.assetid: bd08f356-cc67-4717-98c9-c3d00cad2040
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 071af90af5fe22d6f6cfa662458be660edc5d39f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064827"
---
# <a name="idebugproperty3destroyobjectid"></a>IDebugProperty3::DestroyObjectID
このプロパティに関連付けられている一意の ID を破棄して、呼び出し元が他のすべてのプロパティから一意にこのプロパティを識別しなくなったことを示します。

## <a name="syntax"></a>構文

```cpp
HRESULT DestroyObjectID(
   void
);
```

```csharp
int DestroyObjectID();
```

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 デバッグ エンジンがプロパティの一意の ID をサポートする必要がない場合 (既に内部的に一意に追跡しているため)、このメソッドに対して単に `E_NOTIMPL` を返すことができます。

 呼び出し元が、このプロパティが他のすべてのプロパティで一意に識別されていることを確認するには、[CreateObjectID](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md) メソッドを呼び出すと、一意の ID が作成されます。

## <a name="see-also"></a>関連項目
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [CreateObjectID](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md)
