---
description: このインターフェイスは、コード命令の開始位置を表します。
title: IDebugCodeContext2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCodeContext2
helpviewer_keywords:
- IDebugCodeContext2 interface
ms.assetid: 3670439e-2171-405d-9d77-dedb0f1cba93
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0d1fcf5ed3b40d0fafdc8ecf9a88c7000f01d5d4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088355"
---
# <a name="idebugcodecontext2"></a>IDebugCodeContext2
このインターフェイスは、コード命令の開始位置を表します。 現在、ほとんどの実行時のアーキテクチャでは、コード コンテキストはプログラムの実行ストリームのアドレスと考えることができます。

## <a name="syntax"></a>構文

```
IDebugCodeContext2 : IDebugMemoryContext2
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジンは、コード命令の位置をドキュメントの位置と関連付けるために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 多くのインターフェイスのメソッドは、このインターフェイス (通常は [GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)) を返します。 また、[IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md) インターフェイスおよびブレークポイントの解決情報でも広く使用されています。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスは、[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)|アクティブなコード コンテキストに対応するドキュメント コンテキストを取得します。|
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugcodecontext2-getlanguageinfo.md)|このコード コンテキストの言語情報を取得します。|

## <a name="remarks"></a>解説
 `IDebugCodeContext2` インターフェイスと [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) インターフェイスの主な違いは、`IDebugCodeContext2` が常に命令に沿っていることです。 これは、`IDebugCodeContext2` が常に命令の先頭を指すのに対し、`IDebugMemoryContext2` は実行時のアーキテクチャのメモリの任意のバイトを指す場合があることを意味します。 `IDebugCodeContext2` は、基本ストレージ サイズ (通常はバイト) ではなく、命令によってインクリメントされます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)
- [CanSetNextStatement](../../../extensibility/debugger/reference/idebugthread2-cansetnextstatement.md)
- [SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-next.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
