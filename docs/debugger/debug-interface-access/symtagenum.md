---
description: シンボルの種類を指定します。
title: SymTagEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- SymTagEnum enumeration
ms.assetid: 528a50cf-e13d-46ec-a98c-323d5d047de9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 72d07b0609fd9d66507c898854810043f2911e0c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635198"
---
# <a name="symtagenum"></a>SymTagEnum
シンボルの種類を指定します。

## <a name="syntax"></a>構文

```C++
enum SymTagEnum {
    SymTagNull,
    SymTagExe,
    SymTagCompiland,
    SymTagCompilandDetails,
    SymTagCompilandEnv,
    SymTagFunction,
    SymTagBlock,
    SymTagData,
    SymTagAnnotation,
    SymTagLabel,
    SymTagPublicSymbol,
    SymTagUDT,
    SymTagEnum,
    SymTagFunctionType,
    SymTagPointerType,
    SymTagArrayType,
    SymTagBaseType,
    SymTagTypedef,
    SymTagBaseClass,
    SymTagFriend,
    SymTagFunctionArgType,
    SymTagFuncDebugStart,
    SymTagFuncDebugEnd,
    SymTagUsingNamespace,
    SymTagVTableShape,
    SymTagVTable,
    SymTagCustom,
    SymTagThunk,
    SymTagCustomType,
    SymTagManagedType,
    SymTagDimension,
    SymTagCallSite,
    SymTagInlineSite,
    SymTagBaseInterface,
    SymTagVectorType,
    SymTagMatrixType,
    SymTagHLSLType
};
```

## <a name="elements"></a>要素
`SymTagNull`: シンボルの種類がないことを示します。

`SymTagExe`: シンボルが .exe ファイルであることを示します。 `SymTagExe` シンボルの数はシンボル ストアごとに 1 つだけです。 グローバル スコープとして機能し、構文上の親はありません。

`SymTagCompiland`: シンボル ストアの各コンパイル単位コンポーネントのコンパイル単位シンボルを示します。 ネイティブ アプリケーションの場合、`SymTagCompiland` シンボルは、イメージにリンクされたオブジェクト ファイルに対応します。 一部の種類の Microsoft 中間言語 (MSIL) イメージの場合、クラスごとに 1 つのコンパイル単位があります。

`SymTagCompilandDetails`: シンボルにコンパイル単位の拡張属性が含まれていることを示します。 これらのプロパティを取得するには、コンパイル単位シンボルの読み込みが必要になることがあります。

`SymTagCompilandEnv`: シンボルが、コンパイル単位に対して定義された環境文字列であることを示します。

`SymTagFunction`: シンボルが関数であることを示します。

`SymTagBlock`: シンボルが入れ子になったブロックであることを示します。

`SymTagData`: シンボルがデータであることを示します。

`SymTagAnnotation`: シンボルがコード注釈用であることを示します。 このシンボルの子は定数データ文字列 (`SymTagData`、`LocIsConstant`、`DataIsConstant`) です。 ほとんどのクライアントはこのシンボルを無視します。

`SymTagLabel`: シンボルがラベルであることを示します。

`SymTagPublicSymbol`: シンボルがパブリック シンボルであることを示します。 ネイティブ アプリケーションの場合、このシンボルは、イメージのリンク時に検出された COFF 外部シンボルです。

`SymTagUDT`: シンボルがユーザー定義型 (構造体、クラス、または共用体) であることを示します。

`SymTagEnum`: シンボルが列挙であることを示します。

`SymTagFunctionType`: シンボルが関数シグネチャ型であることを示します。

`SymTagPointerType`: シンボルがポインター型であることを示します。

`SymTagArrayType`: シンボルが配列型であることを示します。

`SymTagBaseType`: シンボルが基本データ型であることを示します。

`SymTagTypedef`: シンボルが `typedef`、つまり別の型の別名であることを示します。

`SymTagBaseClass`: シンボルがユーザー定義型の基底クラスであることを示します。

`SymTagFriend`: シンボルがユーザー定義型のフレンドであることを示します。

`SymTagFunctionArgType`: シンボルが関数の引数であることを示します。

`SymTagFuncDebugStart`: シンボルが関数のプロローグ コードの終了位置であることを示します。

`SymTagFuncDebugEnd`: シンボルが関数のエピローグ コードの開始位置であることを示します。

`SymTagUsingNamespace`: シンボルが現在のスコープ内でアクティブな名前空間の名前であることを示します。

`SymTagVTableShape`: シンボルが仮想テーブルの説明であることを示します。

`SymTagVTable`: シンボルが仮想テーブルのポインターであることを示します。

`SymTagCustom`: シンボルがカスタム シンボルであり、DIA によって解釈されないことを示します。

`SymTagThunk`: シンボルが 16 ビット コードと 32 ビット コードの間でデータを共有するために使用されるサンクであることを示します。

`SymTagCustomType`: シンボルがカスタム コンパイラのシンボルであることを示します。

`SymTagManagedType`: シンボルがメタデータ内にあることを示します。

`SymTagDimension`: シンボルが FORTRAN 多次元配列であることを示します。

`SymTagCallSite`: シンボルが呼び出しサイトを表すことを示します。

`SymTagInlineSite`: シンボルがインライン サイトを表すことを示します。

`SymTagBaseInterface`: シンボルが基底インターフェイスであることを示します。

`SymTagVectorType`: シンボルがベクター型であることを示します。

`SymTagMatrixType`: シンボルがマトリックス型であることを示します。

`SymTagHLSLType`: シンボルが High Level Shader Language 型であることを示します。

## <a name="remarks"></a>解説
デバッグ ファイル内のすべてのシンボルには、シンボルの種類を指定する識別タグがあります。

この列挙の値は、[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md) メソッドへの呼び出しによって返されます。

この列挙の値は、検索のスコープを特定のシンボルの種類に制限するために、次のメソッドに渡されます。

- [IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)

- [IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)

- [IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)

- [IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)

- [IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)

- [IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)

- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)

- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)

## <a name="requirements"></a>要件
ヘッダー: cvconst.h

## <a name="see-also"></a>こちらもご覧ください
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
- [IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)
- [IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)
- [IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)
- [IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)
- [IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)
- [IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
