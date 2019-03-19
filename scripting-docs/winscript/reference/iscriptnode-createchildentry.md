---
title: IScriptNode:。:Createchildentry |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptNode. CreateChildEntry
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptNode::CreateChildEntry
ms.assetid: b9682505-4457-40e9-8691-235843637506
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 75369df719b0cd140ce621e916215eb18cf30a9e
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58156659"
---
# <a name="iscriptnode-createchildentry"></a>IScriptNode:。:Createchildentry
子インスタンスを追加します。`IScriptEntry`します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT CreateChildEntry(  
   ULONG              isn,  
   DWORD              dwCookie,  
   LPCOLESTR          pszDelimiter,  
   IScriptEntry       **ppse  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `isn`  
 [in]親の子のインデックス。  
  
 `dwCookie`  
 [in]ホスト オブジェクトに子エントリを関連付けるために使用するアプリケーション定義の値。  
  
 `pszDelimiter`  
 [in]最後のスクリプト ブロックの区切り記号のアドレス。 解析、ホストは通常、スクリプト ブロックの終了を検出する (2 つ単一引用符) などの区切り記号を使用します。  
  
 区切り記号は、前処理を提供するエンジンを作成するスクリプトをできます。 など、エンジンは、区切り記号として使用するための 2 つの単一引用符で単一引用符を置き換えることが。 エンジンは、区切り記号を使用する方法を決定します。  
  
 区切り記号がスクリプト ブロックの末尾をマークしない場合は NULL に設定します。  
  
 `ppse`  
 [out]ポインターを受け取る変数のアドレス、`IScriptEntry`子インスタンスのインターフェイス。  
  
 `IScriptNode`このパラメーターは、Web ページを表すオブジェクトを返します、`IScriptEntry`インスタンスが、スクリプト ブロックを指定します。  
  
 `IScriptEntry`スクリプト ブロックを表すオブジェクトの場合は、このパラメーターを返します、`IScriptEntry`インスタンスが関数オブジェクトを指定します。  
  
 `IScriptEntry`関数を表すオブジェクトのオブジェクトをこのメソッドは失敗します。  
  
 `IScriptScriptlet`オブジェクトの場合、このメソッドは失敗します。  
  
## <a name="return-value"></a>戻り値  
 `HRESULT`。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|[値]|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>Remarks  
 `IScriptNode`インターフェイスは、Web ページまたはその要素を表します。 `IScriptEntry`インターフェイス (から派生`IScriptNode`) は、スクリプト ブロックまたは関数オブジェクトを表します。 `IScriptScriptlet`インターフェイス (から派生`IScriptEntry`) イベント ハンドラーを表します。  
  
## <a name="see-also"></a>関連項目  
 [IScriptNode インターフェイス](../../winscript/reference/iscriptnode-interface.md)   
 [IScriptEntry インターフェイス](../../winscript/reference/iscriptentry-interface.md)