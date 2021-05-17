---
description: 関連付けられているプログラムへのアタッチの試みをプログラム ノードに通知できるようにします。
title: IDebugProgramNodeAttach2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNodeAttach2
helpviewer_keywords:
- IDebugProgramNodeAttach2 interface
ms.assetid: 46b37ac9-a026-4ad3-997b-f19e2f8deb73
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1a1de6c7480e1ce4dcc0723614741a05dcc961a6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071468"
---
# <a name="idebugprogramnodeattach2"></a>IDebugProgramNodeAttach2
関連付けられているプログラムへのアタッチの試みをプログラム ノードに通知できるようにします。

## <a name="syntax"></a>構文

```
IDebugProgramNodeAttach2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、アタッチ操作の通知を受信し、アタッチ操作をキャンセルする機会を提供するために、 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) インターフェイスを実装するものと同じクラスに実装されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスを取得するには、[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクトの `QueryInterface` メソッドを呼び出します。 アタッチ プロセスを停止する機会をプログラム ノードに与えるには、[Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)メソッドの前に [OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) メソッドを呼び出す必要があります。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスには、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)|関連付けられているプログラムにアタッチするか、[Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドまでアタッチ プロセスを延期します。|

## <a name="remarks"></a>解説
 非推奨の [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md) メソッドの代わりに、このインターフェイスを使用することをお勧めします。 すべてのデバッグ エンジンは、常に `CoCreateInstance` 関数と共に読み込まれます。つまり、デバッグされているプログラムのアドレス空間の外部でインスタンス化されます。

 `IDebugProgramNode2::Attach_V7` メソッドの以前の実装が、単にデバッグ対象プログラムの `GUID` を設定している場合、実装する必要があるのは [OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) メソッドのみです。

 `IDebugProgramNode2::Attach_V7` メソッドの以前の実装で、提供されたコールバック インターフェイスが使用されていた場合は、その機能を、[Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドの実装に移動する必要があります。`IDebugProgramNodeAttach2` インターフェイスを実装する必要はありません。

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [[アタッチ]](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)
