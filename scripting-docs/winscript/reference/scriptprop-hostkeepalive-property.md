---
title: SCRIPTPROP_HOSTKEEPALIVE プロパティ |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: bfa199f2-28ba-4320-bc0f-2320fad018bd
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3724bfcb1ec42617cda4c89269cb0160accafb1a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62840342"
---
# <a name="scriptprophostkeepalive-property"></a>SCRIPTPROP_HOSTKEEPALIVE プロパティ
スクリプト エンジンを未解決の参照がある場合は、完全に機能保持するかどうかを指定するために使用します。  
  
 使用[IActiveScriptProperty::SetProperty](../../winscript/reference/iactivescriptproperty-setproperty.md)にこのプロパティを設定する`true`します。 このプロパティ設定されている場合`true`、スクリプト エンジン自体をまたはに少なくとも 1 つの未解決の参照がある限り、スクリプト エンジンが完全に機能を保持、`IDispatch`スクリプトを使用して作成された JavaScript オブジェクトへのポインターエンジン。 このプロパティに設定しているときに`true`、明示的に閉じるかを使用して、スクリプト エンジンをリセットする必要があります、 [IActiveScript::Close](../../winscript/reference/iactivescript-close.md)または[iactivescript::setscriptstate](../../winscript/reference/iactivescript-setscriptstate.md)メソッド。 オブジェクトのスクリプトへの参照を過去のリリースでは、スクリプト エンジンをシャット ダウンします。  
  
## <a name="syntax"></a>構文  
  
```cpp
#define SCRIPTPROP_HOSTKEEPALIVE 0x70000004  
```  
  
## <a name="requirements"></a>必要条件  
 Activscp.idl と共にインストールされているのバージョンでのみこのプロパティが表示されます[!INCLUDE[win8](../../javascript/includes/win8-md.md)]、上の Internet Explorer 8 のサポート技術情報 2707082 で[!INCLUDE[win7](../../winscript/reference/includes/win7-md.md)]、または Internet Explorer 9 の KB 2722913[!INCLUDE[win7](../../winscript/reference/includes/win7-md.md)]または[!INCLUDE[vista_first](../../winscript/reference/includes/vista-first-md.md)]。