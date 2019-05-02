---
title: IDispatchEx::DeleteMemberByName |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.DeleteMemberByName
apilocation:
- scrobj.dll
helpviewer_keywords:
- DeleteMemberByName method
ms.assetid: a01b4e6a-d989-4b29-bb3f-04554f8c39f7
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: dc7c8db4ab28e0bd0fcb48f352cb07595f72fd17
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63000890"
---
# <a name="idispatchexdeletememberbyname"></a>IDispatchEx::DeleteMemberByName
名前では、メンバーを削除します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT DeleteMemberByName(  
   BSTR bstrName,  
   DWORD grfdex  
  
```  
  
#### <a name="parameters"></a>パラメーター  
 `bstrName`  
 削除するメンバーの名前です。  
  
 `grfdex`  
 かどうか、メンバー名は大文字と小文字を決定します。 次の値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-------------|  
|fdexNameCaseSensitive|名前参照は、大文字と小文字で実行するように要求します。 大文字のルックアップをサポートしていないオブジェクトでは無視できます。|  
|fdexNameCaseInsensitive|名前参照で大文字と小文字を行うように要求します。 大文字のルックアップをサポートしていないオブジェクトでは無視できます。|  
  
## <a name="return-value"></a>戻り値  
 次のいずれかの値を返します。  
  
|||  
|-|-|  
|`S_OK`|成功。|  
|`S_FALSE`|メンバーが存在しますが、削除できません。|  
  
## <a name="remarks"></a>Remarks  
 DISPID が有効でする必要がある場合は、メンバーを削除すると、`GetNextDispID`します。  
  
 指定された名前を持つメンバーが削除され、後で同じ名前のメンバーが再作成された場合、DISPID は同じである必要があります。 (大文字と小文字が異なるだけのメンバーは、「同じ」かどうかはオブジェクトに依存) です。  
  
## <a name="example"></a>例  
  
```cpp
BSTR bstrName;  
IDispatchEx *pdex;  
  
// Assign to pdex and bstrName  
pdex->DeleteMemberByName(bstrName, fdexNameCaseSensitive);  
```  
  
## <a name="see-also"></a>関連項目  
 [IDispatchEx インターフェイス](../../winscript/reference/idispatchex-interface.md)