---
title: IDebugClassField::GetDefaultIndexer | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugClassField::GetDefaultIndexer
helpviewer_keywords:
- IDebugClassField::GetDefaultIndexer method
ms.assetid: 47ce4f45-3816-4b40-909c-5032d0692d75
caps.latest.revision: 10
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
ms.openlocfilehash: 7fe0008e38175254d9ac0eb4146d31d9866d9c69
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="idebugclassfieldgetdefaultindexer"></a>IDebugClassField::GetDefaultIndexer
Gets the name of the default indexer.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT GetDefaultIndexer(   
   BSTR* pbstrIndexer  
);  
```  
  
```csharp  
int GetDefaultIndexer(  
   out string pbstrIndexer  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pbstrIndexer`  
 [out] Returns a string containing the name of the default indexer.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns S_OK or returns S_FALSE if there is no default indexer. Otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 The default indexer of a class is the property that is marked as the `Default` property for array accesses. This is specific to [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)]. Here is an example of a default indexer declared in [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] and how it is used.  
  
```vb  
Imports System.Collections;  
  
Public Class Class1  
    Private myList as Hashtable  
  
    Default Public Property Item(ByVal Index As Integer) As Integer  
        Get  
            Return CType(List(Index), Integer)  
        End Get  
        Set(ByVal Value As Integer)  
            List(Index) = Value  
        End Set  
    End Property  
End Class  
  
Function GetItem(Index as Integer) as Integer  
    Dim classList as Class1 = new Class1  
    Dim value as Integer  
  
    ' Access array through default indexer  
    value = classList(2)  
  
    ' Access array through explicit property  
    value = classList.Item(2)  
  
    Return value  
End Function  
```  
  
## <a name="see-also"></a>See Also  
 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
