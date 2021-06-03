---
title: '方法: 配置手順の実行時にコードを実行する | Microsoft Docs'
description: Visual Studio が配置手順を実行する前と後に SharePoint プロジェクト項目によって生成されたイベントを処理するコードを実行します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending deployment
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 74db1b73dded52ba15ea860873c49c0264f7fea7
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106214409"
---
# <a name="how-to-run-code-when-deployment-steps-are-executed"></a>方法: 配置手順の実行時にコードを実行する
  SharePoint プロジェクトの配置手順に関する追加のタスクを実行したい場合は、Visual Studio が各配置手順を実行する前と後に SharePoint プロジェクト項目によって生成されたイベントを処理できます。 詳細については、[SharePoint のパッケージ化と配置の拡張](../sharepoint/extending-sharepoint-packaging-and-deployment.md)に関するページを参照してください。

### <a name="to-run-code-when-deployment-steps-are-executed"></a>配置手順の実行時にコードを実行するには

1. プロジェクト項目の拡張機能、プロジェクトの拡張機能、または新しいプロジェクト項目の種類の定義を作成します。 詳細については、次のトピックを参照してください。

    - [方法: SharePoint プロジェクト項目の拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)

    - [方法: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

    - [方法: SharePoint プロジェクト項目の種類を定義する](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)

2. 拡張機能で、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType> オブジェクト (プロジェクト項目の拡張機能またはプロジェクトの拡張機能の場合) または <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition> オブジェクト (新しいプロジェクト項目の種類の定義の場合) の <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> および <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepCompleted> イベントを処理します。

3. イベント ハンドラーで、<xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs> および <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepCompletedEventArgs> パラメーターを使用して配置手順に関する情報を取得します。 たとえば、どの配置手順が実行されているかや、ソリューションが配置されているのか、または取り消されているのかを判定できます。

## <a name="example"></a>例
 次のコード例は、リスト インスタンス プロジェクト項目の拡張機能で <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> および <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepCompleted> イベントを処理する方法を示しています。 この拡張機能では、ソリューションの配置および取り消し中に Visual Studio がアプリケーション プールをリサイクルするときに **[出力]** ウィンドウに追加のメッセージを書き込みます。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/handledeploymentstepevents.vb" id="Snippet4":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/handledeploymentstepevents.cs" id="Snippet4":::

## <a name="compile-the-code"></a>コードのコンパイル
 この例には、次のアセンブリへの参照が必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 拡張機能を配置するには、その拡張機能で配布するアセンブリとその他のすべてのファイル用の [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能 (VSIX) パッケージを作成します。 詳細については、「[Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint のパッケージ化と配置を拡張する](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [チュートリアル: SharePoint プロジェクトのカスタム配置手順を作成する](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)
- [方法: SharePoint プロジェクトの配置時または取り消し時にコードを実行する](../sharepoint/how-to-run-code-when-a-sharepoint-project-is-deployed-or-retracted.md)
