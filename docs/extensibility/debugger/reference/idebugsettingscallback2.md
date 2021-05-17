---
description: デバッグ エンジンが、リモートでメトリック設定を読み取れるようにします。
title: IDebugSettingsCallback2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2 interface
ms.assetid: 7e525d0b-7d7a-4d1c-8b78-e1398fa922f2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 58e9ddfd3789fcfe7d81348714a8de2add743090
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071195"
---
# <a name="idebugsettingscallback2"></a>IDebugSettingsCallback2
デバッグ エンジンが、リモートでメトリック設定を読み取れるようにします。

## <a name="syntax"></a>構文

```
IDebugSettingsCallback2D : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
このインターフェイスは、セッション デバッグ マネージャーのイベント コールバックによって実装され、デバッグ エンジンによって使用されます。 また、Dbgmetric[d].lib の代わりにローカルで使用することもできます。

## <a name="methods"></a>メソッド
次の表に、`IDebugSettingsCallback2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[EnumEEs](../../../extensibility/debugger/reference/idebugsettingscallback2-enumees.md)|言語およびベンダー識別子を指定した場合に、使用可能な式エバリュエーターを列挙します。|
|[GetEELocalObject](../../../extensibility/debugger/reference/idebugsettingscallback2-geteelocalobject.md)|メトリックを指定した場合に、式エバリュエーターのローカル オブジェクトを取得します。|
|[GetEEMetricDword](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricdword.md)|式エバリュエーターの指定されたメトリックに対応する値を取得します。|
|[GetEEMetricFile](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricfile.md)|名前またはメトリックを指定した場合に、式エバリュエーターのメトリック ファイルを取得します。|
|[GetEEMetricGuid](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricguid.md)|名前を指定した場合に、式エバリュエーター メトリックの一意の識別子を取得します。|
|[GetEEMetricString](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricstring.md)|名前を指定した場合に、式エバリュエーター メトリックの値文字列を取得します。|
|[GetMetricDword](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricdword.md)|名前を指定した場合に、メトリックの値を取得します。|
|[GetMetricGuid](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricguid.md)|名前を指定した場合に、メトリックの一意の識別子を取得します。|
|[GetMetricString](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricstring.md)|名前を指定した場合に、メトリックの値文字列を取得します。|

## <a name="requirements"></a>必要条件
ヘッダー: Msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>例
次の例は、**IDebugSettingsCallback2** オブジェクトをパラメーターとして受け取る関数を示しています。

```cpp
HRESULT GetDebugSettingsCallback (IDebugSettingsCallback2 **ppCallback)
{
    HRESULT hRes = E_FAIL;

    if ( ppCallback )
    {
        if ( EVAL(m_pdec) )
            hRes = m_pdec->QueryInterface(IID_IDebugSettingsCallback2, (void **)ppCallback);
        else
            hRes = E_FAIL;
    }
    else
        hRes = E_INVALIDARG;

    return ( hRes );
}
```
