---
description: このインターフェイスは、命令のストリームを表します。
title: IDebugDisassemblyStream2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2
helpviewer_keywords:
- IDebugDisassemblyStream2 interface
ms.assetid: b03cab0c-3f0b-4cc6-88dc-acb3b48c567a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8e4ffa8de4b245071f1893eae5f5427a9dccd353
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066881"
---
# <a name="idebugdisassemblystream2"></a>IDebugDisassemblyStream2
このインターフェイスは、命令のストリームを表します。

## <a name="syntax"></a>構文

```
IDebugDisassemblyStream2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジンでは、プログラムのコードの逆アセンブリをサポートするために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md) メソッドを呼び出すと、このインターフェイスが返されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugDisassemblyStream2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[読み取り](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)|逆アセンブリ ストリーム内の現在位置から始まる命令を読み取ります。|
|[Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)|逆アセンブリ ストリーム内の読み取りポインターを、指定された位置を基準にして指定された命令数だけ移動します。|
|[GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)|特定のコード コンテキストのコード位置識別子を返します。|
|[GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)|指定されたコード位置識別子に対応するコード コンテキスト オブジェクトを返します。|
|[GetCurrentLocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md)|現在のコードの場所を表すコードの位置識別子を返します。|
|[GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md)|この逆アセンブリ ストリームに関連付けられているソース ドキュメントを取得します。|
|[GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)|この逆アセンブリ ストリームのスコープを取得します。|
|[GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md)|この逆アセンブリ ストリームのサイズを取得します。|

## <a name="remarks"></a>解説
 逆アセンブリ ストリームは、アドレス空間全体を表すように作成することも、空間内の関数またはモジュールのみを表すように作成することもできます。 各命令は、[Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md) メソッドの呼び出しによって返される [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md) 構造体によって表されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
