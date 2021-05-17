---
description: このインターフェイスは、スタック フレーム プロパティまたはその他のプロパティへの参照を表します。
title: IDebugReference2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2
helpviewer_keywords:
- IDebugReference2 interface
ms.assetid: 3cfed312-f532-4bce-84a5-1677c14567d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f6b1c30b2da2862e17a1ebf16cc41008341127c5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075758"
---
# <a name="idebugreference2"></a>IDebugReference2
このインターフェイスは、スタック フレーム プロパティまたはその他のプロパティへの参照を表します。

> [!NOTE]
> `IDebugReference2` は将来使用するために予約されており、そのすべてのメソッドが `E_NOTIMPL` を返す必要があります。

## <a name="syntax"></a>構文

```
IDebugReference2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE では、特定の種類の値への参照を表すために、このインターフェイスを実装します。 たとえば、値には、式の評価の結果としての数値、メモリの表示に使用されるメモリ コンテキスト、レジスタとその値の一覧などがあります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスを取得するには、[GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md) を呼び出します。 [GetParent](../../../extensibility/debugger/reference/idebugreference2-getparent.md) と [GetDerivedMostReference](../../../extensibility/debugger/reference/idebugreference2-getderivedmostreference.md) でも、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugReference2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)|この参照が記述されている [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 構造体を取得します。|
|[SetValueAsString](../../../extensibility/debugger/reference/idebugreference2-setvalueasstring.md)|文字列からこの参照の値を設定します。|
|[SetValueAsReference](../../../extensibility/debugger/reference/idebugreference2-setvalueasreference.md)|別の参照からこの参照の値を設定します。|
|[EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)|この参照の子を列挙します。|
|[GetParent](../../../extensibility/debugger/reference/idebugreference2-getparent.md)|この参照の親を取得します。|
|[GetDerivedMostReference](../../../extensibility/debugger/reference/idebugreference2-getderivedmostreference.md)|この参照の最派生参照を取得します。|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)|この参照が参照するメモリ バイト数を取得します。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)|この参照のメモリ コンテキストを取得します。|
|[GetSize](../../../extensibility/debugger/reference/idebugreference2-getsize.md)|この参照のサイズ (バイト単位) を取得します。|
|[SetReferenceType](../../../extensibility/debugger/reference/idebugreference2-setreferencetype.md)|この参照型を設定します。|
|[比較](../../../extensibility/debugger/reference/idebugreference2-compare.md)|この参照と別のものを比較します。|

## <a name="remarks"></a>解説

> [!NOTE]
> このような "プロパティ" の使用をクラスのメンバー変数と混同しないでください。ただし、`IDebugReference2` ではこのようなエンティティを表すことができます。

- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) はプロパティを表しますが、`IDebugReference2` はプロパティへの参照、通常はデバッグ中のプログラム内のオブジェクトへの参照を表します。

 プロパティと参照の主な違いは、プロパティがオブジェクトの名前付きインスタンスを参照するのに対し、参照は名前のないインスタンスを参照することです。 たとえば、プロパティでは、`"a.b"` によってプログラムのヒープ内にあるオブジェクトを参照できます。 別のプロパティでは、`"c.d"` と同じオブジェクトを参照できる可能性があります。 このプロパティを参照する方法では、`"a.b"` または `"c.d"` がスコープ内にある必要があります。 この同じオブジェクトへの参照は無名です。そのオブジェクトのメモリが有効である限り、オブジェクトを参照できます。

 `IDebugProperty2` インターフェイスは、名前、型、およびアドレスを持つ値であると考えることができます。 一方、`IDebugReference2` は、型とアドレスであると考えることができます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)
