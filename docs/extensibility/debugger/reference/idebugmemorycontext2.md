---
title: IDebugMemoryContext2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2
helpviewer_keywords:
- IDebugMemoryContext2 interface
ms.assetid: 3a544c8b-11dc-46bb-8549-261e4ac5bbc4
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bb1abe29a915d8ca2aaba1135d2e57946250bc3f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66346971"
---
# <a name="idebugmemorycontext2"></a>IDebugMemoryContext2
このインターフェイスは、デバッグ中のプログラムを実行しているコンピューターのアドレス空間内の位置を表します。

## <a name="syntax"></a>構文

```
IDebugMemoryContext2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 デバッグ エンジン (DE) は、メモリ内のアドレスを表すためには、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元のノート
 呼び出し[GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)または[GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)このインターフェイスを返します。 また、呼び出し[追加](../../../extensibility/debugger/reference/idebugmemorycontext2-add.md)と[減算](../../../extensibility/debugger/reference/idebugmemorycontext2-subtract.md)適切な算術演算を適用した後、このインターフェイスの新しいコピーを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、メソッドの`IDebugMemoryContext2`します。

|メソッド|説明|
|------------|-----------------|
|[GetName](../../../extensibility/debugger/reference/idebugmemorycontext2-getname.md)|このコンテキストの表示名を取得します。|
|[GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)|このコンテキストを説明する情報を取得します。|
|[[追加]](../../../extensibility/debugger/reference/idebugmemorycontext2-add.md)|新しいコンテキストを作成する、現在のコンテキストのアドレスを指定した値を追加します。|
|[Subtract](../../../extensibility/debugger/reference/idebugmemorycontext2-subtract.md)|新しいコンテキストを作成する、現在のコンテキストのアドレスから指定された値を減算します。|
|[Compare](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md)|比較によって示されるように 2 つのコンテキストでは、フラグを比較します。|

## <a name="remarks"></a>Remarks
 Visual Studio の**メモリ**ウィンドウ呼び出し[GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)を取得する、`IDebugMemoryContext2`メモリ アドレスに使用される式の評価結果を格納しているインターフェイス。 このコンテキストに渡されます[ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)と[WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)読み取りまたは書き込みのアドレスを指定します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)
- [GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)
- [ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)
- [WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)