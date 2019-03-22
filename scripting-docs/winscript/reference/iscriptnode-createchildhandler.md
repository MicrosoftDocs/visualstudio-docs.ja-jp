---
title: IScriptNode::CreateChildHandler |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptNode.CreateChildHandler
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptNode::CreateChildHandler
ms.assetid: 4ce5eb10-1a3f-43b0-a4b7-599a397ed3a2
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: bca8b30021d39638f3755bace2625bb38a44242d
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58149248"
---
# <a name="iscriptnodecreatechildhandler"></a>IScriptNode::CreateChildHandler
子インスタンスとしてスクリプトレットを追加、`IScriptNode`します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT CreateChildHandler(  
   LPCOLESTR          pszDefaultName,  
   LPCOLESTR          *prgpszNames,  
   ULONG              cpszNames,  
   LPCOLESTR          pszEvent,  
   LPCOLESTR          pszDelimiter,  
   ITypeInfo*         ptiSignature,  
   ULONG              iMethodSignature,  
   ULONG              isn,  
   DWORD              dwCookie,  
   IScriptEntry       **ppse  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pszDefaultName`  
 [in]スクリプトレットに関連付ける既定の名前のアドレス。  
  
 `prgpszNames`  
 [size_is で (`cpszNames`)]、ホスト上の完全修飾名から識別子の一覧。  
  
 `cpszNames`  
 [in]識別子の数、`prgpszNames`パラメーター。  
  
 `pszEvent`  
 [in]スクリプトレットに関連付けられているイベントの名前を識別するバッファーのアドレス。  
  
 `pszDelimiter`  
 [in]最後のスクリプト ブロックの区切り記号のアドレス。 解析、ホストは通常、スクリプト ブロックの終了を検出する (2 つ単一引用符) などの区切り記号を使用します。  
  
 区切り記号は、スクリプト エンジンを作成して前処理を使用できます。 など、エンジンは、区切り記号として使用するための 2 つの単一引用符で単一引用符を置き換えることが。 エンジンは、区切り記号を使用する方法を決定します。  
  
 スクリプト ブロックの末尾を識別する区切り記号を使用しない場合は NULL に設定します。  
  
 `ptiSignature`  
 [in]関数オブジェクトの型情報。  
  
 `iMethodSignature`  
 [in]内の関数のインデックス、`ITypeInfo``ptiSignature`パラメーター。  
  
 `isn`  
 [in]親の子のインデックス。  
  
 `dwCookie`  
 [in]エントリをそのホスト オブジェクトに関連付けるために使用するアプリケーション定義の値。  
  
 `ppse`  
 [out]ポインターを受け取る変数のアドレス、`IScriptEntry`子インスタンスのインターフェイス。  
  
## <a name="return-value"></a>戻り値  
 `HRESULT`。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|[値]|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>Remarks  
 スクリプトレットは、イベント ハンドラーを指定します。 呼び出された場合、このメソッドがスクリプトレットを作成、 `IScriptNode` Web ページを表すオブジェクト。 このメソッドは、他のインターフェイスによって呼び出された場合に成功しません。  
  
## <a name="see-also"></a>関連項目  
 [IScriptNode インターフェイス](../../winscript/reference/iscriptnode-interface.md)   
 [IScriptEntry インターフェイス](../../winscript/reference/iscriptentry-interface.md)