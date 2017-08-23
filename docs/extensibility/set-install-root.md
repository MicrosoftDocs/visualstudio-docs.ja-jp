---
title: Installing outside the extensions folder with VSIX v3 | Microsoft Docs
ms.custom: 
ms.date: 11/09/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 913c3745-8aa9-4260-886e-a05aecfb2225
caps.latest.revision: 1
author: gregvanl
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
ms.sourcegitcommit: 3cd705d703b3d745c502290422e29b3c6da39ee5
ms.openlocfilehash: 981deb91768c98ef935c57582c34b805d6ce8ed7
ms.contentlocale: ja-jp
ms.lasthandoff: 08/22/2017

---
# <a name="installing-outside-the-extensions-folder"></a>Installing outside the extensions folder

Starting with Visual Studio 2017 and VSIX v3 (version 3), there is now support for installing extension assets outside of the extensions folder. Currently, the following locations are enabled as valid installation locations (where [INSTALLDIR] is mapped to the Visual Studio instance's installation directory):

* [INSTALLDIR]\Common7\IDE\PublicAssemblies
* [INSTALLDIR]\Common7\IDE\ReferenceAssemblies
* [INSTALLDIR]\MSBuild
* [INSTALLDIR]\Schemas
* [INSTALLDIR]\Licenses
* [INSTALLDIR]\RemoteDebugger
* [INSTALLDIR]\VSTargets

>**Note:** The VSIX format does not allow you to install outside the VS install folder structure.

In order to support installing to these directories, the VSIX must be installed "per-instance per-machine". This can be enabled by checking the "all-users" checkbox in the extension.vsixmanifest designer:

![check all users](media/check-all-users.png)

## <a name="how-to-set-the-installroot"></a>How to set the InstallRoot

To set the installation directories, you can use the **Properties** window in Visual Studio. For instance, you can set the `InstallRoot` property of a project reference to one of the above locations:

![install root properties](media/install-root-properties.png)

This will add some metadata to the corresponding `ProjectReference` property inside of the VSIX project's .csproj file:

```xml
 <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
        <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
        <Name>ClassLibrary1</Name>
        <InstallRoot>PublicAssemblies</InstallRoot>
 </ProjectReference>
```

>**Note:** You can edit the .csproj file directly, if you prefer.

## <a name="how-to-set-a-subpath-under-the-installroot"></a>How to set a subpath under the InstallRoot

If you'd like to install to a subpath underneath the `InstallRoot`, you can do so by setting the `VsixSubPath` property just like the `InstallRoot` property. For instance, say we want our project reference's output to install to '[INSTALLDIR]\MSBuild\MyCompany\MySDK\1.0'. We can do this easily with the property designer:

![set subpath](media/set-subpath.png)

The corresponding .csproj changes will look like this:

```xml
<ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
       <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
       <Name>ClassLibrary1</Name>
       <InstallRoot>MSBuild</InstallRoot>
       <VSIXSubPath>MyCompany\MySDK\1.0</VSIXSubPath>
</ProjectReference>
```

## <a name="extra-information"></a>Extra information

The property designer changes apply to more than just project references; you can set the `InstallRoot` metadata for items inside of your project as well (using the same methods described above).

