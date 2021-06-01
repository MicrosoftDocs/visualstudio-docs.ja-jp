---
title: Workflow Foundation プロジェクトを作成する
description: Visual Studio で使用できるプロジェクト テンプレートで、ライブラリとアプリケーションを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 06/25/2018
ms.topic: conceptual
helpviewer_keywords:
- Workflow Designer, creating a workflow project
- creating a workflow project
ms.assetid: 235a125e-ebe7-4a98-bf77-86c8558728fb
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: cf8c0fe0b716cecee19c00bb0b300d4ffdc99355
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894362"
---
# <a name="workflow-project-templates"></a>ワークフロー プロジェクト テンプレート

Visual Studio のプロジェクト テンプレートを使用して、ワークフロー、Windows Communication Foundation (WCF) ワークフロー サービス、カスタム アクティビティ、カスタム アクティビティ デザイナーを作成できます。 この記事では、Visual Studio で使用できるプロジェクト テンプレートで、ライブラリとアプリケーションを作成する方法について説明します。

## <a name="create-a-workflow-project"></a>ワークフロー プロジェクトを作成する

Visual Studio には、4 つの異なるワークフロー プロジェクト テンプレートが用意されています。

- ワークフロー コンソール アプリ

- WCF ワークフロー サービス アプリ

- アクティビティ ライブラリ

- アクティビティ デザイナー ライブラリ

これらのテンプレートにアクセスするには、最初に Visual Studio の **Windows Workflow Foundation** コンポーネントをインストールします。 詳細については、「[Windows Workflow Foundation をインストールする](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation)」を参照してください。

1. **Windows Workflow Foundation** コンポーネントをインストールした後、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

1. ワークフロー プロジェクト テンプレート (**ワークフロー コンソール アプリケーション** テンプレートなど) を検索して選択します。

1. 続けてプロジェクトを作成します。

   > [!NOTE]
   > 既存のソリューションに新しいプロジェクトを追加する場合は、Visual Studio でそのソリューションを開き、**ソリューション エクスプローラー** でソリューションを右クリックして、 **[追加]**  >  **[新しいプロジェクト]** を選択します。

## <a name="workflow-console-app"></a>ワークフロー コンソール アプリ

**ワークフロー コンソール アプリケーション** テンプレートを選択すると、Visual Studio によって XAML にワークフロー定義が作成されます。 ワークフロー デザイナーが開き、作成したワークフロー用のキャンバスが表示されます。 ワークフローを作成するには、アクティビティなどのワークフロー項目を **[ツールボックス]** からデザイン サーフェイスにドラッグします。

## <a name="wcf-workflow-service-app"></a>WCF ワークフロー サービス アプリ

**WCF ワークフロー サービス アプリケーション** テンプレートを選択すると、Visual Studio によってサービス定義が XAML として作成されます。 ワークフロー デザイナーのデザイン ビューが開かれ、<xref:System.ServiceModel.Activities.Receive> と <xref:System.ServiceModel.Activities.SendReply> アクティビティのセットを含む <xref:System.Activities.Statements.Sequence> アクティビティが表示されます。

## <a name="activity-library"></a>アクティビティ ライブラリ

**アクティビティ ライブラリ** テンプレートを選択すると、Visual Studio によって XAML でアクティビティ定義が作成されます。 ワークフロー デザイナーが開き、カスタム アクティビティ用のキャンバスが表示されます。 **[ツールボックス]** のアクティビティをデザイン サーフェイスにドラッグし、カスタム アクティビティに含めます。

> [!NOTE]
> カスタム アクティビティの本体に含めることができる子アクティビティは 1 つだけです。 ただし、その子アクティビティは、<xref:System.Activities.Statements.Sequence> アクティビティや <xref:System.Activities.Statements.Flowchart> アクティビティなどの複合アクティビティでもかまいません。

## <a name="activity-designer-library"></a>アクティビティ デザイナー ライブラリ

**アクティビティ デザイナー ライブラリ** テンプレートを選択すると、Visual Studio によって、アクティビティ デザイナー定義が XAML と分離コード実装ファイルで作成されます。 ワークフロー デザイナーが開き、アクティビティ デザイナー用のキャンバスが表示されます。 **[ツールボックス]** から Windows Presentation Foundation (WPF) コントロールをデザイン サーフェイスにドラッグして、カスタム アクティビティ デザイナーで使用できるようにします。

カスタム アクティビティ デザイナーを実装する方法の例については、「[方法: カスタム アクティビティ デザイナーを作成する](/dotnet/framework/windows-workflow-foundation/how-to-create-a-custom-activity-designer)」を参照してください。

> [!NOTE]
> カスタム アクティビティ デザイナーは、カスタム アクティビティと既定の .NET アクティビティに使用できます。

## <a name="see-also"></a>関連項目

- [ワークフロー デザイナーを使用する](developing-applications-with-the-workflow-designer.md)
- [ワークフローの設計 (.NET Framework)](/dotnet/framework/windows-workflow-foundation/designing-workflows)
