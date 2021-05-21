---
description: このインターフェイスによってメソッドが記述されます。
title: IDebugMethodField | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField
helpviewer_keywords:
- IDebugMethodField interface
ms.assetid: a7dc9030-fc98-4cf1-b943-37a4003300b6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5234f209ecd8866c8fa55735ad21a79cdfd7404d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054323"
---
# <a name="idebugmethodfield"></a>IDebugMethodField
このインターフェイスによってメソッドが記述されます。

## <a name="syntax"></a>構文

```
IDebugMethodField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>実装側の注意
 シンボル プロバイダーは、[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) インターフェイスを実装するのと同じオブジェクトにこのインターフェイスを実装します。 このインターフェイスは、メソッドを提供する特殊化です。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) によって `FIELD_TYPE_METHOD` が返される場合は、[QueryInterface](/cpp/atl/queryinterface) を使用して、[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) インターフェイスからこのインターフェイスを取得します。 さらに、[GetPropertyGetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertygetter.md)、[GetPropertySetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertysetter.md)、[EnumConstructors](../../../extensibility/debugger/reference/idebugclassfield-enumconstructors.md) メソッドはすべて、`IDebugMethodField` インターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスは、[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) および [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[EnumParameters](../../../extensibility/debugger/reference/idebugmethodfield-enumparameters.md)|メソッドのパラメーターの列挙子を作成します。|
|[GetThis](../../../extensibility/debugger/reference/idebugmethodfield-getthis.md)|メソッドを格納しているオブジェクトの "この" ポインターを取得します。|
|[EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md)|メソッドのすべてのローカル変数の列挙子を作成します。|
|[EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)|メソッドの選択されたローカル変数の列挙子を作成します。|
|[IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugmethodfield-iscustomattributedefined.md)|特定のカスタム属性が定義されているかどうかを判断します。|
|[EnumStaticLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumstaticlocals.md)|メソッドの静的ローカル変数の列挙子を作成します。|
|[GetGlobalContainer](../../../extensibility/debugger/reference/idebugmethodfield-getglobalcontainer.md)|メソッドのグローバル コンテナーを取得します。|
|[EnumArguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)|メソッドを呼び出すために必要な各引数の型の列挙子を作成します。|

## <a name="remarks"></a>解説
 メソッドには、ローカル変数だけでなく、パラメーターを含めることもできます。

## <a name="requirements"></a>要件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
