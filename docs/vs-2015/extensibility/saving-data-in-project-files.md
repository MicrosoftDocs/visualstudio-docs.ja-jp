---
title: プロジェクト ファイル内のデータ保存 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- data [Visual Studio], saving in project files
- project files
- project files, saving data
ms.assetid: a3d4b15b-a91e-41ba-b235-e62632d11bc5
caps.latest.revision: 29
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 31a9b093fc912be9db573b89d8c6b09e927c8b87
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60048724"
---
# <a name="saving-data-in-project-files"></a>プロジェクト ファイルでのデータの保存
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プロジェクト サブタイプは、保存し、プロジェクト ファイルのサブタイプに固有のデータを取得できます。 マネージ パッケージ フレームワーク (MPF) は、このタスクを実行する 2 つのインターフェイスを提供します。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>からアクセス プロパティの値により、インターフェイス、 **MSBuild**プロジェクト ファイルのセクション。 によって提供されるメソッド<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>ユーザーのニーズを読み込みまたは保存に関連するデータをビルドするたびにすべてのユーザーが呼び出すことができます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>自由形式の XML でないビルド関連のデータを保持するために使用します。 によって提供されるメソッド<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>によって呼び出される[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]たびに[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]非ビルド プロジェクト ファイルに関連するデータを保持する必要があります。  
  
  ビルドと非ビルド関連のデータを維持する方法の詳細については、次を参照してください。 [MSBuild プロジェクト ファイル内のデータの永続化](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)します。  
  
## <a name="saving-and-retrieving-build-related-data"></a>関連するデータの保存とビルドの取得  
  
#### <a name="to-save-a-build-related-data-in-the-project-file"></a>プロジェクト ファイル内のデータに関連するビルドを保存するには  
  
- 呼び出す、<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A>プロジェクト ファイルの完全なパスを保存するメソッド。  
  
    ```  
    private SpecializedProject project;  
    IVsBuildPropertyStorage projectStorage = (IVsBuildPropertyStorage)project;  
    string newFullPath = GetNewFullPath();  
    // Set a full path of the project file.  
    ErrorHandler.ThrowOnFailure(projectStorage.SetPropertyValue(  
        "MSBuildProjectDirectory",  
        String.Empty,  
        (uint)_PersistStorageType.PST_PROJECT_FILE, newFullPath));  
    ```  
  
#### <a name="to-retrieve-build-related-data-from-the-project-file"></a>関連するデータをプロジェクト ファイルからビルドを取得するには  
  
- 呼び出す、<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.GetPropertyValue%2A>プロジェクト ファイルの完全なパスを取得します。  
  
    ```  
    private SpecializedProject project;  
    IVsBuildPropertyStorage projectStorage = (IVsBuildPropertyStorage)project;  
    string fullPath;  
    // Get a full path of the project file.  
    ErrorHandler.ThrowOnFailure(projectStorage.GetPropertyValue(  
        "MSBuildProjectDirectory",  
        String.Empty,  
        (uint)_PersistStorageType.PST_PROJECT_FILE, out fullPath));  
    ```  
  
## <a name="saving-and-retrieving-non-build-related-data"></a>保存と取得以外のビルド関連データ  
  
#### <a name="to-save-non-build-related-data-in-the-project-file"></a>関連するプロジェクト ファイル内のデータを非ビルドを保存するには  
  
1. 実装、<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.IsFragmentDirty%2A>が最後に、XML フラグメントが変更されたかどうかを判断するメソッドは、現在のファイルを保存します。  
  
    ```  
    public int IsFragmentDirty(uint storage, out int pfDirty)  
    {  
        pfDirty = 0;  
        switch (storage)  
        {  
            case (uint)_PersistStorageType.PST_PROJECT_FILE:  
            {  
                if (isDirty)  
                    pfDirty |= 1;  
                break;  
            }  
            case (uint)_PersistStorageType.PST_USER_FILE:  
            {  
                // We do not store anything in the user file.  
                break;  
            }  
        }  
  
        // Forward the call to inner flavor(s)   
        if (pfDirty == 0 && innerCfg != null && this.innerCfg is IPersistXMLFragment)  
            return ((IPersistXMLFragment)this.innerCfg).IsFragmentDirty(storage, out pfDirty);  
  
        return VSConstants.S_OK;  
  
    }  
    ```  
  
2. 実装、<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Save%2A>プロジェクト ファイルに XML データを保存するメソッド。  
  
    ```  
    public int Save(ref Guid guidFlavor, uint storage, out string pbstrXMLFragment, int fClearDirty)  
    {  
        pbstrXMLFragment = null;  
  
        if (IsMyFlavorGuid(ref guidFlavor))  
        {  
            switch (storage)  
            {  
                case (uint)_PersistStorageType.PST_PROJECT_FILE:  
                {  
                    // Create XML for our data.  
                    XmlDocument doc = new XmlDocument();  
                    XmlNode root = doc.CreateElement(this.GetType().Name);  
  
                    XmlNode node = doc.CreateElement(targetsTag);  
                    node.AppendChild(doc.CreateTextNode(this.TargetsToExecute));  
                    root.AppendChild(node);  
  
                    node = doc.CreateElement(updateTargetsTag);  
                    node.AppendChild(doc.CreateTextNode(this.UpdateTargetList.ToString()));  
                    root.AppendChild(node);  
  
                    doc.AppendChild(root);  
                    // Get XML fragment representing our data  
                    pbstrXMLFragment = doc.InnerXml;  
  
                    if (fClearDirty != 0)  
                        isDirty = false;  
                    break;  
                }  
                case (uint)_PersistStorageType.PST_USER_FILE:  
                {  
                    // We do not store anything in the user file.  
                    break;  
                }  
            }  
        }  
  
        // Forward the call to inner flavor(s)  
        if (this.innerCfg != null && this.innerCfg is IPersistXMLFragment)  
            return ((IPersistXMLFragment)this.innerCfg).Save(ref guidFlavor, storage, out pbstrXMLFragment, fClearDirty);  
  
        return VSConstants.S_OK;  
    }  
    ```  
  
#### <a name="to-retrieve-non-build-related-data-in-the-project-file"></a>非ビルド プロジェクト ファイルに関連するデータを取得するには  
  
1. 実装、<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.InitNew%2A>プロジェクト拡張機能のプロパティとその他のビルドに依存しないデータを初期化します。 プロジェクト ファイルに存在する XML の構成データが存在しない場合は、このメソッドが呼び出されます。  
  
    ```  
    public int InitNew(ref Guid guidFlavor, uint storage)  
    {  
        //Return,if it is our guid.  
        if (IsMyFlavorGuid(ref guidFlavor))  
            return VSConstants.S_OK;  
  
        //Forward the call to inner flavor(s).  
        if (this.innerCfg != null && this.innerCfg is IPersistXMLFragment)  
            return ((IPersistXMLFragment)this.innerCfg).InitNew(ref guidFlavor, storage);  
  
        return VSConstants.S_OK;  
    ```  
  
2. 実装、<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Load%2A>プロジェクト ファイルから XML データを読み込むメソッド。  
  
    ```  
    public int Load(ref Guid guidFlavor, uint storage, string pszXMLFragment)  
    {  
        if (IsMyFlavorGuid(ref guidFlavor))  
        {  
            switch (storage)  
            {  
                case (uint)_PersistStorageType.PST_PROJECT_FILE:  
                {  
                    // Load our data from the XML fragment.  
                    XmlDocument doc = new XmlDocument();  
                    XmlNode node = doc.CreateElement(this.GetType().Name);  
                    node.InnerXml = pszXMLFragment;  
                    if (node == null  
                        || node.FirstChild == null  
                        || node.FirstChild.ChildNodes.Count == 0  
                        || node.FirstChild.ChildNodes[0].Name != targetsTag)  
                        break;  
                    this.TargetsToExecute = node.FirstChild.ChildNodes[0].InnerText;  
  
                    if (node.FirstChild.ChildNodes.Count <= 1  
                        || node.FirstChild.ChildNodes[1].Name != updateTargetsTag)  
                        break;  
                    this.UpdateTargetList = bool.Parse(node.FirstChild.ChildNodes[1].InnerText);  
                    break;  
                }  
                case (uint)_PersistStorageType.PST_USER_FILE:  
                {  
                    // We do not store anything in the user file.  
                    break;  
                }  
            }  
        }  
  
        // Forward the call to inner flavor(s)  
        if (this.innerCfg != null && this.innerCfg is IPersistXMLFragment)  
            return ((IPersistXMLFragment)this.innerCfg).Load(ref guidFlavor, storage, pszXMLFragment);  
  
        return VSConstants.S_OK;  
    }  
    ```  
  
> [!NOTE]
>  このトピックで提供されたすべてのコード例は、例のパーツ[VSSDK のサンプル](../misc/vssdk-samples.md)します。  
  
## <a name="see-also"></a>関連項目  
 [MSBuild プロジェクト ファイルでのデータの保持](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)
