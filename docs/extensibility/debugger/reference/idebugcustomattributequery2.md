---
description: このフィールドにカスタム属性が存在するかどうかを判断し、存在する場合は属性情報を返します。
title: IDebugCustomAttributeQuery2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2
helpviewer_keywords:
- IDebugCustomAttributeQuery interface
- IDebugCustomAttributeQuery2 interface
ms.assetid: 7cfa23e4-a05a-47a3-af6c-bd40c655014b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 00f7e23b280ef92e9883f68f203bd790f5e4d815
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077565"
---
# <a name="idebugcustomattributequery2"></a>IDebugCustomAttributeQuery2
このフィールドにカスタム属性が存在するかどうかを判断し、存在する場合は属性情報を返します。

## <a name="syntax"></a>構文

```
IDebugCustomAttributeQuery2 : IDebugCustomAttributeQuery
```

## <a name="notes-for-implementers"></a>実装側の注意
 シンボル プロバイダーでは、カスタム属性をサポートするために、[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) を実装するのと同じオブジェクトにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [QueryInterface](/cpp/atl/queryinterface) を使用して、[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスからこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、**IDebugCustomAttributeQuery** インターフェイスのメソッドを示しています。

|メソッド|説明|
|------------|-----------------|
|[IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md)|カスタム属性が存在するかどうかを名前で判断します。|
|[GetCustomAttributeByName](../../../extensibility/debugger/reference/idebugcustomattributequery2-getcustomattributebyname.md)|指定されたカスタム属性の属性情報を取得します。|

 `IDebugCustomAttributeQuery2` には、**IDebugCustomAttributeQuery** メソッドに加えて、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[EnumCustomAttributes](../../../extensibility/debugger/reference/idebugcustomattributequery2-enumcustomattributes.md)|このフィールドに関連付けられているすべてのカスタム属性の列挙子を取得します。|

## <a name="remarks"></a>解説
 [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md) メソッドでは、このフィールドに対して定義されているすべてのカスタム属性の列挙子を返すことができます。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
