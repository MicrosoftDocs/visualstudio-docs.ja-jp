---
title: '方法: SharePoint コマンドを実行する |Microsoft Docs'
description: SharePoint ツールの拡張機能からサーバー オブジェクト モデル API を呼び出すためのカスタム SharePoint コマンドを作成する方法について確認してください。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint commands [SharePoint development in Visual Studio], executing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4e22ade9b2414e1d598065bb9e417c4706f75a07
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217178"
---
# <a name="how-to-execute-a-sharepoint-command"></a>方法: SharePoint コマンドを実行する
  SharePoint ツールの拡張機能でサーバー オブジェクト モデルを使用する場合は、API を呼び出すためのカスタム *SharePoint コマンド* を作成する必要があります。 コマンドを定義し、SharePoint ツールの拡張機能と共に配置したら、拡張機能でコマンドを実行して、SharePoint サーバー オブジェクト モデルを呼び出すことができます。 コマンドを実行するには、<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> オブジェクトの ExecuteCommand メソッドのいずれかを使用します。

 SharePoint コマンドの目的について詳しくは、「[SharePoint オブジェクト モデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)」をご覧ください。

### <a name="to-execute-a-sharepoint-command"></a>SharePoint コマンドを実行するには

1. SharePoint ツールの拡張機能で、<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> オブジェクトを取得します。 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> オブジェクトを取得する方法は、作成する拡張機能の種類によって異なります。

    - SharePoint プロジェクト システムの拡張機能では、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.SharePointConnection%2A> プロパティを使用します。

         プロジェクト システムの拡張機能について詳しくは、「[SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)」をご覧ください。

    - **サーバー エクスプローラー** の **[SharePoint 接続]** ノードの拡張機能では、<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeContext.SharePointConnection%2A> プロパティを使用します。 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeContext> オブジェクトを取得するには、<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.Context%2A> プロパティを使用します。

         **サーバー エクスプローラー** の拡張機能について詳しくは、「[サーバー エクスプローラーで SharePoint 接続ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)」をご覧ください。

    - SharePoint ツールの拡張機能の一部ではないコード (プロジェクト テンプレート ウィザードなど) では、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.SharePointConnection%2A> プロパティを使用します。

         プロジェクト サービスの取得について詳しくは、「[SharePoint プロジェクト サービスの使用](../sharepoint/using-the-sharepoint-project-service.md)」をご覧ください。

2. <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> オブジェクトの ExecuteCommand メソッドのいずれかを呼び出します。 実行するコマンドの名前を、ExecuteCommand メソッドの 1 つ目の引数に渡します。 コマンドにカスタム パラメーターがある場合は、そのパラメーターを ExecuteCommand メソッドの 2 つ目の引数に渡します。

     サポートされているコマンド シグネチャごとに、異なる ExecuteCommand オーバーロードがあります。 次の表に、サポートされているシグネチャと、各シグネチャに使用するオーバーロードを示します。

    |コマンド シグネチャ|使用する ExecuteCommand オーバーロード|
    |-----------------------|------------------------------------|
    |コマンドには既定の <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> パラメーターのみがあり、戻り値はない。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |コマンドには既定の <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> パラメーターのみがあり、戻り値がある。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |コマンドに 2 つのパラメーター (既定の <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> パラメーターとカスタム パラメーター) があり、戻り値はない。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |コマンドには、2 つのパラメーターと戻り値がある。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|

## <a name="example"></a>例
 次のコード例は、「[方法: SharePoint コマンドを作成する](../sharepoint/how-to-create-a-sharepoint-command.md)」で説明されている `Contoso.Commands.UpgradeSolution` コマンドを、<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A> オーバーロードを使って呼び出す方法を示したものです。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/upgradestep.cs" id="Snippet6":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/upgradestep.vb" id="Snippet6":::

 この例に示す `Execute` メソッドは、カスタムの配置手順での、<xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep.Execute%2A> インターフェイスの <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep> メソッドの実装です。 このコードをより詳細な例のコンテキストで確認したい場合は、「[チュートリアル: SharePoint プロジェクトのカスタム配置手順の作成](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)」を参照してください。

 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A> メソッドの呼び出しについては、次の点に注意してください。

- 1 つ目のパラメーターは、呼び出すコマンドを識別するものです。 この文字列は、コマンド定義で <xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute> に渡す値と一致します。

- 2 つ目のパラメーターは、コマンドのカスタム (2 つ目の) パラメーターに渡す値です。 今回の場合は、SharePoint サイトにアップグレードされる *.wsp* ファイルの完全なパスになります。

- このコードでは、暗黙的な <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> パラメーターはコマンドに渡されません。 このパラメーターは、SharePoint プロジェクト システムの拡張機能から、または **サーバー エクスプローラー** の **[SharePoint 接続**] ノードの拡張機能からコマンドを呼び出すときに、コマンドに自動的に渡されます。 他の種類のソリューション (<xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイスを実装するプロジェクト テンプレート ウィザードなど) では、このパラメーターは **null** になります。

## <a name="compile-the-code"></a>コードのコンパイル
 この例では、Microsoft.VisualStudio.SharePoint アセンブリへの参照が必要です。

## <a name="see-also"></a>こちらもご覧ください
- [SharePoint オブジェクト モデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [方法: SharePoint コマンドを作成する](../sharepoint/how-to-create-a-sharepoint-command.md)
- [チュートリアル: サーバー エクスプローラーを拡張して Web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
