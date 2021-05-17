---
description: このインターフェイスは、クラスを型として表します。
title: IDebugClassField | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField
helpviewer_keywords:
- IDebugClassField interface
ms.assetid: 49358cbc-8973-4862-9dcc-79b1248e6712
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: dfb07f066d65ed48678c814444881cb004f14697
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088472"
---
# <a name="idebugclassfield"></a>IDebugClassField
このインターフェイスは、クラスを型として表します。

## <a name="syntax"></a>構文

```
IDebugClassField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>実装側の注意
 シンボル プロバイダーは、[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) インターフェイスを実装するのと同じオブジェクトにこのインターフェイスを実装します。 このインターフェイスは、クラス型を表す特殊化です。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 多くのインターフェイスには、[IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)、[IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)、[IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md) などの、このインターフェイスを返すことができるメソッドがあります。 また、[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) メソッドがフラグ `FIELD_TYPE_CLASS` を返す場合に、[QueryInterface](/cpp/atl/queryinterface) を使用して [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) インターフェイスからこのインターフェイスを取得することもできます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスは、[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) および [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) インターフェイスのメソッドに加えて、次を実装します。

|メソッド|説明|
|------------|-----------------|
|[EnumBaseClasses](../../../extensibility/debugger/reference/idebugclassfield-enumbaseclasses.md)|このクラスの基本クラスの列挙子を作成します。|
|[DoesInterfaceExist](../../../extensibility/debugger/reference/idebugclassfield-doesinterfaceexist.md)|クラスで特定のインターフェイスが定義されているかどうかを判断します。|
|[EnumNestedClasses](../../../extensibility/debugger/reference/idebugclassfield-enumnestedclasses.md)|このクラスの入れ子にされたクラスの列挙子を作成します。|
|[GetEnclosingClass](../../../extensibility/debugger/reference/idebugclassfield-getenclosingclass.md)|このクラスを囲むクラスを取得します。|
|[EnumInterfacesImplemented](../../../extensibility/debugger/reference/idebugclassfield-enuminterfacesimplemented.md)|このクラスによって実装されるインターフェイスの列挙子を作成します。|
|[EnumConstructors](../../../extensibility/debugger/reference/idebugclassfield-enumconstructors.md)|このクラスのコンストラクターの列挙子を作成します。|
|[GetDefaultIndexer](../../../extensibility/debugger/reference/idebugclassfield-getdefaultindexer.md)|既定のインデクサーの名前を取得します。|
|[EnumNestedEnums](../../../extensibility/debugger/reference/idebugclassfield-enumnestedenums.md)|このクラスの入れ子にされた列挙子の列挙子を作成します。|

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
