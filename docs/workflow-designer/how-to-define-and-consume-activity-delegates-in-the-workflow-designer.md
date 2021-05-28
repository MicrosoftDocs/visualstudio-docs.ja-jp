---
title: アクティビティ デリゲートの定義と使用
description: ワークフロー デザイナーで、.NET Framework 4.5 に、アクティビティ デリゲートを定義および使用するために使用できる InvokeDelegate アクティビティ用の独創的なデザイナーが含まれていることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: c68e42ad-3ec0-4c2d-b104-fe36c6d83b5e
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
author: TerryGLee
ms.openlocfilehash: 0ce9e59eec2cc9229a5f1104d79337b26115c92a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99971623"
---
# <a name="how-to-define-and-consume-activity-delegates-in-the-workflow-designer"></a>ワークフロー デザイナーでアクティビティ デリゲートを定義および使用する方法

.NET Framework 4.5 には、<xref:System.Activities.Statements.InvokeDelegate> アクティビティのための独創的なデザイナーが含まれています。 このデザイナーを使用すると、<xref:System.Activities.ActivityDelegate> や <xref:System.Activities.ActivityAction> など、<xref:System.Activities.ActivityFunc%601> から派生するアクティビティにデリゲートを割り当てることができます。

## <a name="define-an-activity-delegate"></a>アクティビティ デリゲートの定義

1. 新しい **ワークフロー コンソール アプリケーション** プロジェクトを作成します。

   > [!NOTE]
   > **[ワークフロー]** プロジェクト テンプレートが表示されない場合は、先に Visual Studio の **Windows Workflow Foundation** コンポーネントをインストールします。 詳細については、「[Windows Workflow Foundation をインストールする](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation)」を参照してください。

3. **ソリューション エクスプローラー** でプロジェクトを右クリックし、 **[追加]**  >  **[新しい項目]** を選択します。 **[ワークフロー]** カテゴリを選択し、 **[アクティビティ]** 項目テンプレートを選択します。 新しいアクティビティに「**MyForEach.xaml**」という名前を付け、 **[OK]** をクリックします。

   アクティビティがワークフロー デザイナーで開きます。

4. ワークフロー デザイナーで **[引数]** タブをクリックします。

5. [**Create Argument**] (引数の作成) をクリックします。 新しい引数に「**Items**」という名前を付けます。

6. **[引数の型]** 列で **[配列: [T]]** を選択します。

7. 型ブラウザーで **[オブジェクト]** を選択し、 **[OK]** を選択します。

8. もう一度 **[引数の作成]** をクリックします。 新しい引数に「**Body**」という名前を付けます。 新しい引数の **[方向]** 列で **[プロパティ]** を選択します。

9. [引数の型] 列で **[型の参照]** をクリックします。

10. 型ブラウザーで **[型の名前]** フィールドに「**ActivityAction**」と入力します。 ツリー ビューで **ActivityAction\<T>** を選択します。 表示されたドロップダウンで **[オブジェクト]** を選択し、**ActivityAction\<Object>** 型を引数に割り当てます。

11. <xref:System.Activities.Statements.While> アクティビティを、ツールボックスの **[制御フロー]** セクションからデザイナー画面にドラッグします。

12. <xref:System.Activities.Statements.While> アクティビティを選択し、 **[変数]** タブをクリックします。

13. **[変数の作成]** を選択します。 新しい変数に「**Index**」という名前を付けます。

14. **[変数の型]** 列で **[Int32]** を選択します。 **[スコープ]** を **[While]** のままにし、 **[既定]** 列を空欄のままにします。

15. <xref:System.Activities.Statements.While> アクティビティの **Condition** プロパティを **index < Items.Length;** に設定します。

16. <xref:System.Activities.Statements.InvokeDelegate> アクティビティを、ツールボックスの **[プリミティブ]** セクションから <xref:System.Activities.Statements.While> アクティビティの **Body** にドラッグします。

17. [デリゲート] ドロップダウンで **[Body]** を選択します。

18. <xref:System.Activities.Statements.InvokeDelegate> アクティビティの **[プロパティ]** グリッドで、 **[デリゲート引数]** プロパティの **[...]** ボタンをクリックします。

19. **Argument** という引数の **[値]** 列に「**Items[Index]** 」と入力します。 **[OK]** をクリックして **[DelegateArguments]** ダイアログ ボックスを閉じます。

20. <xref:System.Activities.Statements.Assign> アクティビティを <xref:System.Activities.Statements.InvokeDelegate> アクティビティの下の水平線にドラッグします。 <xref:System.Activities.Statements.Assign> アクティビティが作成されます。また、**MyForEach** アクティビティの **Body** セクションに 2 つのアクティビティを含めるように <xref:System.Activities.Statements.Sequence> アクティビティが自動的に作成されます。 **Body** セクションに含めることができるアクティビティは 1 つだけのため、シーケンスが必要になります。 新しい <xref:System.Activities.Statements.Sequence> アクティビティの自動作成は .NET Framework 4.5 の新機能です。

21. <xref:System.Activities.Statements.Assign> アクティビティの **To** プロパティを **index** に設定します。 **Assign** アクティビティの **Value** プロパティを **index+1** に設定します。

    カスタムの **MyForEach** アクティビティは、**Items** コレクションを通じて渡された値ごとに任意のアクティビティを 1 回呼び出し、コレクション内の値をアクティビティの入力として使用します。

## <a name="use-the-custom-activity-in-a-workflow"></a>ワーク フローでのカスタム アクティビティの使用

1. **Ctrl** + **Shift** + **B** キーを押して、プロジェクトをビルドします。

2. **ソリューション エクスプローラー** で、**Workflow1.xaml** をデザイナーで開きます。

3. **MyForEach** アクティビティをツールボックスからデザイナー画面にドラッグします。 アクティビティは、プロジェクトと同じ名前のツールボックスのセクションにあります。

4. **MyForEach** アクティビティの **Items** プロパティを **new Object[] {1, "abc"}** に設定します。

5. <xref:System.Activities.Statements.WriteLine> アクティビティを、ツールボックスの **[プリミティブ]** セクションから **MyForEach** アクティビティの **Delegate:Body** セクションにドラッグします。

6. <xref:System.Activities.Statements.WriteLine> アクティビティの **Text** プロパティを **Argument.ToString()** に設定します。

ワーク フローを実行すると、次の出力がコンソールに表示されます。

**1**
**abc**
