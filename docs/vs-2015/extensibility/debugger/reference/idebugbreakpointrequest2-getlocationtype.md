---
title: IDebugBreakpointRequest2::GetLocationType |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest2::GetLocationType
helpviewer_keywords:
- IDebugBreakpointRequest2::GetLocationType
ms.assetid: b6d14c59-d3aa-48ff-8278-f6b5bba9c2f3
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ef335232b20fbc74c323fe96ab283280e9d2aad6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62431512"
---
# <a name="idebugbreakpointrequest2getlocationtype"></a>IDebugBreakpointRequest2::GetLocationType
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このブレークポイント要求のブレークポイントの場所の種類を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetLocationType(   
   BP_LOCATION_TYPE* pBPLocationType  
);  
```  
  
```csharp  
int GetLocationType(   
   out enum_BP_LOCATION_TYPE pBPLocationType  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pBPLocationType`  
 [out]値を返します、 [BP_LOCATION_TYPE](../../../extensibility/debugger/reference/bp-location-type.md)このブレークポイント要求の場所を表す列挙体。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。 返します`E_FAIL`場合、`bpLocation`フィールドに関連付けられている[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)構造が無効です。  
  
## <a name="example"></a>例  
 次の例は、単純なは、このメソッドを実装する方法を示しています。`CDebugBreakpointRequest`を公開するオブジェクト、[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)インターフェイス。  
  
```  
HRESULT CDebugBreakpointRequest::GetLocationType(BP_LOCATION_TYPE* pBPLocationType)    
{    
   HRESULT hr;    
  
   if (pBPLocationType)    
   {    
      // Set default BP_LOCATION_TYPE.    
      *pBPLocationType = BPLT_NONE;    
  
      // Check if the BPREQI_BPLOCATION flag is set in BPREQI_FIELDS.    
      if (IsFlagSet(m_bpRequestInfo.dwFields, BPREQI_BPLOCATION))    
      {    
         // Get the new BP_LOCATION_TYPE.    
         *pBPLocationType = m_bpRequestInfo.bpLocation.bpLocationType;    
         hr = S_OK;    
      }    
      else    
      {    
         hr = E_FAIL;    
      }    
   }    
   else    
   {    
      hr = E_INVALIDARG;    
   }    
  
   return hr;    
}    
```  
  
## <a name="see-also"></a>関連項目  
 [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)   
 [BP_LOCATION_TYPE](../../../extensibility/debugger/reference/bp-location-type.md)   
 [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)   
 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
