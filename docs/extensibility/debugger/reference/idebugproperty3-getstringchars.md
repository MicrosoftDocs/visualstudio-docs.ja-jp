---
title: IDebugProperty3::GetStringChars | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugProperty3::GetStringChars
helpviewer_keywords:
- IDebugProperty3::GetStringChars
ms.assetid: 832c37f3-85cb-4227-8ab2-f27a80eafe90
caps.latest.revision: 7
ms.author: gregvanl
manager: ghogen
translation.priority.mt:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: MT
ms.sourcegitcommit: ff8ecec19f8cab04ac2190f9a4a995766f1750bf
ms.openlocfilehash: d7c706c5f9b7b3e21bae4e5af1d2314f6db95734
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="idebugproperty3getstringchars"></a>IDebugProperty3::GetStringChars
Retrieves the string associated with this property and stores it in a user-supplied buffer.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT GetStringChars(  
   ULONG  buflen,  
   WCHAR* rgString,  
   ULONG* pceltFetched  
);  
```  
  
```cs  
int GetStringChars(  
   uint       buflen,   
   out string rgString,   
   out uint   pceltFetched  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `buflen`  
 [in] Maximum number of characters the user-supplied buffer can hold.  
  
 `rgString`  
 [out] Returns the string.  
  
 [C++ only], `rgString` is a pointer to a buffer that receives the Unicode characters of the string. This buffer must be at least `buflen` characters (not bytes) in size.  
  
 `pceltFetched`  
 [out] Where the number of characters actually stored in the buffer is returned. (Can be `NULL` in C++.)  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise returns an error code.  
  
## <a name="remarks"></a>Remarks  
 In C++, care must be taken to insure that the buffer is at least `buflen` Unicode characters long. Note that a Unicode character is 2 bytes long.  
  
> [!NOTE]
>  In C++, the returned string does not include a terminating null character. If given, `pceltFetched` will specify the number of characters in the string.  
  
## <a name="example"></a>Example  
 
```cpp  
CStringW RetrievePropertyString(IDebugProperty2 *pPropInfo)  
{  
    CStringW returnString = L"";  
    CComQIPtr<IDebugProperty3> pProp3 = pPropInfo->pProperty;  
    If (pProp3 != NULL) {  
        ULONG dwStrLen = 0;  
        HRESULT hr;  
        hr = pProp3->GetStringCharLength(&dwStrLen);  
        if (SUCCEEDED(hr) && dwStrLen > 0) {  
            ULONG dwRead;  
            CStrBufW buf(returnString,dwStrLen,CStrBuf::SET_LENGTH);  
            hr = pProp3->GetStringChars(dwStrLen,  
                                        reinterpret_cast<WCHAR*>(static_cast<CStringW::PXSTR>(buf)),  
                                        &dwRead);  
        }  
    }  
    return(returnString);
}
```    
  
## <a name="see-also"></a>See Also  
 [GetStringCharLength](../../../extensibility/debugger/reference/idebugproperty3-getstringcharlength.md)   
 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)   
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
