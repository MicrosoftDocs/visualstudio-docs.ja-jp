---
title: Neutral Resources Languages for Localization | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- localization [Visual Studio], resources
- NeutralResourcesLanguageAttribute class
- globalization [Visual Studio], resources
- resources [Visual Studio], fallback system
- culture, locating resources
- neutral resources
ms.assetid: ef064995-3b84-4698-a708-9689b7723533
caps.latest.revision: 8
author: kempb
ms.author: kempb
manager: ghogen
translation.priority.ht:
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
ms.translationtype: HT
ms.sourcegitcommit: ff8ecec19f8cab04ac2190f9a4a995766f1750bf
ms.openlocfilehash: cc31ee5c559478e5c1faefc485e02f022f98caa5
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="neutral-resources-languages-for-localization"></a>Neutral Resources Languages for Localization
The <xref:System.Resources.NeutralResourcesLanguageAttribute> class specifies the culture of the resources included in the main assembly. This attribute is used as a performance enhancement, so that the <xref:System.Resources.ResourceManager> object does not search for resources that are included in the main assembly.  
  
 The following code shows how to set the neutral resources language. The code can be placed in either a build script or in the AssemblyInfo.vb or AssemblyInfo.cs file.  
  
```vb  
' Set neutral resources language for assembly.  
<Assembly: NeutralResourcesLanguageAttribute("en")>  
  
```  
  
```cs  
// Set neutral resources language for assembly.  
[assembly: NeutralResourcesLanguageAttribute("en")]  
```  
  
## <a name="see-also"></a>See Also  
 <xref:System.Resources.ResourceManager>   
 [Introduction to International Applications Based on the .NET Framework](../ide/introduction-to-international-applications-based-on-the-dotnet-framework.md)   
 [Hierarchical Organization of Resources for Localization](../ide/hierarchical-organization-of-resources-for-localization.md)   
 [Localizing Applications](../ide/localizing-applications.md)   
 [Globalizing and Localizing Applications](../ide/globalizing-and-localizing-applications.md)
