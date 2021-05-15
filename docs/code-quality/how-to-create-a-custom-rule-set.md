---
title: カスタム コード分析ルール セットを作成する
ms.date: 11/02/2018
description: Visual Studio でコード分析ルール セットをカスタマイズする方法について説明します。 新しいセットを最初から作成する方法と既存のセットから作成する方法を示します。 ルールの優先順位を理解します。
ms.custom: SEO-VS-2020
ms.topic: how-to
f1_keywords:
- vs.codeanalysis.addremoverulesets
helpviewer_keywords:
- rule sets
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: dda89e9822e361438346300a2f60c05bcfd64d6f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860153"
---
# <a name="customize-a-rule-set"></a>ルール セットをカスタマイズする

コード分析でプロジェクトの特定のニーズを満たすために、カスタム ルール セットを作成できます。

## <a name="create-a-custom-rule-set-from-an-existing-rule-set"></a>既存のルール セットからカスタム ルール セットを作成する

カスタム ルール セットを作成するには、**ルール セット エディター** で組み込みのルール セットを開きます。 そこから、特定のルールを追加または削除したり、ルールに違反したときに実行されるアクション (警告やエラーの表示など) を変更したりできます。

1. **ソリューション エクスプローラー** でプロジェクトを右クリックし、 **[プロパティ]** を選択します。

2. **[プロパティ]** ページで **[コード分析]** タブを選択します。

::: moniker range="vs-2017"

3. **[この規則セットを実行]** ドロップダウン リストで、次のいずれかを行います。

::: moniker-end

::: moniker range=">=vs-2019"

3. **[アクティブな規則]** ドロップダウン リストで、次のいずれかを行います。

::: moniker-end

   - カスタマイズするルール セットを選択します。

     \- または

   - **\<Browse>** を選択して、一覧にない既存のルール セットを指定します。

4. **[開く]** を選択して、ルール セット エディターでルールを表示します。

> [!NOTE]
> .NET Core または .NET Standard プロジェクトがある場合、プロジェクトのプロパティの **[コード分析]** タブで同じオプションがサポートされていないため、プロセスが少し異なります。 手順に従って、[定義済みのルール セットをプロジェクトにコピーし、アクティブなルール セットとして設定](/dotnet/fundamentals/code-analysis/code-quality-rule-options)します。 ルール セットをコピーしたら、**ソリューション エクスプローラー** からそれを開いて、[Visual Studio のルール セット エディターで編集](working-in-the-code-analysis-rule-set-editor.md)できます。

## <a name="create-a-new-rule-set"></a>新しいルール セットを作成する

新しいルール セット ファイルは、 **[新しいファイル]** ダイアログから作成できます。

1. **[ファイル]**  >  **[新規作成]**  >  **[ファイル]** の順に選択するか、**Ctrl** + **N** キーを押します。

2. **[新しいファイル]** ダイアログ ボックスで、左側の **[全般]** カテゴリを選択し、 **[コード分析規則セット]** を選択します。

3. **[Open]** を選択します。

   ルール セット エディターに新しい *.ruleset* ファイルが開きます。

## <a name="create-a-custom-rule-set-from-multiple-rule-sets"></a>複数のルール セットからカスタム ルール セットを作成する

> [!NOTE]
> 次の手順は、 **[コード分析]** プロパティ タブの同じ機能がサポートされていない .NET Core または .NET Standard プロジェクトには適用されません。

1. **ソリューション エクスプローラー** でプロジェクトを右クリックし、 **[プロパティ]** を選択します。

2. **[プロパティ]** ページで **[コード分析]** タブを選択します。

::: moniker range="vs-2017"

3. **[この規則セットを実行]** から **\<Choose multiple rule sets>** を選択します。

::: moniker-end

::: moniker range=">=vs-2019"

3. **[アクティブな規則]** から **\<Choose multiple rule sets>** を選択します。

::: moniker-end

4. **[規則セットの追加と削除]** ダイアログ ボックスで、新しいルール セットに含めるルール セットを選択します。

   ![[規則セットの追加と削除] ダイアログ ボックス](media/add-remove-rule-sets.png)

5. **[名前を付けて保存]** を選択し、 *.ruleset* ファイルの名前を入力して、 **[保存]** を選択します。

   **[この規則セットを実行]** の一覧で、新しいルール セットが選択されます。

6. **[開く]** を選択して、ルール セット エディターで新しいルール セットを開きます。

## <a name="rule-precedence"></a>ルールの優先順位

- ルール セットに重大度が異なる同じルールが 2 回以上示されていると、コンパイラはエラーを生成します。 次に例を示します。

   ```xml
   <RuleSet Name="Rules for ClassLibrary21" Description="Code analysis rules for ClassLibrary21.csproj." ToolsVersion="15.0">
     <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
       <Rule Id="CA1021" Action="Warning" />
       <Rule Id="CA1021" Action="Error" />
     </Rules>
   </RuleSet>
   ```

- ルール セットに "*同じ*" 重大度の同じルールが 2 回以上示されている場合、 **[エラー一覧]** に次の警告が表示されることがあります。

   **CA0063: 規則セット ファイル'\[your].ruleset' か、またはその依存先の規則セット ファイルの 1 つを読み込めませんでした。ファイルが規則セットのスキーマに準拠していません。**

- **Include** タグを使用してルール セットに子ルール セットが含まれており、子と親のルール セットに重大度が異なる同じルールが示されている場合は、親ルール セットの重大度が優先されます。 次に例を示します。

   ```xml
   <!-- Parent rule set -->
   <?xml version="1.0" encoding="utf-8"?>
   <RuleSet Name="Rules for ClassLibrary21" Description="Code analysis rules for ClassLibrary21.csproj." ToolsVersion="15.0">
     <Include Path="classlibrary_child.ruleset" Action="Default" />
     <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
       <Rule Id="CA1021" Action="Warning" /> <!-- Overrides CA1021 severity from child rule set -->
     </Rules>
   </RuleSet>

   <!-- Child rule set -->
   <?xml version="1.0" encoding="utf-8"?>
   <RuleSet Name="Rules from child" Description="Code analysis rules from child." ToolsVersion="15.0">
     <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
       <Rule Id="CA1021" Action="Error" />
     </Rules>
   </RuleSet>
   ```

## <a name="name-and-description"></a>名前と説明

エディターで開いているルール セットの表示名を変更するには、メニュー バーで **[表示]**  >  **[プロパティ ウィンドウ]** の順に選択して、 **[プロパティ]** ウィンドウを開きます。 **[名前]** ボックスに表示名を入力します。 また、ルール セットの説明を入力することもできます。

## <a name="next-steps"></a>次のステップ

ルール セットを用意できたので、次に、ルールを追加または削除したり、ルール違反の重大度を変更したりして、ルールをカスタマイズします。

> [!div class="nextstepaction"]
> [ルール セット エディターでルールを変更する](../code-quality/working-in-the-code-analysis-rule-set-editor.md)

## <a name="see-also"></a>関連項目

- [方法: マネージド コード プロジェクトのコード分析を構成する](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)
- [コード分析規則セットの参照](../code-quality/rule-set-reference.md)