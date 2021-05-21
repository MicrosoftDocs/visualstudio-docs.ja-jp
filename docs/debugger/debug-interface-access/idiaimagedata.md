---
description: モジュールまたはイメージの基本場所とメモリ オフセットの詳細を公開します。
title: IDiaImageData | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaImageData interface
ms.assetid: b696f350-fc08-4352-9287-a15e87512c1e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c8cee712f393c3b006484eeda4a0ec1033c1f26b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634891"
---
# <a name="idiaimagedata"></a>IDiaImageData
モジュールまたはイメージの基本場所とメモリ オフセットの詳細を公開します。

## <a name="syntax"></a>構文

```
IDiaImageData : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表に、`IDiaImageData` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[IDiaImageData::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiaimagedata-get-relativevirtualaddress.md)|アプリケーションを基準とする、モジュールの仮想メモリ内の場所を取得します。|
|[IDiaImageData::get_virtualAddress](../../debugger/debug-interface-access/idiaimagedata-get-virtualaddress.md)|イメージの仮想メモリ内の場所を取得します。|
|[IDiaImageData::get_imageBase](../../debugger/debug-interface-access/idiaimagedata-get-imagebase.md)|イメージのベースとなるメモリの場所を取得します。|

## <a name="remarks"></a>解説
一部のデバッグ ストリーム (XDATA、PDATA) には、イメージに保存されているデータのコピーが含まれています。 これらのストリーム データ オブジェクトに対して、`IDiaImageData` インターフェイスのクエリを実行できます。 詳細については、このトピックの「呼び出し元に関する注意事項」を参照してください。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
このインターフェイスを取得するには、[IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md) オブジェクトに対して `QueryInterface` を呼び出します。 すべてのデバッグ ストリームで `IDiaImageData` インターフェイスがサポートされているわけではないことに注意してください。 たとえば、現時点で `IDiaImageData` インターフェイスをサポートしているのは、XDATA および PDATA ストリームだけです。

## <a name="example"></a>例
この例では、すべてのデバッグ ストリームを対象に、`IDiaImageData` インターフェイスをサポートするストリームを検索します。 そのようなストリームが見つかった場合は、そのストリームに関する情報が表示されます。

```C++
void ShowImageData(IDiaSession *pSession)
{
    if (pSession != NULL)
    {
        CComPtr<IDiaEnumDebugStreams> pStreamsList;
        HRESULT hr;

        hr = pSession->getEnumDebugStreams(&pStreamsList);
        if (SUCCEEDED(hr))
        {
            LONG numStreams = 0;
            hr = pStreamsList->get_Count(&numStreams);
            if (SUCCEEDED(hr))
            {
                ULONG fetched = 0;
                for (LONG i = 0; i < numStreams; i++)
                {
                    CComPtr<IDiaEnumDebugStreamData> pStream;
                    hr = pStreamsList->Next(1,&pStream,&fetched);
                    if (fetched == 1)
                    {
                        CComPtr<IDiaImageData> pImageData;
                        hr = pStream->QueryInterface(__uuidof(IDiaImageData),
                                                     (void **)&pImageData);
                        if (SUCCEEDED(hr))
                        {
                            CComBSTR name;
                            hr = pStream->get_name(&name);
                            if (SUCCEEDED(hr))
                            {
                                wprintf(L"Stream %s:\n",(BSTR)name);
                            }
                            else
                            {
                                wprintf(L"Failed to get name of stream\n");
                            }

                            ULONGLONG imageBase = 0;
                            if (pImageData->get_imageBase(&imageBase) == S_OK)
                            {
                                wprintf(L"  image base = 0x%0I64x\n",imageBase);
                            }

                            DWORD relVA = 0;
                            if (pImageData->get_relativeVirtualAddress(&relVA) == S_OK)
                            {
                                wprintf(L"  relative virtual address = 0x%08lx\n",relVA);
                            }

                            ULONGLONG va = 0;
                            if (pImageData->get_virtualAddress(&va) == S_OK)
                            {
                                wprintf(L"  virtual address = 0x%0I64x\n", va);
                            }
                        }
                    }
                }
            }
        }
    }
}
```

## <a name="requirements"></a>必要条件
ヘッダー: Dia2.h

ライブラリ: diaguids.lib

DLL: msdia80.dll

## <a name="see-also"></a>関連項目
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)
