---
title: IDebugBreakpointUnboundEvent2::GetReason |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBreakpointUnboundEvent2::GetReason
helpviewer_keywords:
- IDebugBreakpointUnboundEvent2::GetReason
ms.assetid: 0f8a4fec-d3eb-417d-8516-4f7b51904033
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6633fa2b3950d49a3db3b286157d50c026261300
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68160035"
---
# <a name="idebugbreakpointunboundevent2getreason"></a>IDebugBreakpointUnboundEvent2::GetReason
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ブレークポイントがバインドされた理由を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetReason(   
   BP_UNBOUND_REASON* pdwUnboundReason  
);  
```  
  
```csharp  
int GetReason(   
   out enum_ BP_UNBOUND_REASON pdwUnboundReason  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pdwUnboundReason`  
 [out]値を返します、 [BP_UNBOUND_REASON](../../../extensibility/debugger/reference/bp-unbound-reason.md)ブレークポイントがバインドされた理由を指定する列挙体。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="remarks"></a>Remarks  
 上の理由からには、エディット コンティニュの操作の場合、またはエラーでブレークポイントがバインドされている決定した後、別の場所に再バインドされているブレークポイントが含まれます。  
  
## <a name="example"></a>例  
 次の例では、このメソッドを実装する方法を示しています、 **CBreakpointUnboundDebugEventBase**を公開するオブジェクト、 [IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)インターフェイス。  
  
```cpp#  
STDMETHODIMP CBreakpointUnboundDebugEventBase::GetReason(  
    BP_UNBOUND_REASON* pdwUnboundReason)  
{  
    HRESULT hRes = E_FAIL;  
  
    if ( EVAL(pdwUnboundReason) )  
    {  
        *pdwUnboundReason = m_dwReason;  
  
        hRes = S_OK;  
    }  
    else  
        hRes = E_INVALIDARG;  
  
    return ( hRes );  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)
