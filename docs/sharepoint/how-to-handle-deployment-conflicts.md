---
title: '方法: 配置競合を処理する |Microsoft Docs'
description: SharePoint プロジェクト項目の配置競合を処理するために、独自のコードを実装する方法の例を紹介します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
helpviewer_keywords:
- SharePoint development in Visual Studio, extending deployment
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b09db3fecde5d4b87b24963930b2783b0c68052c
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106213980"
---
# <a name="how-to-handle-deployment-conflicts"></a>方法: 配置競合を処理する
  SharePoint プロジェクト項目の配置競合を処理するために、独自のコードを提供することができます。 たとえば、現在のプロジェクト項目のファイルが配置場所に既に存在するかどうかを確認したうえで、現在のプロジェクト項目が配置される前に、配置済みのファイルを削除することができます。 配置競合の詳細については、「[SharePoint のパッケージ化と配置の拡張](../sharepoint/extending-sharepoint-packaging-and-deployment.md)」を参照してください。

### <a name="to-handle-a-deployment-conflict"></a>配置競合を処理するには

1. プロジェクト項目の拡張機能、プロジェクトの拡張機能、または新しいプロジェクト項目の種類の定義を作成します。 詳細については、次のトピックを参照してください。

    - [方法: SharePoint プロジェクト項目の拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)

    - [方法: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

    - [方法: SharePoint プロジェクト項目の種類を定義する](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)

2. 拡張機能で、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType> オブジェクト (プロジェクト項目の拡張機能またはプロジェクトの拡張機能) または <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition> オブジェクト (新しいプロジェクト項目の種類の定義内) の <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> イベントを処理します。

3. イベント ハンドラーで、配置しようとしているプロジェクト項目と SharePoint サイトに配置されているソリューションとの間に競合があるかどうかを、シナリオに適用される条件に基づいて判定します。 配置しようとしているプロジェクト項目は、イベント引数パラメーターの <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemEventArgs.ProjectItem%2A> プロパティを使って分析できます。また、配置場所にあるファイルは、この目的のために定義した SharePoint コマンドを呼び出すことによって分析できます。

     多くの競合の種類では、どの配置手順が実行されているかを最初に確認する必要があります。 これは、イベント引数パラメーターの <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs.DeploymentStepInfo%2A> プロパティを使用することで実行できます。 通常は、組み込みの <xref:Microsoft.VisualStudio.SharePoint.Deployment.DeploymentStepIds.AddSolution> 配置手順で競合を検出するのが合理的ですが、任意の配置手順の間に競合を確認することもできます。

4. 競合が存在する場合は、イベント引数の <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs.Conflicts%2A> プロパティの <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflictCollection.Add%2A> メソッドを使って、新しい <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> オブジェクトを作成します。 このオブジェクトが、配置の競合を表します。 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflictCollection.Add%2A> メソッドの呼び出しでは、競合を解決するために呼び出されるメソッドも指定します。

## <a name="example"></a>例
 次のコード例は、リスト定義プロジェクト項目のプロジェクト項目拡張機能での配置競合を処理するための、基本的なプロセスを示したものです。 別の種類のプロジェクト項目の配置競合を処理するには、<xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> に別の文字列を渡します。 詳細については、「[SharePoint プロジェクト項目の拡張](../sharepoint/extending-sharepoint-project-items.md)」を参照してください。

 わかりやすくするために、この例の <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> イベント ハンドラーでは、配置競合が存在することを前提とします (つまり、常に新しい <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> オブジェクトを追加します)。`Resolve` メソッドは、競合が解決されたことを示すために **true** を返します。 実際のシナリオでは、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> イベント ハンドラーで、現在のプロジェクト項目内のファイルと配置場所にあるファイルとの間に競合があるかどうかを最初に確認し、競合が存在する場合にのみ、<xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> オブジェクトを追加するようにしてください。 たとえば、イベント ハンドラーの `e.ProjectItem.Files` プロパティを使ってプロジェクト項目内のファイルを分析し、SharePoint コマンドを呼び出して、配置場所にあるファイルを分析することができます。 同様に、実際のシナリオでは、`Resolve` メソッドで SharePoint コマンドを呼び出して、SharePoint サイトの競合を解決することもできます。 SharePoint コマンドの作成について詳しくは、「[方法: SharePoint コマンドを作成する](../sharepoint/how-to-create-a-sharepoint-command.md)」をご覧ください。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/deploymentconflict/extension/deploymentconflictextension.vb" id="Snippet1":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/deploymentconflict/extension/deploymentconflictextension.cs" id="Snippet1":::

## <a name="compile-the-code"></a>コードのコンパイル
 このコード例では、次のアセンブリへの参照が必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 拡張機能を配置するには、拡張機能と共に配布するアセンブリやその他のファイルに対応した、[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能 (VSIX) パッケージを作成します。 詳しくは、「[Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」をご覧ください。

## <a name="see-also"></a>こちらもご覧ください
- [SharePoint のパッケージ化と配置の拡張](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [SharePoint プロジェクト項目の拡張](../sharepoint/extending-sharepoint-project-items.md)
- [方法: 配置手順の実行時にコードを実行する](../sharepoint/how-to-run-code-when-deployment-steps-are-executed.md)
- [方法: SharePoint コマンドを作成する](../sharepoint/how-to-create-a-sharepoint-command.md)
