---
title: Workflow Foundation プロジェクトを作成します。
ms.date: 06/25/2018
ms.topic: conceptual
helpviewer_keywords:
- Workflow Designer, creating a workflow project
- creating a workflow project
ms.assetid: 235a125e-ebe7-4a98-bf77-86c8558728fb
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 15c02312d5c257f13b9c0394790bc8a2611d7972
ms.sourcegitcommit: 489aca71046fb6e4aafd0a4509cd7dc149d707b1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2019
ms.locfileid: "58414759"
---
# <a name="workflow-project-templates"></a>ワークフロー プロジェクト テンプレート

Visual Studio プロジェクト テンプレートを使用して、ワークフロー、Windows Communication Foundation (WCF) のワークフロー サービス、カスタム アクティビティ、およびカスタム アクティビティ デザイナーを作成できます。 この記事では、Visual Studio で使用できるプロジェクト テンプレートをライブラリやアプリケーションを作成する方法について説明します。

## <a name="create-a-workflow-project"></a>ワークフロー プロジェクトを作成する

Visual Studio には、4 つの異なるワークフロー プロジェクト テンプレートが用意されています。

- ワークフロー コンソール アプリケーション

- WCF ワークフロー サービス アプリ

- アクティビティ ライブラリ

- アクティビティ デザイナー ライブラリ

これらのテンプレートにアクセスするには、まずインストール、 **Windows Workflow Foundation** Visual Studio のコンポーネント。 詳細については、[Windows Workflow Foundation のインストール](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation)を参照してください。

1. インストールした後、 **Windows Workflow Foundation**コンポーネントで、**ファイル** > **新規** > **プロジェクト**.

1. 検索し、たとえば、ワークフロー プロジェクト テンプレートを選択、**ワークフロー コンソール アプリケーション**テンプレート。

1. プロジェクトを作成する手順を続行します。

   > [!NOTE]
   > 既存のソリューションに新しいプロジェクトを追加する場合は、Visual Studio でそのソリューションを開きでソリューションを右クリックして**ソリューション エクスプ ローラー**、選び**追加** > **新規プロジェクト**します。

## <a name="workflow-console-app"></a>ワークフロー コンソール アプリケーション

選択した場合、**ワークフロー コンソール アプリケーション**テンプレート、Visual Studio で XAML ワークフロー定義を作成します。 ワークフロー デザイナーが開き、作成したワークフローのキャンバスが表示されます。 ワークフローを作成するアクティビティまたはからには、その他のワークフロー項目をドラッグします。**ツールボックス**デザイン サーフェイスにします。

## <a name="wcf-workflow-service-app"></a>WCF ワークフロー サービス アプリ

選択した場合、 **WCF ワークフロー サービス アプリケーション**テンプレート、Visual Studio XAML としてのサービス定義を作成します。 ワークフロー デザイナーでデザイン ビューが表示されます、<xref:System.Activities.Statements.Sequence>アクティビティのセットを含む<xref:System.ServiceModel.Activities.Receive>と<xref:System.ServiceModel.Activities.SendReply>アクティビティ。

## <a name="activity-library"></a>アクティビティ ライブラリ

選択した場合、**アクティビティ ライブラリ**テンプレート、Visual Studio で XAML アクティビティ定義を作成します。 ワークフロー デザイナーが開き、カスタム アクティビティのキャンバスが表示されます。 アクティビティをドラッグ**ツールボックス**に含めるカスタム アクティビティ デザイン サーフェイスにします。

> [!NOTE]
> 1 つだけの子アクティビティは、カスタム アクティビティの本体で許可されています。 ただし、その子アクティビティが複合アクティビティにするなどを<xref:System.Activities.Statements.Sequence>アクティビティまたは<xref:System.Activities.Statements.Flowchart>アクティビティ。

## <a name="activity-designer-library"></a>アクティビティ デザイナー ライブラリ

選択した場合、**アクティビティ デザイナー ライブラリ**テンプレート、Visual Studio で XAML と分離コード実装ファイル、アクティビティ デザイナー定義を作成します。 ワークフロー デザイナーが開き、アクティビティ デザイナーのキャンバスが表示されます。 ドラッグ Windows Presentation Foundation (WPF) コントロールを**ツールボックス**カスタム アクティビティ デザイナーで使用するデザイン サーフェイスにします。

カスタム アクティビティ デザイナーを実装する方法の例は、次を参照してください。[方法。カスタム アクティビティ デザイナーを作成](/dotnet/framework/windows-workflow-foundation/how-to-create-a-custom-activity-designer)です。

> [!NOTE]
> カスタム アクティビティと .NET Framework の既定の活動は、カスタム アクティビティ デザイナーを使用できます。

## <a name="see-also"></a>関連項目

- [ワークフロー デザイナーを使用します。](developing-applications-with-the-workflow-designer.md)
- [(.NET Framework) のワークフローを設計します。](/dotnet/framework/windows-workflow-foundation/designing-workflows)