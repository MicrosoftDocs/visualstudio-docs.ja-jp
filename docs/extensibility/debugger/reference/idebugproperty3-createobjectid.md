---
title: IDebugProperty3::CreateObjectID |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::CreateObjectID
helpviewer_keywords:
- IDebugProperty3::CreateObjectID
ms.assetid: f2fa81e7-822f-456e-8729-a96a18eea771
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cf17196b4dae8642a81664dd339eaa78c2d2d8e9
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63412748"
---
# <a name="idebugproperty3createobjectid"></a>IDebugProperty3::CreateObjectID
その他のすべてのプロパティ間で一意であることを確認するこのプロパティの一意の ID を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreateObjectID(
   void
);
```

```csharp
int CreateObjectID();
```

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 セッション デバッグ マネージャーがこのプロパティは、その他のすべてのプロパティの間で一意に識別することを確認するときに、このメソッドが呼び出されます。 デバッグ エンジン (DE) は、処理プロパティが既に一意に識別される場合を除き、このメソッドをサポートしています。 返すかどうか、DE は、このメソッドをサポートしていません、`E_NOTIMPL`します。

 一意の ID が作成された`CreateObjectID`が破棄されるときに、 [DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)メソッドが呼び出される; も、このプロパティを一意に識別するための必要性の終端を表すこれです。

> [!NOTE]
> 一意の Id にして必要な DE を行うことができます、この一意の ID を取得するメソッドがないときに、`CreateObjectID`メソッドが呼び出されます。

## <a name="see-also"></a>関連項目
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)