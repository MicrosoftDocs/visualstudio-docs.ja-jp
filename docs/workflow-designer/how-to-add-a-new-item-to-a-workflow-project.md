---
title: 'ワークフロー デザイナー: ワークフロー プロジェクトに新しい項目を追加する'
description: ワークフロー プロジェクトを作成した後、ワークフロー アクティビティ、デザイナー、およびその他の一般的な Visual Studio 項目をプロジェクトに追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 06/25/2018
ms.topic: how-to
ms.assetid: 5c6180ca-af10-4513-b0cb-7d478fd84eab
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e0cc4b24462583a5f704f47c16e6e8d30456512b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99938461"
---
# <a name="how-to-add-a-new-item-to-a-workflow-project"></a>方法: ワークフロー プロジェクトに新しい項目を追加する

ワークフロー プロジェクトを作成した後、ワークフロー アクティビティ、デザイナー、およびその他の一般的な Visual Studio 項目をプロジェクトに追加できます。

次の表は、ワークフロー プロジェクトに追加できる Windows Workflow Foundation (WF) 項目の一覧です。

| 名前 | 説明 |
|-| - |
| アクティビティ | 他のアクティビティで構成されるアクティビティ。 この項目を選択すると、新しいプロジェクト用の **[アクティビティ ライブラリ]** テンプレートを選択した場合に取得されるものと同じ XAML ファイルがプロジェクトに追加されます。 この手順の詳細については、「[ワークフロー プロジェクトを作成する](creating-a-workflow-project.md)」を参照してください。 |
| アクティビティ デザイナー | アクティビティのデザイン時の操作をカスタマイズするデザイナー。 この項目を選択すると、新しいプロジェクト用の **[アクティビティ デザイナー ライブラリ]** テンプレートを選択した場合に取得されるものと同じファイルがプロジェクトに追加されます。 |
| Code アクティビティ | コードに記述される実行ロジックを含むアクティビティ。 <xref:System.Activities.CodeActivity.Execute%2A> メソッドのオーバーライドを含むソース コード ファイルは既に自動的に生成されています。 |
| WCF ワークフロー サービス | ワークフロー アクティビティを使用して作成された [!INCLUDE[indigo2](../workflow-designer/includes/indigo2_md.md)] サービス。 この項目を選択すると、新しいプロジェクト用の **[WCF ワークフロー サービス アプリケーション]** テンプレートを選択した場合に取得されるものと同じファイルがプロジェクトに追加されます。 この手順の詳細については、「[方法: WCF ワークフロー サービス アプリケーションを作成する](creating-a-workflow-project.md)」を参照してください。 |

## <a name="to-add-a-new-item-to-a-workflow-project"></a>ワークフロー プロジェクトに新しい項目を追加するには

1. **[プロジェクト]** メニューで、 **[新しい項目の追加]** を選択します。

   **[新しい項目の追加]** ダイアログ ボックスが開きます。

1. 左側のペインで、 **[ワークフロー]** カテゴリを選択し、ワークフロー項目テンプレートを選択します。

   > [!NOTE]
   > **[ワークフロー]** カテゴリが表示されない場合は、先に Visual Studio の **Windows Workflow Foundation** コンポーネントをインストールします。 詳細については、「[Windows Workflow Foundation をインストールする](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation)」を参照してください。

1. ダイアログ ボックスの下部にある **[名前]** ボックスに、項目の適切な名前を入力します。

1. **[追加]** を選択して、プロジェクトに項目を追加します。

## <a name="see-also"></a>関連項目

- [ワークフロー プロジェクトを作成する](../workflow-designer/creating-a-workflow-project.md)
