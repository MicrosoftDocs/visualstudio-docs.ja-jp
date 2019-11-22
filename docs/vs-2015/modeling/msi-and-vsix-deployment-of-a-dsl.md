---
title: MSI and VSIX Deployment of a DSL | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 6ce16f06-1978-4e19-8cdc-441ee65a3fb2
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4917fc81f439ef0185a753fb1c4c85e460eb7681
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297744"
---
# <a name="msi-and-vsix-deployment-of-a-dsl"></a>DSL の MSI および VSIX 配置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

You can install a domain-specific language on your own computer or on other computers. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] must already be installed on the target computer.

## <a name="which"></a> Choosing between VSIX and MSI Deployment
 There are two methods of deploying a domain-specific language:

|メソッド|利点|
|------------|--------------|
|VSX ([!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Extension)|Very easy to deploy: Copy and execute the **.vsix** file from the DslPackage project.<br /><br /> For more information see [Installing and Uninstalling a DSL by using the VSX](#Installing).|
|MSI (installer file)|-   Allows the user to open [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] by double-clicking a DSL file.<br />-   Associates an icon with the DSL file type in the target computer.<br />-   Associates an XSD (XML schema) with the DSL file type. This avoids warnings when the file is loaded into [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].<br /><br /> You must add a setup project to your solution to create an MSI.<br /><br /> For more information, see [Deploying a DSL by using an MSI file](#msi).|

## <a name="Installing"></a> Installing and Uninstalling a DSL by using the VSX
 When your DSL is installed by this method, the user can open a DSL file from within [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], but the file cannot be opened from Windows Explorer.

#### <a name="to-install-a-dsl-by-using-the-vsx"></a>To install a DSL by using the VSX

1. In your computer, find the **.vsix** file that was built by your DSL Package project.

    1. In **Solution Explorer**, right-click the **DslPackage** project, and then click **Open Folder in Windows Explorer**.

    2. Locate the file **bin\\\*\\** _YourProject_ **.DslPackage.vsix**

2. Copy the **.vsix** file to the target computer on which you want to install the DSL. 自分のコンピューターでも別のコンピューターでもかまいません。

    - The target computer must have one of the editions of [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] that supports DSLs at run time. For more information, see [Supported Visual Studio Editions for Visualization & Modeling SDK](../modeling/supported-visual-studio-editions-for-visualization-amp-modeling-sdk.md).

    - The target computer must have one of the editions of [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] specified in **DslPackage\source.extensions.manifest**.

3. On the target computer, double-click the **.vsix** file.

     **Visual Studio 拡張機能インストーラー** が起動され、拡張機能がインストールされます。

4. [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]を起動または再起動します。

5. To test the DSL, use [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] to create a new file that has the extension that you defined for your DSL.

#### <a name="to-uninstall-a-dsl-that-was-installed-by-using-vsx"></a>To uninstall a DSL that was installed by using VSX

1. On the **Tools** menu, click **Extension Manager**.

2. **[インストール済みの拡張機能]** を展開します。

3. Select the extension in which the DSL is defined, and then click **Uninstall**.

   拡張機能の障害が原因で読み込みが失敗し、エラー ウィンドウにレポートが生成されることがまれにありますが、それは拡張機能マネージャーには表示されません。 その場合は、以下の場所からファイルを削除して、拡張機能を削除します。

   *LocalAppData* **\Microsoft\VisualStudio\10.0\Extensions**

## <a name="msi"></a> Deploying a DSL in an MSI
 By defining an MSI (Windows Installer) file for your DSL, you can allow users to open DSL files from Windows Explorer. You can also associate an icon and short description with your file name extension. In addition, the MSI can install an XSD that can be used to validate DSL files. If you want, you can add other components into the MSI that will be installed at the same time.

 For more information about MSI files and other deployment options, see [Deploying Applications, Services, and Components](../deployment/deploying-applications-services-and-components.md).

 To build an MSI, you add a Setup project to your [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] solution. The easiest method of creating a Setup project is to use the CreateMsiSetupProject.tt template, which you can download from the [VMSDK site](https://go.microsoft.com/fwlink/?LinkID=186128).

#### <a name="to-deploy-a-dsl-in-an-msi"></a>To Deploy a DSL in an MSI

1. Set `InstalledByMsi` in the extension manifest. This prevents the VSX from being installed and uninstalled except by the MSI. This is important if you will include other components in the MSI.

   1. Open DslPackage\source.extension.tt

   2. Insert the following line before `<SupportedProducts>`:

       ```
       <InstalledByMsi>true</InstalledByMsi>
       ```

2. Create or edit an icon that will represent your DSL in Windows Explorer. For example, edit **DslPackage\Resources\File.ico**

3. Make sure that the following attributes of your DSL are correct:

   - In DSL Explorer click the root node, and in Properties window, review:

       - 説明

       - Version

   - Click the **Editor** node and in the Properties window, click **Icon**. Set the value to reference an icon file in **DslPackage\Resources**, such as **File.ico**

   - On the **Build** menu, open **Configuration Manager**, and select the configuration that you want to build, such as **Release** or **Debug**.

4. Go to [Visualization and Modeling SDK home page](https://go.microsoft.com/fwlink/?LinkID=186128), and from the **Downloads** tab, download **CreateMsiSetupProject.tt**.

5. Add **CreateMsiSetupProject.tt** to your Dsl project.

    [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] will create a file named **CreateMsiSetupProject.vdproj**.

6. In Windows Explorer, copy Dsl\\*.vdproj to a new folder named Setup.

    (If you want, you can now exclude CreateMsiSetupProject.tt from your Dsl project.)

7. In **Solution Explorer**, add **Setup\\\*.vdproj** as an existing project.

8. On the **Project** menu, click **Project Dependencies**.

    In the **Project Dependencies** dialog box, select the setup project.

    Select the box next to **DslPackage**.

9. ソリューションをリビルドします。

10. In Windows Explorer, locate the built MSI file in your Setup project.

     Copy the MSI file to a computer on which you want to install your DSL. Double-click the MSI file. The installer runs.

11. In the target computer, create a new file that has the file extension of your DSL. Verify that:

    - In Windows Explorer list view, the file appears with the icon and description that you defined.

    - When you double-click the file, [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] starts, and opens the DSL file in your DSL editor.

    If you prefer, you can create the Setup project manually, instead of using the text template. For a walkthrough that includes this procedure see Chapter 5 of the [Visualization and Modeling SDK Lab](https://go.microsoft.com/fwlink/?LinkId=208878).

#### <a name="to-uninstall-a-dsl-that-was-installed-from-an-msi"></a>To uninstall a DSL that was installed from an MSI

1. In Windows, open the **Programs and Features** control panel.

2. Uninstall the DSL.

3. Visual Studio を再起動します。
