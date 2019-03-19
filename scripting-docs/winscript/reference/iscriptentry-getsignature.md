---
title: IScriptEntry::GetSignature |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptEntry.GetSignature
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptEntry::GetSignature
ms.assetid: 8cbf37ac-b14c-4e15-a613-06f34857da9b
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 70cc1939ae4eb1e3c58d31b3d42b7f1b4603ce9e
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58145305"
---
# <a name="iscriptentrygetsignature"></a>IScriptEntry::GetSignature
型の情報を返します、`IScriptEntry`関数オブジェクト。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetSignature(  
   ITypeInfo          **ppti  
   ULONG              *piMethod  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppti`  
 [out]これに関連付けられている情報を入力`IScriptEntry`関数オブジェクト。  
  
 `piMethod`  
 [out]メソッドのインデックスで、`ITypeInfo`オブジェクト。  
  
## <a name="return-value"></a>戻り値  
 `HRESULT`。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|[値]|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>Remarks  
 使用して型情報を設定する[IScriptEntry::SetSignature](../../winscript/reference/iscriptentry-setsignature.md)または[IScriptNode::CreateChildHandler](../../winscript/reference/iscriptnode-createchildhandler.md)します。 関数の内部表現に基づくエントリによって、型情報を生成こともできます。  
  
## <a name="see-also"></a>関連項目  
 [IScriptEntry インターフェイス](../../winscript/reference/iscriptentry-interface.md)