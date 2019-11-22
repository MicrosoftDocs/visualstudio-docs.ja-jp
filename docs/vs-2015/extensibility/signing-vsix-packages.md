---
title: Signing VSIX Packages | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- signature
- signing
- authenticode
- vsix
- packages
ms.assetid: e34cfc2c-361c-44f8-9cfe-9f2be229d248
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b74222804e9ed42e6f8263cbe6ad0daf19cda81f
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300325"
---
# <a name="signing-vsix-packages"></a>VSIX パッケージの署名
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Extension assemblies do not need to be signed before they can run in Visual Studio, but it is a good practice to do so.  
  
 If you want to secure your extension and make sure it hasn’t been tampered with, you can add a digital signature to a VSIX package. When a VSIX is signed, the VSIX installer will display a message indicating that it is signed, plus more information about the signature itself. If the contents of the VSIX have been modified, and the VSIX has not been signed again, the VSIX installer will show that the signature is not valid. The installation is not stopped, but the user is warned.  
  
> [!IMPORTANT]
> Beginning in 2015, VSIX packages signed using anything other than SHA256 encryption will be identified as having an invalid signature. VSIX installation is not blocked but the user will be warned.  
  
## <a name="signing-a-vsix-with-vsixsigntool"></a>Signing a VSIX with VSIXSignTool  
 There is a SHA256 encryption signing tool available from [VisualStudioExtensibility](https://www.nuget.org/profiles/VisualStudioExtensibility) on nuget.org at [VsixSignTool](https://www.nuget.org/packages/Microsoft.VSSDK.Vsixsigntool).  
  
#### <a name="to-use-the-vsixsigntool"></a>To use the VSIXSignTool  
  
1. Add your VSIX to a project.  
  
2. Right click on the project node in Solution Explorer, selecting **Add &#124; Manage NuGet Packages**.  For more information on NuGet and adding NuGet packages see [NuGet Overview](https://docs.microsoft.com/nuget/) and [Manage NuGet Packages Using the Dialog](https://docs.microsoft.com/nuget/consume-packages/install-use-packages-visual-studio).  
  
3. Search for VSIXSignTool from VisualStudioExtensibility and install the NuGet package.  
  
4. You can now run the VSIXSignTool from the project’s local packages location. Consult the tool’s command line help for your signing scenario (VSIXSignTool.exe /?).  
  
   For example to sign with a password protected certificate file:  
  
   VSIXSignTool.exe sign /f \<certfile> /p \<password> \<VSIXfile>  
  
## <a name="see-also"></a>参照  
 [Visual Studio 拡張機能の配布](../extensibility/shipping-visual-studio-extensions.md)
