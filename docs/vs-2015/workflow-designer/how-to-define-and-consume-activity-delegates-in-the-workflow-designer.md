---
title: '方法: ワークフローデザイナーでアクティビティデリゲートを定義および使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: c68e42ad-3ec0-4c2d-b104-fe36c6d83b5e
caps.latest.revision: 3
author: steved0x
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 26ba92a2ba7aa6eed471383c875104549e896804
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72603851"
---
# <a name="how-to-define-and-consume-activity-delegates-in-the-workflow-designer"></a>ワークフロー デザイナーでアクティビティ デリゲートを定義および使用する方法
[!INCLUDE[net_v45](../includes/net-v45-md.md)] には、すぐに使用できる <xref:System.Activities.Statements.InvokeDelegate> アクティビティの新しいデザイナーが用意されています。 このデザイナーを使用すると、<xref:System.Activities.ActivityDelegate> や <xref:System.Activities.ActivityAction> など、<xref:System.Activities.ActivityFunc%601> から派生するアクティビティにデリゲートを割り当てることができます。

### <a name="define-an-activity-delegate"></a>アクティビティ デリゲートの定義

1. @No__t_0 で、 **[ファイル]** 、 **[新規作成]** 、 **[プロジェクト]** の順番に選択します。 左側の **[ワークフロー]** ノードを選択し、右側の **[ワークフローコンソールアプリケーション]** テンプレートを選択します。 必要に応じてプロジェクトに名前を指定し、[ **Ok]** をクリックします。

2. **ソリューションエクスプローラー**でプロジェクトを右クリックし、 **[追加]** 、 **[新しい項目]** の順に選択します。 左側の **[ワークフロー]** ノードを選択し、右側の**アクティビティ**テンプレートを選択します。 新しいアクティビティに「 **Myforeach .Xaml** 」という名前を指定し、[ **Ok]** をクリックします。 ワークフロー デザイナーでアクティビティが開かれます。

3. ワークフローデザイナーで、 **[引数]** タブをクリックします。

4. **[引数の作成]** をクリックします。 新しい引数の**項目**に名前を指定します。

5. **[引数の型]** 列で、 **[[T] の配列**] を選択します。

6. 型ブラウザーで、 **[オブジェクト]** を選択します。 [ **Ok]** をクリックします。

7. **[引数の作成]** をもう一度クリックします。 新しい引数の**本体**に名前を指定します。 新しい引数の **[方向]** 列で、 **[プロパティ]** を選択します。

8. 引数の型 列で、**型の参照** を選択します。

9. 型ブラウザーで、 **[型名]** フィールドに「 **activityaction** 」と入力します。 ツリービューで [ **Activityaction \<T >** ] を選択します。 表示されるドロップダウンリストで **[オブジェクト]** を選択して、引数に **\<Object > 型 activityaction**を割り当てます。

10. ツールボックスの **[制御フロー]** セクションから <xref:System.Activities.Statements.While> アクティビティをデザイナー画面にドラッグします。

11. @No__t_0 アクティビティを選択し、 **[変数]** タブを選択します。

12. **[変数の作成]** を選択します。 新しい変数の**インデックス**に名前を付けます。

13. **[変数の型]** 列で **[Int32]** を選択します。 [**スコープ** **] はそのままにし**、**既定**の列は空白のままにします。

14. @No__t_1 アクティビティの**Condition**プロパティを**index < Items. Length;** に設定します。

15. ツールボックスの **[プリミティブ]** セクションから <xref:System.Activities.Statements.While> アクティビティの**本文**に <xref:System.Activities.Statements.InvokeDelegate> アクティビティをドラッグします。

16. デリゲート ドロップダウンで **本文** を選択します。

17. @No__t_1 アクティビティの**プロパティ**グリッドで、[. **.** ] をクリックします。 **[デリゲート引数]** プロパティのボタン。

18. Argument という名前の引数の**値**列に「 **Items [Index]** **」と入力**します。 **[Ok]** をクリックして、 **[DelegateArguments]** ダイアログボックスを閉じます。

19. <xref:System.Activities.Statements.Assign> アクティビティを <xref:System.Activities.Statements.InvokeDelegate> アクティビティの下の水平線にドラッグします。 @No__t_0 アクティビティが作成され、<xref:System.Activities.Statements.Sequence> アクティビティが自動的に作成され、 **Myforeach**アクティビティの**Body**セクションに2つのアクティビティが含まれます。 **Body**セクションには1つのアクティビティのみを含めることができるため、シーケンスが必要です。 新しい <xref:System.Activities.Statements.Sequence> アクティビティの自動作成は [!INCLUDE[net_v45](../includes/net-v45-md.md)] の新機能です。

20. @No__t_1 アクティビティの**To**プロパティを**index**に設定します。 **Assign**アクティビティの**Value**プロパティを**index + 1**に設定します。

    カスタム**Myforeach**アクティビティは、**項目**コレクションを通じて渡された値ごとに任意のアクティビティを1回呼び出します。コレクション内の値は、アクティビティの入力として使用されます。

### <a name="use-the-custom-activity-in-a-workflow"></a>ワーク フローでのカスタム アクティビティの使用

1. **Ctrl + Shift + B**キーを押してプロジェクトをビルドします。

2. **ソリューションエクスプローラー**で、デザイナーで**workflow1.xaml**を開きます。

3. ツールボックス から  **Myforeach** アクティビティをデザイナー画面にドラッグします。 アクティビティは、プロジェクトと同じ名前のツールボックスのセクションにあります。

4. **Myforeach**アクティビティの**Items**プロパティを**新しいオブジェクト [] {1, "abc"}** に設定します。

5. ツールボックス の **プリミティブ** セクションから、 **myforeach**アクティビティの **Delegate: Body** セクションに <xref:System.Activities.Statements.WriteLine> アクティビティをドラッグします。

6. @No__t_1 アクティビティの**Text**プロパティを**Argument. ToString ()** に設定します。

   ワーク フローの実行時に、コンソールには次のように表示されます。

   **1** 
   **abc**