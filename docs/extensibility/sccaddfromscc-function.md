---
title: SccAddFromScc Function | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SccAddFromScc
helpviewer_keywords:
- SccAddFromScc function
ms.assetid: 902e764d-200e-46e1-8c42-4da7b037f9a0
caps.latest.revision: 17
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
ms.openlocfilehash: 4711028976d9a55e4281cb2ba3e8b0dd27aa1417
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="sccaddfromscc-function"></a>SccAddFromScc Function
This function allows the user to browse for files that are already in the source control system and subsequently make those files part of the current project. For example, this function can get a common header file into the current project without copying the file. The return array of files, `lplpFileNames`, contains the list of files that the user wants to add to the IDE project.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
SCCRTN SccAddFromScc (  
   LPVOID   pvContext,  
   HWND     hWnd,  
   LPLONG   lpnFiles,  
   LPCSTR** lplpFileNames  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 pvContext  
 [in] The source control plug-in context structure.  
  
 hWnd  
 [in] A handle to the IDE window that the source control plug-in can use as a parent for any dialog boxes that it provides.  
  
 lpnFiles  
 [in, out] A buffer for the number of files that are being added in. (This is `NULL` if the memory pointed to by `lplpFileNames` is to be released. See Remarks for details.)  
  
 lplpFileNames  
 [in, out] An array of pointers to all the file names without directory paths. This array is allocated and freed by the source control plug-in. If `lpnFiles` = 1 and `lplpFileNames` is not `NULL`, the first name in the array pointed to by `lplpFileNames` contains the destination folder.  
  
## <a name="return-value"></a>Return Value  
 The source control plug-in implementation of this function is expected to return one of the following values:  
  
|Value|Description|  
|-----------|-----------------|  
|SCC_OK|The files were successfully located and added to the project.|  
|SCC_I_OPERATIONCANCELED|Operation was canceled with no effect.|  
|SCC_I_RELOADFILE|A file or project needs to be reloaded.|  
  
## <a name="remarks"></a>Remarks  
 The IDE calls this function. If the source control plug-in supports specifying a local destination folder, the IDE passes `lpnFiles` = 1 and passes the local folder name into `lplpFileNames`.  
  
 When the call to the `SccAddFromScc` function returns, the plug-in has assigned values to `lpnFiles` and `lplpFileNames`, allocating the memory for the file name array as necessary (note that this allocation replaces the pointer in `lplpFileNames`). The source control plug-in is responsible for placing all files into the user's directory or in the specified designation folder. The IDE then adds the files to the IDE project.  
  
 Finally, the IDE calls this function a second time, passing in `NULL` for `lpnFiles`. This is interpreted as a special signal by the source control plug-in to release the memory allocated for the file-name array in `lplpFileNames``.`  
  
 `lplpFileNames` is a `char ***` pointer. The source control plug-in places a pointer to an array of pointers to file names, thus passing the list in the standard way for this API.  
  
> [!NOTE]
>  Initial versions of the VSSCI API did not provide a way to indicate the target project for the added files. To accommodate this, the semantics of the `lplpFIleNames` parameter have been enhanced to make it an in/out parameter rather than an output parameter. If only a single file is specified, that is, the value pointed to by `lpnFiles` = 1, then the first element of `lplpFileNames` contains the target folder. To use these new semantics, the IDE calls the `SccSetOption` function with the `nOption`parameter set to `SCC_OPT_SHARESUBPROJ`. If a source control plug-in does not support the semantics, it returns `SCC_E_OPTNOTSUPPORTED`. Doing so disables the use of the **Add from Source Control** feature. If a plug-in supports the **Add from Source Control** feature (`SCC_CAP_ADDFROMSCC`), then it must support the new semantics and return `SCC_I_SHARESUBPROJOK`.  
  
## <a name="see-also"></a>See Also  
 [Source Control Plug-in API Functions](../extensibility/source-control-plug-in-api-functions.md)   
 [SccSetOption](../extensibility/sccsetoption-function.md)
