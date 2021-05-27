---
title: SharePoint のパッケージ化と配置の拡張 | Microsoft Docs
description: SharePoint のパッケージ化と配置を拡張します。 配置手順と構成を作成します。 配置競合を処理します。 検証規則をカスタマイズします。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: cd4967e38738018f9b30365575a2dcb9e8970963
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99948753"
---
# <a name="extend-sharepoint-packaging-and-deployment"></a>SharePoint のパッケージ化と配置の拡張
  SharePoint プロジェクトのパッケージ化と配置のプロセスを拡張できます。

## <a name="create-deployment-steps"></a>配置手順を作成する
 SharePoint プロジェクトを配置するとき、[!INCLUDE[vs_current_short](../sharepoint/includes/vs-current-short-md.md)] によって一連の配置手順が実行されます。 Visual Studio には、ソリューションの取り消しや追加など、さまざまなタスクに関する組み込みの配置手順が用意されています。 ただし、配置手順は独自に作成することもできます。

 配置手順の作成方法のチュートリアルについては、「[チュートリアル: SharePoint プロジェクトのカスタム配置手順の作成](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)」を参照してください。

## <a name="create-deployment-configurations"></a>配置構成を作成する
 配置構成は、特定のプロジェクトについて実行される一連の配置手順ですが、すべての SharePoint プロジェクト項目に影響を与えることがあります。 すべての配置構成には、プロジェクトが配置されるときに実行される手順と、プロジェクトが取り消されるときに実行される手順が含まれています。 [!INCLUDE[vs_current_short](../sharepoint/includes/vs-current-short-md.md)] には、組み込みの配置構成が 2 つ付属していますが、自分独自で作成することもできます。 配置構成を自分で作成する場合、組み込みの配置手順と独自に作成した配置手順とを混在させることができます。

 配置構成の作成方法のチュートリアルについては、「[チュートリアル: SharePoint プロジェクトのカスタム配置手順の作成](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)」を参照してください。

## <a name="run-code-when-a-sharepoint-solution-is-deployed-or-retracted"></a>SharePoint ソリューションの配置時または取り消し時にコードを実行する
 SharePoint ソリューションの配置時または取り消し時に、別途タスクを実行するためにイベントを処理することができます。 Visual Studio では、次のシナリオで処理できるイベントが生成されます。

- SharePoint プロジェクト項目について各配置手順が実行される前後。 詳細については、「[方法: 配置手順の実行時にコードを実行する](../sharepoint/how-to-run-code-when-deployment-steps-are-executed.md)」を参照してください。

- SharePoint プロジェクトの配置または取り消しが行われる前後。 詳細については、「[方法: SharePoint プロジェクトの配置時または取り消し時にコードを実行する](../sharepoint/how-to-run-code-when-a-sharepoint-project-is-deployed-or-retracted.md)」を参照してください。

## <a name="handle-deployment-conflicts"></a>配置競合を処理する
 モジュール、Web パーツ、リスト インスタンス、コンテンツ タイプなど、一部の種類の SharePoint プロジェクト項目では、組み込みの配置競合の解決が用意されています。 これらのいずれかのプロジェクト項目が含まれるソリューションを配置すると、Visual Studio は、まず、配置しようとしている項目に含まれるファイルと同じ名前、URL、または ID を持つファイルが、SharePoint サイトに既に存在しているかどうかを確認します。 競合が発生する場合、Visual Studio に自動的に競合を解決させることも、Visual Studio に競合を解決させるか配置を取り消すかを判断するようユーザーに要求することもできます。 詳細については、「 [Troubleshooting SharePoint Packaging and Deployment](../sharepoint/troubleshooting-sharepoint-packaging-and-deployment.md)」を参照してください。

 配置競合を確認および解決する独自のコードを使用して、この機能を拡張できます。 詳細については、「[方法: 配置競合を処理する](../sharepoint/how-to-handle-deployment-conflicts.md)」を参照してください。

## <a name="run-command-line-operations-before-or-after-a-project-is-deployed"></a>プロジェクトが配置される前と後にコマンド ライン操作を実行する
 SharePoint ソリューションの配置時にコマンド ライン操作を実行する場合、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> オブジェクトの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.PreDeploymentCommand%2A> プロパティと <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.PostDeploymentCommand%2A> プロパティを設定することができます。 これらのコマンドは、プロジェクトが配置される前と後に Visual Studio によって実行されます。

 場合によっては、配置の競合が発生することがあります。 競合を解決する方法はいくつかあります。 詳細については、「[SharePoint のパッケージ化と配置のトラブルシューティング](../sharepoint/troubleshooting-sharepoint-packaging-and-deployment.md)」を参照してください。

## <a name="customize-validation-rules"></a>検証規則をカスタマイズする
 ソリューション パッケージ (.wsp) を配置する前に、フィーチャーまたはパッケージが有効であることを検証するために、カスタムのフィーチャー検証規則およびパッケージ検証規則を作成できます。 たとえば、検証に関する問題の修正に役立つように、情報、警告、またはエラーを開発者に報告できます。 詳細については、「[方法:SharePoint ソリューションのフィーチャーとパッケージのカスタム検証規則を作成する](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: 配置手順の実行時にコードを実行する](../sharepoint/how-to-run-code-when-deployment-steps-are-executed.md)
- [チュートリアル: SharePoint プロジェクトのカスタム配置手順の作成](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)
- [方法: SharePoint ソリューションの機能とパッケージの検証を作成する](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md)
- [SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)
