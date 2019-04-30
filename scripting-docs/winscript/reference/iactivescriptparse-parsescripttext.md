---
title: Iactivescriptparse::parsescripttext |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptParse.ParseScriptText
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptParse_ParseScriptText
ms.assetid: 2d237d6c-cc65-415b-8808-72791304a136
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3396aee8c044ee9b84d7d6256c6ad69a99965170
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62954891"
---
# <a name="iactivescriptparseparsescripttext"></a>IActiveScriptParse::ParseScriptText
指定したコード スクリプトレットを解析することで、宣言を名前空間に追加し、必要に応じてコードを評価します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT ParseScriptText(  
    LPCOLESTR pstrCode,              // address of scriptlet text  
    LPCOLESTR pstrItemName,          // address of item name  
    IUnknown *punkContext,           // address of debugging context  
    LPCOLESTR pstrDelimiter,         // address of end-of-scriptlet delimiter  
    DWORD_PTR dwSourceContextCookie, // cookie for debugging  
    ULONG ulStartingLineNumber,      // starting line of the script  
    DWORD dwFlags,                   // scriptlet flags  
    VARIANT *pvarResult,             // address of buffer for results  
    EXCEPINFO *pexcepinfo            // address of buffer for error data  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
  
|||  
|-|-|  
|`pstrCode`|[入力] 評価するスクリプトレット テキストのアドレス。 この文字列の解釈はスクリプト言語によって異なります。|  
|`pstrItemName`|[入力] スクリプトレットが評価されるコンテキストを指定する項目名のアドレス。 このパラメーターが NULL の場合、コードはスクリプト エンジンのグローバル コンテキストで評価されます。|  
|`punkContext`|[入力] コンテキスト オブジェクトのアドレス。 このオブジェクトはデバッグ環境用に予約されています。アクティブなランタイム コンテキストを表すためにデバッガーによって指定される場合があります。 このパラメーターが NULL の場合、エンジンは `pstrItemName` を使用してコンテキストを識別します。|  
|`pstrDelimiter`|[入力] スクリプトレット末尾の区切り記号のアドレス。 `pstrCode` がテキストのストリームから解析されるとき、ホストは通常、2 つの単一引用符 ('') などの区切り文字を使用してスクリプトレットの末尾を検出します。 このパラメーターには、ホストが使用する区切り文字を指定します。それにより、スクリプト エンジンで何らかの条件付きのプリミティブな前処理が可能になります (単一引用符 (') を区切り文字として使用するために 2 つの単一引用符に置き換えるなど)。 スクリプト エンジンがこの情報を厳密にどのような方法 (条件) で使用するかは、スクリプト エンジンによって異なります。 ホストがスクリプトレットの末尾を示す区切り文字を使用しない場合は、このパラメーターを `NULL` に設定します。|  
|`dwSourceContextCookie`|[入力] デバッグ目的で使用されるクッキー。|  
|`ulStartingLineNumber`|[入力] 解析が開始される行を指定するゼロから始まる値。|  
|`dwFlags`|[入力] スクリプトレットに関連付けられるフラグ。 次の値の組み合わせが可能です。|  
  
|[値]|説明|  
|-----------|-------------|  
|SCRIPTTEXT_ISEXPRESSION|計算式とステートメントの区別は重要ですが、スクリプト言語で文法的にあいまいな場合、このフラグは、スクリプトレットがステートメント (またはステートメントの列挙) としてではなく式として解釈されることを指定します。 どちらであるかスクリプトレット テキストの構文から正しく判断できない場合、既定ではステートメントとして解釈されます。|  
|SCRIPTTEXT_ISPERSISTENT|スクリプト エンジンが保存される場合 (`IPersist*::Save` の呼び出しなどにより)、または初期化状態に戻すことでリセットされる場合、この呼び出し中に追加されたコードを保存する必要があることを指定します。|  
|SCRIPTTEXT_ISVISIBLE|スクリプト テキストをスクリプトの名前空間内でグローバル メソッドとして参照可能にする (名前で呼び出せるようにする) 必要があることを指定します。|  
  
|||  
|-|-|  
|`pvarResult`|[出力] 呼び出し元に結果を返す必要がない (SCRIPTTEXT_ISEXPRESSION 値が設定されていない) 場合に、スクリプトレットの処理結果または `NULL` を受け取るバッファーのアドレス。|  
|`pexcepinfo`|[出力] 例外情報を受け取る構造体のアドレス。 `IActiveScriptParse::ParseScriptText` が DISP_E_EXCEPTION を返す場合、この構造体に情報が格納されます。|  
  
## <a name="return-value"></a>戻り値  
 次のいずれかの値を返します。  
  
|戻り値|説明|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`DISP_E_EXCEPTION`|スクリプトレットの処理中に例外が発生しました。 `pexcepinfo` パラメーターに例外に関する情報が格納されます。|  
|`E_INVALIDARG`|引数が無効です。|  
|`E_POINTER`|無効なポインターが指定されました。|  
|`E_NOTIMPL`|このメソッドはサポートされていません。 スクリプト エンジンが式やステートメントの実行時の評価をサポートしていません。|  
|`E_UNEXPECTED`|呼び出しは不要でした (スクリプト エンジンが未初期化または終了状態である場合や、SCRIPTTEXT_ISEXPRESSION フラグが設定されていてスクリプト エンジンが初期化状態である場合など)。|  
|`OLESCRIPT_E_SYNTAX`|指定されていない構文エラーがスクリプトレットで発生しました。|  
  
## <a name="remarks"></a>Remarks  
 スクリプト エンジンが初期化状態である場合、コードは実際にはこの呼び出し中に評価されません。コードはキューに入れられ、スクリプト エンジンが起動状態に移行 (を経過) すると実行されます。 コードの実行が初期化状態では許可されないため、初期化状態のときに SCRIPTTEXT_ISEXPRESSION フラグを設定してこのメソッドを呼び出すと、エラーになります。  
  
 スクリプトレットは、スクリプト言語で許可されている限り、式でもステートメントの列挙でも、その他のものでもかまいません。 HTML の評価でこのメソッドを使用するなど、\<スクリプト > タグが実行されるだけにスクリプトの状態へのコンパイルではなく、HTML ページが構築されるようにステートメントを許可します。  
  
 このメソッドに渡されるコードは、コードとして有効であり完結している必要があります。 たとえば VBScript では、このメソッドを Sub Function(x) で 1 回呼び出し、`End Sub` でもう 1 回呼び出すことは無効です。 パーサーは、このメソッドの 2 回目の呼び出しがあるため、サブルーチンの完了を待たずに、解析エラーを生成します。サブルーチンの宣言が開始したが完了しなかったためです。  
  
 スクリプトの状態の詳細については、のスクリプト エンジンの状態を参照してください[Windows スクリプト エンジン](../../winscript/windows-script-engines.md)します。  
  
## <a name="see-also"></a>関連項目  
 [IActiveScriptParse](../../winscript/reference/iactivescriptparse.md)