---
title: IDiaFrameData |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData interface
ms.assetid: 2f1b4986-341b-4641-89a4-226e261e9d93
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d586cfe3e78a320ffed42e7181463eb79a6b313a
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743464"
---
# <a name="idiaframedata"></a>IDiaFrameData
スタックフレームの詳細を公開します。

## <a name="syntax"></a>構文

```
IDiaFrameData : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表は、`IDiaFrameData` のメソッドを示しています。

|メソッド|説明|
|------------|-----------------|
|[IDiaFrameData::get_addressSection](../../debugger/debug-interface-access/idiaframedata-get-addresssection.md)|フレームのコードアドレスのセクション部分を取得します。|
|[IDiaFrameData::get_addressOffset](../../debugger/debug-interface-access/idiaframedata-get-addressoffset.md)|フレームのコードアドレスのオフセット部分を取得します。|
|[IDiaFrameData::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiaframedata-get-relativevirtualaddress.md)|フレームのコードの相対仮想アドレス (RVA) を取得します。|
|[IDiaFrameData::get_virtualAddress](../../debugger/debug-interface-access/idiaframedata-get-virtualaddress.md)|フレームのコードの仮想アドレス (VA) を取得します。|
|[IDiaFrameData::get_lengthBlock](../../debugger/debug-interface-access/idiaframedata-get-lengthblock.md)|フレームによって記述されたコードブロックの長さをバイト単位で取得します。|
|[IDiaFrameData::get_lengthLocals](../../debugger/debug-interface-access/idiaframedata-get-lengthlocals.md)|スタックにプッシュされたローカル変数のバイト数を取得します。|
|[IDiaFrameData::get_lengthParams](../../debugger/debug-interface-access/idiaframedata-get-lengthparams.md)|スタックにプッシュされたパラメーターのバイト数を取得します。|
|[IDiaFrameData::get_maxStack](../../debugger/debug-interface-access/idiaframedata-get-maxstack.md)|フレーム内のスタックにプッシュされる最大バイト数を取得します。|
|[IDiaFrameData::get_lengthProlog](../../debugger/debug-interface-access/idiaframedata-get-lengthprolog.md)|ブロック内のプロローグコードのバイト数を取得します。|
|[IDiaFrameData::get_lengthSavedRegisters](../../debugger/debug-interface-access/idiaframedata-get-lengthsavedregisters.md)|スタックにプッシュされた、保存されたレジスタのバイト数を取得します。|
|[IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)|現在の関数の呼び出しの前にレジスタセットを計算するために使用されるプログラム文字列を取得します。|
|[IDiaFrameData::get_systemExceptionHandling](../../debugger/debug-interface-access/idiaframedata-get-systemexceptionhandling.md)|システム例外処理が有効であることを示すフラグを取得します。|
|[IDiaFrameData::get_cplusplusExceptionHandling](../../debugger/debug-interface-access/idiaframedata-get-cplusplusexceptionhandling.md)|例外処理が有効であるC++ことを示すフラグを取得します。|
|[IDiaFrameData::get_functionStart](../../debugger/debug-interface-access/idiaframedata-get-functionstart.md)|ブロックに関数のエントリポイントが含まれていることを示すフラグを取得します。|
|[IDiaFrameData::get_allocatesBasePointer](../../debugger/debug-interface-access/idiaframedata-get-allocatesbasepointer.md)|このアドレス範囲のコードに対して基本ポインターが割り当てられていることを示すフラグを取得します。 このメソッドは非推奨です。|
|[IDiaFrameData::get_type](../../debugger/debug-interface-access/idiaframedata-get-type.md)|コンパイラ固有のフレームの種類を取得します。|
|[IDiaFrameData::get_functionParent](../../debugger/debug-interface-access/idiaframedata-get-functionparent.md)|外側の関数のフレームデータインターフェイスを取得します。|
|[IDiaFrameData::execute](../../debugger/debug-interface-access/idiaframedata-execute.md)|スタックアンワインドを実行し、スタックウォークフレームインターフェイス内のレジスタの現在の状態を返します。|

## <a name="remarks"></a>Remarks
 フレームに対して使用できる詳細は、アドレスとブロックの長さで示されるアドレス範囲内の実行ポイントです。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスを取得するには、 [IDiaEnumFrameData:: Next](../../debugger/debug-interface-access/idiaenumframedata-next.md)メソッドまたは[IDiaEnumFrameData:: Item](../../debugger/debug-interface-access/idiaenumframedata-item.md)メソッドを呼び出します。 詳細については、 [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)インターフェイスを参照してください。

## <a name="example"></a>例
 この例では、`IDiaFrameData` オブジェクトのプロパティを出力します。 @No__t_1 インターフェイスの取得方法の例については、 [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)インターフェイスを参照してください。

```C++
void PrintFrameData(IDiaFrameData* pFrameData){
    DWORD dwSect;
    DWORD dwOffset;
    DWORD cbBlock;
    DWORD cbLocals; // Number of bytes reserved for the function locals
    DWORD cbParams; // Number of bytes reserved for the function arguments
    DWORD cbMaxStack;
    DWORD cbProlog;
    DWORD cbSavedRegs;
    BOOL  bSEH;
    BOOL  bEH;
    BOOL  bStart;
    BSTR  wszProgram;

    if(pFrameData->get_addressSection(&dwSect) == S_OK &&
       pFrameData->get_addressOffset(&dwOffset) == S_OK &&
       pFrameData->get_lengthBlock(&cbBlock) == S_OK &&
       pFrameData->get_lengthLocals(&cbLocals) == S_OK &&
       pFrameData->get_lengthParams(&cbParams) == S_OK &&
       pFrameData->get_maxStack(&cbMaxStack) == S_OK &&
       pFrameData->get_lengthProlog(&cbProlog) == S_OK &&
       pFrameData->get_lengthSavedRegisters(&cbSavedRegs) == S_OK &&
       pFrameData->get_systemExceptionHandling(&bSEH) == S_OK &&
       pFrameData->get_cplusplusExceptionHandling(&bEH) == S_OK &&
       pFrameData->get_functionStart(&bStart) == S_OK )
    {
        wprintf(L"Frame address  : %04X:%08X\n", dwSect, dwOffset);
        wprintf(L"Block size     : 0x%8X\n", cbBlock);
        wprintf(L"Locals size    : 0x%8X\n", cbLocals);
        wprintf(L"Parms size     : 0x%8X\n", cbParams);
        wprintf(L"Max stack used : 0x%8X\n", cbMaxStack);
        wprintf(L"Prolog size    : 0x%8X\n", cbProlog);
        wprintf(L"Saved regs size: 0x%8X\n", cbSavedRegs);
        wprintf(L"System Exception Handling: %c\n", bSEH ? L'Y' : L'N');
        wprintf(L"C++ Exception Handling   : %c\n", bEH ? L'Y' : L'N');
        wprintf(L"Function starts in block : %c\n", bStart ? L'Y' : L'N');

        if (pFrameData->get_program(&wszProgram) == S_OK)
        {
            wprintf(L"Program used for register set: %s\n", wszProgram);
            SysFreeString(wszProgram);
        }
        else
        {
            wprintf(L"\n");
        }
    }
}
```

## <a name="requirements"></a>［要件］
ヘッダー: Dia2

ライブラリ: diaguids

DLL: msdia80

## <a name="see-also"></a>関連項目
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)
- [IDiaEnumFrameData::Item](../../debugger/debug-interface-access/idiaenumframedata-item.md)
- [IDiaEnumFrameData::Next](../../debugger/debug-interface-access/idiaenumframedata-next.md)
