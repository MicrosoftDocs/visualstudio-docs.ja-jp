---
title: IDebugReference2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2
helpviewer_keywords:
- IDebugReference2 interface
ms.assetid: 3cfed312-f532-4bce-84a5-1677c14567d7
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fe49341bf485068701d3fb06842c5ef65359a9bf
ms.sourcegitcommit: 50f0c3f2763a05de8482b3579026d9c76c0e226c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2019
ms.locfileid: "65458673"
---
# <a name="idebugreference2"></a>IDebugReference2
このインターフェイスは、スタック フレームのプロパティまたはその他のいくつかのプロパティへの参照を表します。

> [!NOTE]
> `IDebugReference2` 将来の使用とそのメソッドが返す必要がありますすべてに予約されている`E_NOTIMPL`します。

## <a name="syntax"></a>構文

```
IDebugReference2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 デでは、特定の種類の値への参照を表すためには、このインターフェイスを実装します。 たとえば、値は、式の評価、メモリ、またはレジスタとその値の一覧を表示するためのメモリのコンテキストの結果として数値。

## <a name="notes-for-callers"></a>呼び出し元のノート
 呼び出す[GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)このインターフェイスを取得します。 [GetParent](../../../extensibility/debugger/reference/idebugreference2-getparent.md)と[GetDerivedMostReference](../../../extensibility/debugger/reference/idebugreference2-getderivedmostreference.md)このインターフェイスを返すこともできます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、メソッドの`IDebugReference2`します。

|メソッド|説明|
|------------|-----------------|
|[GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)|取得、 [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)この参照を記述する構造体。|
|[SetValueAsString](../../../extensibility/debugger/reference/idebugreference2-setvalueasstring.md)|この参照文字列からの値を設定します。|
|[SetValueAsReference](../../../extensibility/debugger/reference/idebugreference2-setvalueasreference.md)|この参照別の参照からの値を設定します。|
|[EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)|この参照の子を列挙します。|
|[GetParent](../../../extensibility/debugger/reference/idebugreference2-getparent.md)|この参照の親を取得します。|
|[GetDerivedMostReference](../../../extensibility/debugger/reference/idebugreference2-getderivedmostreference.md)|この参照の最も多く派生された参照を取得します。|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)|この参照が参照するメモリのバイト数を取得します。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)|この参照は、メモリのコンテキストを取得します。|
|[GetSize](../../../extensibility/debugger/reference/idebugreference2-getsize.md)|この参照のバイト単位のサイズを取得します。|
|[SetReferenceType](../../../extensibility/debugger/reference/idebugreference2-setreferencetype.md)|この参照型を設定します。|
|[Compare](../../../extensibility/debugger/reference/idebugreference2-compare.md)|この参照を別に比較します。|

## <a name="remarks"></a>Remarks

> [!NOTE]
> この「プロパティ」を使用する必要がありますと混同しない、つまり、クラスのメンバー変数が、`IDebugReference2`そのエンティティを表すことができます。

- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 、プロパティを表す、 `IDebugReference2` 、デバッグ中のプログラム内のオブジェクトへの参照を通常のプロパティの参照を表します。

 プロパティとの参照の主な違いは、プロパティは、名前のないインスタンスを参照中に、オブジェクトの名前付きインスタンスを参照します。 によって、プログラムのヒープ内のオブジェクトにプロパティをたとえば、参照する可能性があります`"a.b"`します。 別のプロパティと同じオブジェクトを参照してください`"c.d"`します。 このプロパティを参照する方法である必要があります`"a.b"`または`"c.d"`スコープ内にします。 この同じオブジェクトへの参照が無名です。オブジェクトは、そのオブジェクトのメモリが有効な限りを参照できます。

 `IDebugProperty2`インターフェイスは、名前、種類、およびアドレスの値として考えることができます。 `IDebugReference2`、もう一方の一方、型と、アドレスとして考えることができます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)