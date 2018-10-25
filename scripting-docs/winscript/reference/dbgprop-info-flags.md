---
title: DBGPROP_INFO_FLAGS |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DBGPROP_INFO_FLAGS
apilocation:
- scrobj.dll
f1_keywords:
- DBGPROP_INFO_FLAGS
helpviewer_keywords:
- DBGPROP_INFO_FLAGS
ms.assetid: e9450a21-a802-4c3e-8b3d-8e202f555de1
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 377815adc7751841e2a2a3bb2f4dc8b51beecdea
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49941283"
---
# <a name="dbgpropinfoflags"></a>DBGPROP_INFO_FLAGS
指定するために使用`DebugPropertyInfo`フィールド  
  
## <a name="syntax"></a>構文  
  
```  
enum {  
   DBGPROP_INFO_NAME  =0x001,  
   DBGPROP_INFO_TYPE  =0x002,  
   DBGPROP_INFO_VALUE  =0x004,  
   DBGPROP_INFO_FULLNAME  =0x020,  
   DBGPROP_INFO_ATTRIBUTES  =0x008,  
   DBGPROP_INFO_DEBUGPROP  =0x010,  
   DBGPROP_INFO_AUTOEXPAND  =0x8000000  
};  
```  
  
## <a name="members"></a>メンバー  
 DBGPROP_INFO_NAME  
 初期化します、`bstrName`フィールド。  
  
 DBGPROP_INFO_TYPE  
 初期化します、`bstrType`フィールド。  
  
 DBGPROP_INFO_VALUE  
 初期化します、`bstrValue`フィールド。  
  
 DBGPROP_INFO_FULLNAME  
 初期化します、`bstrFullName`フィールド。  
  
 DBGPROP_INFO_ATTRIBUTES  
 初期化します、`dwAttrib`フィールド。  
  
 DBGPROP_INFO_DEBUGPROP  
 初期化します、`pDebugProp`フィールドを含む、`IDebugProperty`インターフェイス。  
  
 DBGPROP_INFO_AUTOEXPAND  
 [値] フィールドは、この種類のオブジェクトの使用可能な場合は、自動拡張値を含める必要がありますを指定します。  
  
## <a name="see-also"></a>関連項目  
 [DebugPropertyInfo 構造体](../../winscript/reference/debugpropertyinfo-structure.md)   
 [IDebugProperty インターフェイス](../../winscript/reference/idebugproperty-interface.md)