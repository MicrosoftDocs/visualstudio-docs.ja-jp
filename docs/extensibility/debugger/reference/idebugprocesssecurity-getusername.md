---
title: IDebugProcessSecurity::GetUserName | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- IDebugProcessSecurity::GetUserName
ms.assetid: c73c60ac-da6e-45ae-8f04-95353a24ca3e
caps.latest.revision: 4
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
ms.sourcegitcommit: 4a36302d80f4bc397128e3838c9abf858a0b5fe8
ms.openlocfilehash: 081f073ba59021ca56dd084bd2cef0fde6c5c32e
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="idebugprocesssecuritygetusername"></a>IDebugProcessSecurity::GetUserName
Gets the user name from the port supplier.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT GetUserName(  
    BSTR *pbstrUserName  
);  
```  
  
```csharp  
int GetUserName (  
    string pbstrUserName  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pbstrUserName`  
 [out] A string containing the user name.  
  
## <a name="return-value"></a>Return Value  
 If the method succeeds, it returns `S_OK`. Otherwise it returns an error code.  
  
## <a name="remarks"></a>Remarks  
 `GetUserName` returns the user name that is displayed in the **User Name** column of the **Attach to Process** dialog box. To view the **Attach to Process** dialog box, click **Attach to Process** on the **Tools** menu in the [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] integrated development environment (IDE).  
  
## <a name="see-also"></a>See Also  
 [IDebugProcessSecurity](../../../extensibility/debugger/reference/idebugprocesssecurity.md)
