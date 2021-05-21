---
description: ソース ファイル内の指定された行番号が内部または近くにあるコンパイル単位の行番号を特定します。
title: IDiaSession::findLinesByLinenum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findLinesByLinenum method
ms.assetid: 76d5622d-9a91-4c2a-a98f-263af5d1daef
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 924b3aada49fca11056a1cf7f1b577bab505b3ce
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634315"
---
# <a name="idiasessionfindlinesbylinenum"></a>IDiaSession::findLinesByLinenum
ソース ファイル内の指定された行番号が内部または近くにあるコンパイル単位の行番号を特定します。

## <a name="syntax"></a>構文

```C++
HRESULT findLinesByLinenum ( 
    IDiaSymbol*           compiland,
    IDiaSourceFile*       file,
    DWORD                 linenum,
    DWORD                 column,
    IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>パラメーター
`compiland`

[入力] 行番号を検索するコンパイル単位を表す [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクト。 このパラメーターを `NULL` とすることはできません。

`file`

[入力] 検索対象のソース ファイルを表す [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md) オブジェクト。 このパラメーターを `NULL` とすることはできません。

`linenum`

[入力] 1 から始まる行番号を指定します。

> [!NOTE]
> 0 を使用してすべての行を指定することはできません (すべての行を検索するには、[IDiaSession::findLines](../../debugger/debug-interface-access/idiasession-findlines.md) メソッドを使用します)。

`column`

[入力] 列番号を指定します。 すべての列を指定するには 0 を使用します。 列は行へのバイト オフセットです。

`ppResult`

[出力] 取得した行番号のリストを含む [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="example"></a>例
次の例は、ソース ファイルを開き、このファイルによって提供されるコンパイル単位を列挙し、各コンパイル単位が始まるソース ファイル内の行番号を見つける方法を示しています。

```C++
void ShowLinesInCompilands(IDiaSession *pSession, LPCOLESTR filename)
{
    IDiaEnumSourceFiles* pEnum;
    IDiaSourceFile*      pFile;
    DWORD                celt;

    pSession->findFile ( NULL, filename, nsFNameExt, &pEnum );
    while ( pEnum->Next ( 1, &pFile, &celt ) == S_OK ) // for each file
    {
        IDiaEnumSymbols* pEnumCompilands;
        IDiaSymbol* pCompiland;

        pFile->get_compilands ( &pEnumCompilands );
        // for each compiland
        while ( pEnumCompilands->Next ( 1, &pCompiland, &celt ) == S_OK )
        {
            IDiaEnumLineNumbers* pEnum;
            // Find first compiland closest to line 1 of the file.
            if (pSession->findLinesByLinenum( pCompiland, pFile, 1, 0, &pEnum ) == S_OK)
            {
                IDiaLineNumber *pLineNumber;
                DWORD lineCount;
                while ( pEnum->Next(1,&pLineNumber,&lineCount) == S_OK)
                {
                    DWORD lineNum;
                    if (pLineNumber->get_line(&lineNum) == S_OK)
                    {
                        printf("compiland starts in source at line number = %lu\n",lineNum);
                    }
                }
            }
        }
    }
}
```

## <a name="see-also"></a>関連項目
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSession::findLinesByAddr](../../debugger/debug-interface-access/idiasession-findlinesbyaddr.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
