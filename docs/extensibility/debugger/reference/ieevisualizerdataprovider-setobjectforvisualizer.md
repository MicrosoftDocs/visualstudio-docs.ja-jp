---
description: このメソッドは、ビジュアライザーで表されるオブジェクトを変更します。
title: IEEVisualizerDataProvider::SetObjectForVisualizer | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerDataProvider::SetObjectForVisualizer
helpviewer_keywords:
- IEEVisualizerDataProvider::SetObjectForVisualizer method
ms.assetid: 40dad2be-57ff-4f74-9d82-c48039c125c4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2e0a59c10293d5d8cc13d46b625a7b43136cb71b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091800"
---
# <a name="ieevisualizerdataprovidersetobjectforvisualizer"></a>IEEVisualizerDataProvider::SetObjectForVisualizer
このメソッドは、ビジュアライザーで表されるオブジェクトを変更します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetObjectForVisualizer(
   IDebugObject*  pNewObject,
   BSTR*          error,
   IDebugObject** pException
);
```

```csharp
int SetObjectForVisualizer(
   IDebugObject     pNewObject,
   out string       error,
   out IDebugObject pException
);
```

## <a name="parameters"></a>パラメーター
`pNewObject`\
[入力] 設定するオブジェクト。

`error`\
[出力] オブジェクトの設定中にエラーが発生した場合、この文字列はエラー メッセージを保持します。

`pException`\
[出力] エラーが発生した場合、このオブジェクトは例外情報を保持します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 エラー情報がどのように返されるかを決定するのは、実装者の責任です。 ただし、一部の呼び出し元は、エラーが発生したことを知るために例外オブジェクトが返されたかどうかだけを確認する可能性があるため、エラーが発生した場合、このメソッドは常に例外オブジェクトを返す必要があります。 このエラー文字列は、呼び出し元がそれを利用したい場合に備えて提供する必要があります。

## <a name="see-also"></a>関連項目
- [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
