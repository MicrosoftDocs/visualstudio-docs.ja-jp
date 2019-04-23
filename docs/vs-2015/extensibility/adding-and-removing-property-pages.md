---
title: 追加とプロパティ ページの削除 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- property pages, adding
- property pages, project subtypes
- property pages, removing
ms.assetid: 34853412-ab8a-4caa-9601-7d0727b2985d
caps.latest.revision: 30
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0b7845d80b895d1b4c68afc59f2d2fe821be11f7
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60102797"
---
# <a name="adding-and-removing-property-pages"></a>プロパティ ページの追加と削除
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プロジェクト デザイナーは、プロジェクトのプロパティ、設定、および内のリソースを管理するための一元的な場所を提供します。[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]します。 単一のウィンドウとして表示されます、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]統合開発環境 (IDE) と、左側のタブを使用してアクセスされる右側のウィンドウの数値が含まれています。 プロジェクト デザイナーのペイン (プロパティ ページとも呼ばれます) は、プロジェクトの種類と言語によって異なります。 プロジェクト デザイナーをアクセスするのには、**プロパティ**コマンドを**プロジェクト**メニュー。  
  
 多くの場合、プロジェクトのサブタイプは、プロジェクト デザイナーに追加のプロパティ ページを表示する必要があります。 同様に、いくつかのプロジェクト サブタイプは、組み込みのプロパティ ページを削除する必要があります。 いずれかには、プロジェクトのサブタイプを実装する必要があります、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>インターフェイスし、オーバーライド、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>メソッド。 このメソッドをオーバーライドしを使用して`propId`パラメーターの値のいずれかを含む、<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>列挙型でフィルター処理、追加またはプロジェクトのプロパティを削除することができます。 たとえば、構成に依存するプロパティ ページにページを追加する必要があります。 これを行うには、構成に依存するプロパティ ページをフィルター処理し、既存のリストに新しいページを追加する必要があります。  
  
## <a name="adding-and-removing-property-pages-in-project-designer"></a>追加して、プロジェクト デザイナーのプロパティ ページを削除します。  
  
#### <a name="to-remove-a-property-page-in-project-designer"></a>プロジェクト デザイナーのプロパティ ページを削除するには  
  
1. 上書き、`GetProperty(uint itemId, int propId, out object property)`メソッドをプロパティ ページをフィルター処理し、取得、`clsids`一覧。  
  
    ```vb  
    Protected Overrides int GetProperty(uint itemId, int propId, out object property)  
    Protected Overrides Function GetProperty(ByVal itemId As UInteger, ByVal propId As Integer, ByRef [property] As Object) As Integer  
        'Use propId to filter configuration-independent property pages.  
        Select Case propId  
            ....   
            Case CInt(Fix(__VSHPROPID2.VSHPROPID_PropertyPagesCLSIDList))  
                'Get a semicolon-delimited list of clsids of the configuration-independent property pages  
                ErrorHandler.ThrowOnFailure(MyBase.GetProperty(itemId, propId, [property]))  
                   Dim propertyPagesList As String = ((String)[property]).ToUpper(CultureInfo.InvariantCulture)  
                'Remove the property page here  
                   ....  
            ....  
        End Select  
            ....   
        Return MyBase.GetProperty(itemId, propId, [property])  
    End Function  
  
    ```  
  
    ```csharp  
    protected override int GetProperty(uint itemId, int propId, out object property)  
    {  
        //Use propId to filter configuration-independent property pages.  
        switch (propId)  
        {  
            . . . .  
  
            case (int)__VSHPROPID2.VSHPROPID_PropertyPagesCLSIDList:  
                {  
                    //Get a semicolon-delimited list of clsids of the configuration-independent property pages  
                    ErrorHandler.ThrowOnFailure(base.GetProperty(itemId, propId, out property));  
                    string propertyPagesList = ((string)property).ToUpper(CultureInfo.InvariantCulture);  
                    //Remove the property page here  
                    . . . .  
                }  
             . . . .  
         }  
            . . . .  
        return base.GetProperty(itemId, propId, out property);  
    }  
    ```  
  
2. 削除、**ビルド イベント**ページから取得した`clsids`一覧。  
  
    ```vb  
    Private buildEventsPageGuid As String = "{1E78F8DB-6C07-4D61-A18F-7514010ABD56}"  
    Private index As Integer = propertyPagesList.IndexOf(buildEventsPageGuid)  
    If index <> -1 Then  
        ' GUIDs are separated by ';' so if you remove the last GUID, also remove the last ';'  
        Dim index2 As Integer = index + buildEventsPageGuid.Length + 1  
        If index2 >= propertyPagesList.Length Then  
            propertyPagesList = propertyPagesList.Substring(0, index).TrimEnd(";"c)  
        Else  
            propertyPagesList = propertyPagesList.Substring(0, index) + propertyPagesList.Substring(index2)  
        End If  
    End If  
    'New property value  
    property = propertyPagesList  
    ```  
  
    ```csharp  
    string buildEventsPageGuid = "{1E78F8DB-6C07-4D61-A18F-7514010ABD56}";  
    int index = propertyPagesList.IndexOf(buildEventsPageGuid);  
    if (index != -1)  
    {  
        // GUIDs are separated by ';' so if you remove the last GUID, also remove the last ';'  
        int index2 = index + buildEventsPageGuid.Length + 1;  
        if (index2 >= propertyPagesList.Length)  
            propertyPagesList = propertyPagesList.Substring(0, index).TrimEnd(';');  
        else  
            propertyPagesList = propertyPagesList.Substring(0, index) + propertyPagesList.Substring(index2);  
    }  
    //New property value  
    property = propertyPagesList;  
    ```  
  
#### <a name="to-add-a-property-page-in-project-designer"></a>プロジェクト デザイナーのプロパティ ページを追加するには  
  
1. 追加するプロパティ ページを作成します。  
  
    ```vb  
    Class DeployPropertyPage  
            Inherits Form  
            Implements Microsoft.VisualStudio.OLE.Interop.IPropertyPage  
        'Summary: Return a stucture describing your property page.  
        ....   
        Public Sub GetPageInfo(ByVal pPageInfo As Microsoft.VisualStudio.OLE.Interop.PROPPAGEINFO())  
            Dim info As PROPPAGEINFO = New PROPPAGEINFO()  
            info.cb = CUInt(Marshal.SizeOf(GetType(PROPPAGEINFO)))  
            info.dwHelpContext = 0  
            info.pszDocString = Nothing  
            info.pszHelpFile = Nothing  
            info.pszTitle = "Deployment" 'Assign tab name  
            info.SIZE.cx = Me.Size.Width  
            info.SIZE.cy = Me.Size.Height  
            If Not pPageInfo Is Nothing AndAlso pPageInfo.Length > 0 Then  
                pPageInfo(0) = info  
            End If  
        End Sub  
    End Class  
    ```  
  
    ```csharp  
    class DeployPropertyPage : Form, Microsoft.VisualStudio.OLE.Interop.IPropertyPage  
    {  
        . . . .   
        //Summary: Return a stucture describing your property page.  
        public void GetPageInfo(Microsoft.VisualStudio.OLE.Interop.PROPPAGEINFO[] pPageInfo)  
        {  
            PROPPAGEINFO info = new PROPPAGEINFO();  
            info.cb = (uint)Marshal.SizeOf(typeof(PROPPAGEINFO));  
            info.dwHelpContext = 0;  
            info.pszDocString = null;  
            info.pszHelpFile = null;  
            info.pszTitle = "Deployment";  //Assign tab name  
            info.SIZE.cx = this.Size.Width;  
            info.SIZE.cy = this.Size.Height;  
            if (pPageInfo != null && pPageInfo.Length > 0)  
                pPageInfo[0] = info;  
        }  
    }  
    ```  
  
2. 新しいプロパティ ページを登録します。  
  
    ```vb  
    <MSVSIP.ProvideObject(GetType(DeployPropertyPage), RegisterUsing = RegistrationMethod.CodeBase)>  
    ```  
  
    ```csharp  
    [MSVSIP.ProvideObject(typeof(DeployPropertyPage), RegisterUsing = RegistrationMethod.CodeBase)]  
    ```  
  
3. 上書き、`GetProperty(uint itemId, int propId, out object property)`プロパティ ページをフィルター処理を取得するメソッド、`clsids`を一覧表示し、新しいプロパティ ページを追加します。  
  
    ```vb  
    Protected Overrides Function GetProperty(ByVal itemId As UInteger, ByVal propId As Integer, ByRef [property] As Object) As Integer  
        'Use propId to filter configuration-dependent property pages.  
        Select Case propId  
            ....   
            case CInt(Fix(__VSHPROPID2.VSHPROPID_CfgPropertyPagesCLSIDList)):  
                'Get a semicolon-delimited list of clsids of the configuration-dependent property pages.  
                ErrorHandler.ThrowOnFailure(MyBase.GetProperty(itemId, propId, [property]))  
                'Add the Deployment property page.  
                [property] &= ";"c + GetType(DeployPropertyPage).GUID.ToString("B")  
        End Select  
            ....   
            Return MyBase.GetProperty(itemId, propId, [property])  
    End Function  
    ```  
  
    ```csharp  
    protected override int GetProperty(uint itemId, int propId, out object property)  
    {  
        //Use propId to filter configuration-dependent property pages.  
        switch (propId)  
        {  
            . . . .  
            case (int)__VSHPROPID2.VSHPROPID_CfgPropertyPagesCLSIDList:  
                {  
                    //Get a semicolon-delimited list of clsids of the configuration-dependent property pages.  
                    ErrorHandler.ThrowOnFailure(base.GetProperty(itemId, propId, out property));  
                    //Add the Deployment property page.  
                    property += ';' + typeof(DeployPropertyPage).GUID.ToString("B");  
                }  
         }  
            . . . .  
        return base.GetProperty(itemId, propId, out property);  
    }  
    ```  
  
> [!NOTE]
>  このトピックで提供されたすべてのコード例は、例のパーツ[VSSDK のサンプル](../misc/vssdk-samples.md)します。  
  
## <a name="see-also"></a>関連項目  
 [プロジェクト サブタイプ](../extensibility/internals/project-subtypes.md)
