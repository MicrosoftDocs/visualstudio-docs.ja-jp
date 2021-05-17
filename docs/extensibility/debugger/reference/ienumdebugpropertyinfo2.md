---
description: このインターフェイスによって DEBUG_PROPERTY_INFO 構造体が列挙されます。
title: IEnumDebugPropertyInfo2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPropertyInfo2
helpviewer_keywords:
- IEnumDebugPropertyInfo2
ms.assetid: fdea8262-40b8-473e-88ba-639e4c4648e6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 82de88b69a3609db50d601fb4a566c510712afd8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095252"
---
# <a name="ienumdebugpropertyinfo2"></a>IEnumDebugPropertyInfo2
このインターフェイスによって [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体が列挙されます。

## <a name="syntax"></a>構文

```
IEnumDebugPropertyInfo2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) では、特定のプロパティに関する情報を表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [Enumchildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) を呼び出して、特定のプロパティの子を表すこのインターフェイスを取得します。 [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md) を呼び出して、特定のスタック フレームのプロパティを表すこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IEnumDebugPropertyInfo2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md)|列挙型シーケンス内の指定された数の [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体を取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-skip.md)|列挙型シーケンス内の指定された数の [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体をスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-reset.md)|列挙型シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md)|列挙子内の [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体の数を取得します。|

## <a name="remarks"></a>解説
 一般に、プロパティは、名前、値、アドレス、型、および関連付けられているプロパティ オブジェクトまたはスタック フレームに適したその他の情報を含めることができる情報の階層です。 詳細については、「[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)」を参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
- [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)
