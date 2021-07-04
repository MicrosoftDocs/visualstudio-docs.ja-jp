---
title: プロジェクト ファイルへのデータの保存 | Microsoft Docs
description: プロジェクト ファイル内にサブタイプ固有のデータを保存および取得するために Managed Package Framework に用意されているインターフェイスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- data [Visual Studio], saving in project files
- project files
- project files, saving data
ms.assetid: a3d4b15b-a91e-41ba-b235-e62632d11bc5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5859fc9286a3e584c04ccacc1d8b8a35d98dea89
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904982"
---
# <a name="save-data-in-project-files"></a>プロジェクト ファイルにデータを保存する
プロジェクト サブタイプを使用すると、サブタイプ固有のデータをプロジェクト ファイルに保存および取得できます。 Managed Package Framework (MPF) には、このタスクを実行するための 2 つのインターフェイスが用意されています。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> インターフェイスを使用すると、プロジェクト ファイルの **MSBuild** セクションからプロパティ値にアクセスできます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> に用意されているメソッドは、ユーザーがビルド関連データを読み込むまたは保存する必要があるときはいつでも、任意のユーザーが呼び出すことができます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> は、非ビルド関連データを自由形式の XML で保持するために使用されます。 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> に用意されているメソッドは、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] により、非ビルド関連データをプロジェクト ファイルに保持する必要がある場合は常に、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] によって呼び出されます。

  ビルド関連データと非ビルド関連データを保持する方法の詳細については、[MSBuild プロジェクト ファイルへのデータの保持](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)に関するページを参照してください。

## <a name="save-and-retrieve-build-related-data"></a>ビルド関連データの保存と取得

### <a name="to-save-a-build-related-data-in-the-project-file"></a>ビルド関連データをプロジェクト ファイルに保存するには

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A> メソッドを呼び出して、プロジェクト ファイルの完全なパスを保存します。

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

### <a name="to-retrieve-build-related-data-from-the-project-file"></a>プロジェクト ファイルからビルド関連データを取得するには

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.GetPropertyValue%2A> メソッドを呼び出して、プロジェクト ファイルの完全なパスを取得します。

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

## <a name="save-and-retrieve-non-build-related-data"></a>非ビルド関連データの保存と取得

### <a name="to-save-non-build-related-data-in-the-project-file"></a>非ビルド関連データをプロジェクト ファイルに保存するには

1. XML フラグメントが現在のファイルに最後に保存されてから変更されたかどうかを判断するには、<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.IsFragmentDirty%2A> メソッドを実装します。

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

2. XML データをプロジェクト ファイルに保存するには、<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Save%2A> メソッドを実装します。

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

### <a name="to-retrieve-non-build-related-data-in-the-project-file"></a>非ビルド関連データをプロジェクト ファイルに取得するには

1. プロジェクト拡張プロパティとその他のビルドに依存しないデータを初期化するには、<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.InitNew%2A> メソッドを実装します。 このメソッドは、プロジェクト ファイルに XML 構成データが存在しない場合に呼び出されます。

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

2. プロジェクト ファイルから XML データを読み込むには、<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Load%2A> メソッドを実装します。

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
> このトピックで取り上げるすべてのコード例は、[VSSDK サンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)の大きな例の一部です。

## <a name="see-also"></a>こちらもご覧ください
- [MSBuild プロジェクト ファイルにデータを保持する](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)
