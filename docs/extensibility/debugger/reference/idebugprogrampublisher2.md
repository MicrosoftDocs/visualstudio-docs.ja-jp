---
description: このインターフェイスによって、デバッグ エンジン (DE) またはカスタム ポート サプライヤーでデバッグ用のプログラムを登録できます。
title: IDebugProgramPublisher2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2
helpviewer_keywords:
- IDebugProgramPublisher2 interface
ms.assetid: b1d17f63-7146-4076-a588-034cfc6858b9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c51fac369ed91f00c91482dd7069362d758b7346
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065100"
---
# <a name="idebugprogrampublisher2"></a>IDebugProgramPublisher2
このインターフェイスによって、デバッグ エンジン (DE) またはカスタム ポート サプライヤーでデバッグ用のプログラムを登録できます。

## <a name="syntax"></a>構文

```
IDebugProgramPublisher2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
Visual Studio では、デバッグ中のプログラムを登録して、複数のプロセスからデバッグ目的で参照できるようにするために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
このインターフェイスを取得するには、`CLSID_ProgramPublisher` を指定して COM の `CoCreateInstance` 関数を呼び出します (例を参照)。 DE またはカスタム ポート サプライヤーでは、このインターフェイスを使用して、デバッグ中のプログラムを表すプログラム ノードを登録します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
このインターフェイスには、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[PublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)|プログラム ノードを DE およびセッション デバッグ マネージャー (SDM) で使用可能にします。|
|[UnpublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogramnode.md)|プログラム ノードを削除して使用不可にします。|
|[PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md)|プログラムを DE および SDM で使用可能にします。|
|[UnpublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogram.md)|プログラムを削除して使用不可にします。|
|[SetDebuggerPresent](../../../extensibility/debugger/reference/idebugprogrampublisher2-setdebuggerpresent.md)|デバッガーの存在を示すフラグを設定します。|

## <a name="remarks"></a>解説
このインターフェイスは、プログラムおよびプログラム ノードを DE やセッション デバッグ マネージャー (SDM) で使用できるようにします (つまり "公開" します)。 公開されたプログラムおよびプログラム ノードにアクセスするには、[IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md) インターフェイスを使用します。 これは、プログラムがデバッグ中であることを Visual Studio が認識できる唯一の方法です。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>例
この例は、プログラムの公開元をインスタンス化してプログラム ノードを登録する方法を示しています。 これは、[プログラム ノードの公開](/previous-versions/bb161795(v=vs.90))に関するチュートリアルからの引用です。

```cpp
// This is how m_srpProgramPublisher is defined in the class definition:
// CComPtr<IDebugProgramPublisher2> m_srpProgramPublisher.

void CProgram::Start(IDebugEngine2 * pEngine)
{
    m_spEngine = pEngine;

    HRESULT hr = m_srpProgramPublisher.CoCreateInstance(CLSID_ProgramPublisher);
    if ( FAILED(hr) )
    {
        ATLTRACE("Failed to create the program publisher: 0x%x.", hr);
        return;
    }

    // Register ourselves with the program publisher. Note that
    // CProgram implements the IDebgProgramNode2 interface, hence
    // the static cast on "this".
    hr = m_srpProgramPublisher->PublishProgramNode(
        static_cast<IDebugProgramNode2*>(this));
    if ( FAILED(hr) )
    {
        ATLTRACE("Failed to publish the program node: 0x%x.", hr);
        m_srpProgramPublisher.Release();
        return;
    }

    ATLTRACE("Added program node.\n");
}
```

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
