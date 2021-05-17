---
description: 次の表に、構文階層内のシンボル型を示します。
title: シンボル型の構文階層 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- symbols [DIA SDK], type hierarchies
ms.assetid: 912da653-ddfe-45a4-84aa-64281283739a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 605b16d2a53178b52095e9919c10bba53f3f21a1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634568"
---
# <a name="lexical-hierarchy-of-symbol-types"></a>シンボル型の構文階層
次の表に、構文階層内のシンボル型を示します。

## <a name="symbol-types"></a>シンボル型

|シンボル型|説明|
|-----------------|-----------------|
|[注釈](../../debugger/debug-interface-access/annotation.md)|プログラム コード内の注釈付きの場所を指定します。|
|[ブロック](../../debugger/debug-interface-access/block.md)|関数内の入れ子になったスコープを指定します。|
|`Compiland`|.exe ファイルにリンクされた `compiland` を指定します。|
|[CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md)|コンパイル単位の追加情報の読み込みを必要とする可能性があり、したがって取得するには実行時のオーバーヘッドが発生する可能性がある、コンパイル単位データを指定します。|
|[CompilandEnv](../../debugger/debug-interface-access/compilandenv.md)|コンパイル単位のコンパイルにとって重要な追加の環境変数を指定します。|
|[カスタム (Debug Interface Access SDK)](../../debugger/debug-interface-access/custom-debug-interface-access-sdk.md)|ユーザー定義のシンボルを指定します。|
|[データ (Debug Interface Access SDK)](../../debugger/debug-interface-access/data-debug-interface-access-sdk.md)|パラメーター、ローカル変数、グローバル変数、クラス メンバーといった変数を指定します。|
|[Exe](../../debugger/debug-interface-access/exe.md)|データのグローバル スコープを指定します。 .exe ファイルまたは .dll ファイル全体に相当します。|
|[FuncDebugEnd](../../debugger/debug-interface-access/funcdebugend.md)|デバッグを終了するポイントが定義されている関数を指定します。|
|[FuncDebugStart](../../debugger/debug-interface-access/funcdebugstart.md)|デバッグを開始するポイントが定義されている関数を指定します。|
|[関数 (Debug Interface Access SDK)](../../debugger/debug-interface-access/function-debug-interface-access-sdk.md)|関数を指定します。|
|[ラベル (Debug Interface Access SDK)](../../debugger/debug-interface-access/label-debug-interface-access-sdk.md)|プログラム コード内の場所を指定します。|
|[PublicSymbol](../../debugger/debug-interface-access/publicsymbol.md)|実行可能プログラムのビルド中に出現する外部シンボルを指定します。|
|[サンク](../../debugger/debug-interface-access/thunk.md)|`thunk` を指定します。|
|[UsingNameSpace](../../debugger/debug-interface-access/usingnamespace.md)|`namespace` 識別子を指定します。|

> [!NOTE]
> シンボルの種類によっては、追加のシンボル プロパティを使用できる場合があります。 これらのプロパティの一覧については、個々のシンボルのトピックを参照してください。

## <a name="see-also"></a>関連項目
- [シンボル型のクラス階層](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)
- [IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)
- [シンボルとシンボル タグ](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)
- [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
