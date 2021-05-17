---
description: このインターフェイスは、ソース ドキュメント内の関数の抽象的な位置を表します。
title: IDebugFunctionPosition2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionPosition2
helpviewer_keywords:
- IDebugFunctionPosition2 interface
ms.assetid: a835f65b-91b0-48ad-8485-04534c814b1b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e5afd44827d8d9b6f244bc914728bd090261ab25
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063475"
---
# <a name="idebugfunctionposition2"></a>IDebugFunctionPosition2
このインターフェイスは、ソース ドキュメント内の関数の抽象的な位置を表します。

## <a name="syntax"></a>構文

```
IDebugFunctionPosition2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) では、ソース ドキュメント内の関数の位置を表すために、このインターフェイスを実装しています。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) 共用体 (具体的には、保留中のブレークポイントの作成に使用される [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 構造体の一部である [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md) 構造体) の一部として提供されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugFunctionPosition2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetFunctionName](../../../extensibility/debugger/reference/idebugfunctionposition2-getfunctionname.md)|この位置の相対的な基準である関数の名前を取得します。|
|[GetOffset](../../../extensibility/debugger/reference/idebugfunctionposition2-getoffset.md)|関数の先頭からのオフセットを取得します。|

## <a name="remarks"></a>解説
 このインターフェイスによって表される位置はテキストベースであり、具体的には [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 構造体です。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
