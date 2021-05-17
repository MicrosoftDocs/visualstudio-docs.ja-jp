---
description: このインターフェイスにより、式エバリュエーター (EE) では必要な形式でプロパティの値を表示できます。
title: IDebugCustomViewer | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomViewer
helpviewer_keywords:
- IDebugCustomViewer interface
ms.assetid: 7aca27d3-c7b8-470f-b42c-d1e9d9115edd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3c44706549d7d638a8fbf3686de57780ffa6bf4e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077552"
---
# <a name="idebugcustomviewer"></a>IDebugCustomViewer
このインターフェイスにより、式エバリュエーター (EE) では必要な形式でプロパティの値を表示できます。

## <a name="syntax"></a>構文

```
IDebugCustomViewer : IUknown
```

## <a name="notes-for-implementers"></a>実装側の注意
EE では、このインターフェイスを実装して、プロパティの値をカスタム書式で表示します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
COM の `CoCreateInstance` 関数を呼び出すと、このインターフェイスがインスタンス化されます。 `CoCreateInstance` に渡される `CLSID` はレジストリから取得されます。 [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) を呼び出すと、レジストリ内の場所が取得されます。 詳細と例については、「解説」を参照してください。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
このインターフェイスには、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[DisplayValue](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)|指定された値を表示するために必要な処理を実行します。|

## <a name="remarks"></a>解説
このインターフェイスは、通常の方法 (たとえば、データ テーブルやその他の複合プロパティ型を使用) ではプロパティの値を表示できない場合に使用されます。 `IDebugCustomViewer` インターフェイスによって表されるカスタム ビューアーは、型ビジュアライザー (EE に関係なく特定の型のデータを表示するための外部プログラム) とは異なります。 EE には、その EE に固有のカスタム ビューアーが実装されています。 ユーザーは、使用するビジュアライザーの種類として、型ビジュアライザーまたはカスタム ビューアーを選択します。 このプロセスの詳細については、「[データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)」を参照してください。

カスタム ビューアーは、EE と同じ方法で登録されるため、言語 GUID とベンダー GUID が必要です。 正確なメトリック (またはレジストリ エントリ名) は、EE にのみ認識されます。 このメトリックは [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md) 構造体で返され、この構造体は [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) の呼び出しによって返されます。 メトリックに格納される値は、COM の `CoCreateInstance` 関数に渡される `CLSID` です (「例」を参照)。

[デバッグ用の SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)関数 (`SetEEMetric`) を使用して、カスタム ビューアーを登録できます。 カスタム ビューアーで必要な特定のレジストリ キーについては、「`Debugging SDK Helpers`」の式エバリュエーターに関するレジストリ セクションを参照してください。 カスタム ビューアーに必要なメトリックは 1 つだけですが (これは EE の実装者が定義します)、式エバリュエーターにはいくつかの定義済みメトリックが必要です。

[Displayvalue](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md) に渡される [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) インターフェイスには、文字列以外のプロパティ値を変更するメソッドがないため、通常、カスタム ビューアーには、データの読み取り専用ビューが用意されています。 任意のデータ ブロックの変更をサポートするために、EE では、`IDebugProperty3` インターフェイスを実装するのと同じオブジェクトにカスタム インターフェイスを実装します。 このカスタム インターフェイスには、任意のデータ ブロックを変更するために必要なメソッドを用意します。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>例
この例では、プロパティに任意のカスタム ビューアーが含まれている場合に、そのプロパティから最初のカスタム ビューアーを取得する方法を示します。

```cpp
IDebugCustomViewer *GetFirstCustomViewer(IDebugProperty2 *pProperty)
{
    // This string is typically defined globally.  For this example, it
    // is defined here.
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";
    IDebugCustomViewer *pViewer = NULL;
    if (pProperty != NULL) {
        CComQIPtr<IDebugProperty3> pProperty3(pProperty);
        if (pProperty3 != NULL) {
            HRESULT hr;
            ULONG viewerCount = 0;
            hr = pProperty3->GetCustomViewerCount(&viewerCount);
            if (viewerCount > 0) {
                ULONG viewersFetched = 0;
                DEBUG_CUSTOM_VIEWER viewerInfo = { 0 };
                hr = pProperty3->GetCustomViewerList(0,
                                                     1,
                                                     &viewerInfo,
                                                     &viewersFetched);
                if (viewersFetched == 1) {
                    CLSID clsidViewer = { 0 };
                    CComPtr<IDebugCustomViewer> spCustomViewer;
                    // Get the viewer's CLSID from the registry.
                    ::GetEEMetric(viewerInfo.guidLang,
                                  viewerInfo.guidVendor,
                                  viewerInfo.bstrMetric,
                                  &clsidViewer,
                                  strRegistrationRoot);
                    if (!IsEqualGUID(clsidViewer,GUID_NULL)) {
                        // Instantiate the custom viewer.
                        spCustomViewer.CoCreateInstance(clsidViewer);
                        if (spCustomViewer != NULL) {
                            pViewer = spCustomViewer.Detach();
                        }
                    }
                }
            }
        }
    }
    return(pViewer);
}
```

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)
- [デバッグ用 SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
