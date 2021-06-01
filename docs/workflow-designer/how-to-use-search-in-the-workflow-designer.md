---
title: ワークフロー デザイナーで検索を使用する方法
description: より大規模で複雑なワークフローを容易に作成できるように、ワークフロー デザイナーでキーワードを使用して項目を検索する方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: f42d3115-2ed2-4941-8f1e-92dac41c30fa
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6fb30d4846c24638f87989d2a7a716df06b0523b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894115"
---
# <a name="how-to-use-search-in-the-workflow-designer"></a>ワークフロー デザイナーで検索を使用する方法

より大規模で複雑なワークフローを容易に作成するため、ワークフロー デザイナー内でキーワードを使用して項目を検索できます。 デザイナーでは、置換はサポートされないことに注意してください。

## <a name="quick-find"></a>クイック検索

クイック検索はデザイナー内で次の項目を検索します。

- <xref:System.Activities.Activity> オブジェクト、<xref:System.Activities.Statements.FlowNode> オブジェクト、<xref:System.Activities.Statements.State> オブジェクト、遷移、およびその他のカスタム フロー制御項目のプロパティ。

- 変数

- 引数

- 式

### <a name="use-quick-find"></a>クイック検索を使用する

1. ワークフロー デザイナーを開いた状態で、**Ctrl + F** キーを押すか、 **[編集]**  >  **[検索と置換]**  >  **[クイック検索]** を選択します。

2. 検索用語を **[検索する文字列]** ボックスに入力し、 **[次を検索]** をクリックします。

3. 検索用語が現在のワークフローで検索されます。 アクティビティの表示名がデザイナーで見つかったことを示す画像を次に示します。

   ![ワークフロー デザイナーでの検索結果](../workflow-designer/media/designersearch.png)

## <a name="find-in-files"></a>フォルダーを指定して検索する

[フォルダーを指定して検索] を使用すると、XAML ファイルなどのワークフロー ファイル内で文字列が検索されます。

### <a name="use-find-in-files"></a>[フォルダーを指定して検索] を使用する

1. Visual Studio で、**Ctrl** + **Shift** + **F** キーを押すか、 **[編集]**  >  **[検索と置換]**  >  **[フォルダーを指定して検索]** を選択します。

2. 検索項目を **[検索する文字列]** ボックスに入力し、 **[すべて検索]** をクリックします。

3. 検索結果が **[検索結果]** ビューに表示されます。 結果の項目をダブルクリックすると、ワークフロー デザイナーで一致する項目が含まれるアクティビティに移動します。