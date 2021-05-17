---
description: この登録済みインターフェイスにより、セッション デバッグ マネージャー (SDM) で、IDebugProgramPublisher2 インターフェイスを通じて公開されたプログラムに関する情報を取得できます。
title: IDebugProgramProvider2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramProvider2
helpviewer_keywords:
- IDebugProgramProvider2 interface
ms.assetid: a9ec7b3e-a59c-4069-b2ee-6f45916eeb78
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5bead60e23c708d8a23fcd382b4db0f3f9f7e4c1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065243"
---
# <a name="idebugprogramprovider2"></a>IDebugProgramProvider2
この登録済みインターフェイスにより、セッション デバッグ マネージャー (SDM) で、[IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md) インターフェイスを通じて "公開" されたプログラムに関する情報を取得できます。

## <a name="syntax"></a>構文

```
IDebugProgramProvider2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
デバッグ エンジン (DE) では、デバッグ中のプログラムに関する情報を提供するために、このインターフェイスを実装します。 このインターフェイスは、「[デバッグ用の SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)」で説明されているように、メトリック `metricProgramProvider` を使用してレジストリの DE セクションに登録されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
レジストリから取得した、プログラム プロバイダーの `CLSID` を指定して COM の `CoCreateInstance` 関数を呼び出します。 「例」を参照してください。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド

|メソッド|説明|
|------------|-----------------|
|[GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)|実行中のプログラムに関する情報を、さまざまな方法でフィルター処理して取得します。|
|[GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)|特定のプロセス ID を指定してプログラム ノードを取得します。|
|[WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)|特定の種類のプロセスに関連付けられたプロバイダー イベントを監視するためのコールバックを設定します。|
|[SetLocale](../../../extensibility/debugger/reference/idebugprogramprovider2-setlocale.md)|DE で必要とされる言語固有リソースのロケールを設定します。|

## <a name="remarks"></a>解説
通常、プロセスではこのインターフェイスを使用して、そのプロセスで実行されているプログラムに関する情報を確認します。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>例

```cpp
IDebugProgramProvider2 *GetProgramProvider(GUID *pDebugEngineGuid)
{
    // This is typically defined globally. For this example, it is
    // defined here.
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";
    IDebugProgramProvider2 *pProvider = NULL;
    if (pDebugEngineGuid != NULL) {
        CLSID clsidProvider = { 0 };
        ::GetMetric(NULL,
                    metrictypeEngine,
                    *pDebugEngineGuid,
                    metricProgramProvider,
                    &clsidProvider,
                    strRegistrationRoot);
        if (!IsEqualGUID(clsidProvider,GUID_NULL)) {
            CComPtr<IDebugProgramProvider2> spProgramProvider;
            spProgramProvider.CoCreateInstance(clsidProvider);
            if (spProgramProvider != NULL) {
                pProvider = spProgramProvider.Detach();
            }
        }
    }
    return(pProvider);
}
```

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)
- [デバッグ用 SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
