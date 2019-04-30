---
title: シンボル型の構文階層 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- symbols [DIA SDK], type hierarchies
ms.assetid: 912da653-ddfe-45a4-84aa-64281283739a
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e70b83046c41b13cb51324eb63e81b26a118a81f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63403502"
---
# <a name="lexical-hierarchy-of-symbol-types"></a>シンボル型の構文階層
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

次の表では、構文の階層でシンボルの型を示します。  
  
## <a name="symbol-types"></a>シンボル型  
  
|記号の型|説明|  
|-----------------|-----------------|  
|[注釈](../../debugger/debug-interface-access/annotation.md)|プログラム コードでは、注釈付きの場所を指定します。|  
|[ブロック](../../debugger/debug-interface-access/block.md)|関数では、入れ子になったスコープを指定します。|  
|`Compiland`|指定します、 `compiland` .exe ファイルにリンクさせます。|  
|[CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md)|コンパイル単位のデータを追加のコンパイル単位の詳細を読み込んでを必要としを取得するため実行時のオーバーヘッドが発生する可能性がありますを指定します。|  
|[CompilandEnv](../../debugger/debug-interface-access/compilandenv.md)|コンパイル単位をコンパイルする重要な追加の環境変数を指定します。|  
|[カスタム (Debug Interface Access SDK)](../../debugger/debug-interface-access/custom-debug-interface-access-sdk.md)|ユーザー定義の記号を指定します。|  
|[データ (Debug Interface Access SDK)](../../debugger/debug-interface-access/data-debug-interface-access-sdk.md)|パラメーター、ローカル変数、グローバル変数、およびクラス メンバーとして、このような変数を指定します。|  
|[Exe](../../debugger/debug-interface-access/exe.md)|は、データのグローバル スコープを指定します.exe または .dll のファイル全体に対応します。|  
|[FuncDebugEnd](../../debugger/debug-interface-access/funcdebugend.md)|定義されたポイントを持つ関数を指定します。 デバッグするには、終了します。|  
|[FuncDebugStart](../../debugger/debug-interface-access/funcdebugstart.md)|定義されたポイントを持つ関数を指定するデバッグでは、開始します。|  
|[関数 (Debug Interface Access SDK)](../../debugger/debug-interface-access/function-debug-interface-access-sdk.md)|関数を指定します。|  
|[ラベル (Debug Interface Access SDK)](../../debugger/debug-interface-access/label-debug-interface-access-sdk.md)|プログラム コードでは、場所を指定します。|  
|[PublicSymbol](../../debugger/debug-interface-access/publicsymbol.md)|実行可能プログラムを作成するときに表示される外部シンボルを指定します。|  
|[サンク](../../debugger/debug-interface-access/thunk.md)|指定します、`thunk`します。|  
|[UsingNameSpace](../../debugger/debug-interface-access/usingnamespace.md)|指定します、`namespace`識別子。|  
  
> [!NOTE]
> その他のシンボル プロパティは、シンボルの種類に応じてできる場合があります。 これらのプロパティは、個々 のシンボルのトピックに表示されます。  
  
## <a name="see-also"></a>関連項目  
 [シンボル型のクラス階層](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)   
 [IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)   
 [シンボルとシンボル タグ](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)   
 [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
