---
title: SccQueryInfo Function | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SccQueryInfo
helpviewer_keywords:
- SccQueryInfo function
ms.assetid: 3973d336-a9b7-41a2-a4e6-bb8184a96aaf
caps.latest.revision: 18
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
ms.openlocfilehash: 4efd9b29a89bc490255c35558e5862ebc14b7fec
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="sccqueryinfo-function"></a>SccQueryInfo Function
This function obtains status information for a set of selected files under source control.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
SCCRTN SccQueryInfo(  
   LPVOID  pvContext,  
   LONG    nFiles,  
   LPCSTR* lpFileNames,  
   LPLONG  lpStatus  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 pvContext  
 [in] The source control plug-in context structure.  
  
 nFiles  
 [in] Number of files specified in the `lpFileNames` array and the length of the `lpStatus` array.  
  
 lpFileNames  
 [in] An array of names of files to be queried.  
  
 lpStatus  
 [in, out] An array in which the source control plug-in returns the status flags for each file. For more information, see [File Status Code](../extensibility/file-status-code-enumerator.md).  
  
## <a name="return-value"></a>Return Value  
 The source control plug-in implementation of this function is expected to return one of the following values:  
  
|Value|Description|  
|-----------|-----------------|  
|SCC_OK|Query was successful.|  
|SCC_E_ACCESSFAILURE|There was a problem with accessing the source control system, probably caused by network or contention issues. A retry is recommended.|  
|SCC_E_PROJNOTOPEN|The project is not open under source control.|  
|SCC_E_NONSPECIFICERROR|Nonspecific failure.|  
  
## <a name="remarks"></a>Remarks  
 If `lpFileName` is an empty string, there is currently no status information to update. Otherwise, it is the full path name of the file for which the status information may have changed.  
  
 The return array can be a bitmask of `SCC_STATUS_xxxx` bits. For more information, see [File Status Code](../extensibility/file-status-code-enumerator.md). A source control system may not support all bit types. For example, if `SCC_STATUS_OUTOFDATE` is not offered, the bit is just not set.  
  
 When using this function to check out files, note the following `MSSCCI` status requirements:  
  
-   `SCC_STATUS_OUTBYUSER` is set when the current user has checked out the file.  
  
-   `SCC_STATUS_CHECKEDOUT` cannot be set unless `SCC_STATUS_OUTBYUSER` is set.  
  
-   `SCC_STATUS_CHECKEDOUT` is only set when the file is checked-out into the designated working directory.  
  
-   If the file is checked-out by the current user into a directory other than the working directory, `SCC_STATUS_OUTBYUSER` is set but `SCC_STATUS_CHECKEDOUT` is not.  
  
## <a name="see-also"></a>See Also  
 [Source Control Plug-in API Functions](../extensibility/source-control-plug-in-api-functions.md)   
 [File Status Code](../extensibility/file-status-code-enumerator.md)
