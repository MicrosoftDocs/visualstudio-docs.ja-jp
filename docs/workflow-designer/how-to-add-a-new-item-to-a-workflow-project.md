---
title: 'ワークフローデザイナー: ワークフロープロジェクトに新しい項目を追加する'
description: ワークフロープロジェクトを作成した後に、ワークフローアクティビティ、デザイナー、およびその他の使い慣れた Visual Studio 項目をプロジェクトに追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 06/25/2018
ms.topic: how-to
ms.assetid: 5c6180ca-af10-4513-b0cb-7d478fd84eab
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: af6563d21ce41d54e66f474de126c3bd4070ff8a
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94437971"
---
# <a name="how-to-add-a-new-item-to-a-workflow-project"></a>方法: ワークフロープロジェクトに新しい項目を追加する

ワークフロープロジェクトを作成したら、ワークフローアクティビティ、デザイナー、およびその他の使い慣れた Visual Studio 項目をプロジェクトに追加できます。

次の表は、ワークフロープロジェクトに追加できる Windows Workflow Foundation (WF) 項目を示しています。

| 名前 | 説明 |
|-| - |
| アクティビティ | 他のアクティビティで構成されるアクティビティ。 この項目を選択すると、新しいプロジェクトの [ **アクティビティライブラリ** ] テンプレートを選択したときに取得したものと同じ XAML ファイルがプロジェクトに追加されます。 この手順の詳細については、「 [ワークフロープロジェクトの作成](creating-a-workflow-project.md)」を参照してください。 |
| アクティビティ デザイナー | アクティビティのデザイン時の操作をカスタマイズするデザイナー。 この項目を選択すると、新しいプロジェクトに対して [ **アクティビティデザイナーライブラリ** ] テンプレートを選択したときに取得したものと同じファイルがプロジェクトに追加されます。 |
| Code アクティビティ | コードに記述される実行ロジックを含むアクティビティ。 <xref:System.Activities.CodeActivity.Execute%2A> メソッドのオーバーライドを含むソース コード ファイルは既に自動的に生成されています。 |
| WCF ワークフロー サービス | ワークフロー アクティビティを使用して作成された [!INCLUDE[indigo2](../workflow-designer/includes/indigo2_md.md)] サービス。 この項目を選択すると、新しいプロジェクトの **WCF ワークフローサービスアプリケーション** テンプレートを選択したときに取得したものと同じファイルがプロジェクトに追加されます。 この手順の詳細については、「 [方法: WCF ワークフローサービスアプリケーションを作成](creating-a-workflow-project.md)する」を参照してください。 |

## <a name="to-add-a-new-item-to-a-workflow-project"></a>ワークフロー プロジェクトに新しい項目を追加するには

1. **[プロジェクト]** メニューで、 **[新しい項目の追加]** を選択します。

   **[新しい項目の追加]** ダイアログ ボックスが開きます。

1. 左側のウィンドウで、[ **ワークフロー** ] カテゴリを選択し、ワークフロー項目テンプレートを選択します。

   > [!NOTE]
   > **ワークフロー** カテゴリが表示されない場合は、まず Visual Studio の **Windows Workflow Foundation** コンポーネントをインストールします。 詳細については、「 [Install Windows Workflow Foundation](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation)」を参照してください。

1. ダイアログボックスの下部にある [ **名前** ] ボックスに、項目の名前を入力します。

1. [ **追加** ] を選択して、プロジェクトに項目を追加します。

## <a name="see-also"></a>関連項目

- [ワークフロープロジェクトの作成](../workflow-designer/creating-a-workflow-project.md)
