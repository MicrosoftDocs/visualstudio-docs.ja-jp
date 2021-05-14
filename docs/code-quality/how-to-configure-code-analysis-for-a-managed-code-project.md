---
title: コード分析を構成する
ms.date: 04/04/2018
description: Visual Studio のレガシ コード分析で使用されるルール セットを構成する方法について説明します。 ソリューション内の 1 つまたは複数のプロジェクトにルール セットを適用する方法を示します。
ms.custom: SEO-VS-2020
ms.topic: how-to
f1_keywords:
- vs.codeanalysis.propertypages.csvb
- vs.codeanalysis.propertypages.solution
- vs.codeanalysis.propertypages.asp
dev_langs:
- CSharp
- VB
- FSharp
helpviewer_keywords:
- code analysis, selecting rule sets
- code analysis, rule sets
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 8b76678b1e5c0f53502e24f8baee87ede3bd3ef6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860179"
---
# <a name="how-to-configure-legacy-analysis-for-managed-code"></a>方法: マネージド コードのレガシ分析を構成する

Visual Studio では、マネージド コード プロジェクトに適用するコード分析[ルール セット](../code-quality/rule-set-reference.md)を一覧から選択できます。 既定では、**Microsoft 最小推奨規則** ルール セットが選択されていますが、必要に応じて別のルール セットを適用できます。 ルール セットは、ソリューション内の 1 つまたは複数のプロジェクトに適用できます。

> [!NOTE]
> この記事は、[.NET Compiler Platform ベースのコード アナライザー](use-roslyn-analyzers.md)ではなく、レガシ分析に適用されます。

## <a name="configure-a-rule-set-for-a-net-framework-project"></a>.NET Framework プロジェクトのルール セットを構成する

1. プロジェクトのプロパティ ページで、 **[コード分析]** タブを開きます。 この操作は次のいずれかの方法で行うことができます。

   - **ソリューション エクスプローラー** でプロジェクトを選択します。 メニュー バーで、 **[分析]**  >  **[コード分析の設定]**  >  **[\<projectname>]** の順に選択します。

   - **ソリューション エクスプローラー** で、プロジェクトを右クリックして **[プロパティ]** を選択し、 **[コード分析]** タブを選択します。

2. **[構成]** および **[プラットフォーム]** の一覧で、ビルド構成とターゲット プラットフォームを選択します。

::: moniker range="vs-2017"

3. 選択した構成を使用して、プロジェクトをビルドするたびにコード分析を実行するには、 **[ビルド時のコード分析の有効化]** を選択します。 **[分析]**  >  **[コード分析の実行]**  >  **[\<projectname> でコード分析を実行]** を選択して、コード分析を手動で実行することもできます。

::: moniker-end

::: moniker range=">=vs-2019"

3. 選択した構成を使用して、プロジェクトをビルドするたびにコード分析を実行するには、 **[バイナリ アナライザー]** セクションの **[ビルド時に実行]** を選択します。 レガシ コード分析を手動で実行することもできます。詳細については、「[方法: マネージド コードのレガシ コード分析を手動で実行する](how-to-run-legacy-code-analysis-manually-for-managed-code.md)」をご覧ください。

::: moniker-end

4. 生成されたコードの警告を表示するには、 **[生成されたコードの結果を表示しない]** チェック ボックスをオフにします。

    > [!NOTE]
    > コード分析のエラーおよび警告がフォームやテンプレートで表示される場合、このオプションを使用しても、生成されたコードからこのエラーおよび警告の出力は抑制されません。 フォームまたはテンプレートのソース コードは、表示することも保持することもでき、上書きされることはありません。

::: moniker range="vs-2017"

5. **[この規則セットを実行]** の一覧で、次のいずれかを行います。

::: moniker-end

::: moniker range=">=vs-2019"

5. **[アクティブな規則]** の一覧で、次のいずれかを行います。

::: moniker-end

   - 使用するルール セットを選択します。

   - **\<Browse>** を選択して、一覧にない既存のカスタム ルール セットを見つけます。

   - [カスタム ルール セット](../code-quality/how-to-create-a-custom-rule-set.md)を定義します。

## <a name="specify-rule-sets-for-multiple-projects-in-a-solution"></a>ソリューション内の複数のプロジェクトのルール セットを指定する

既定では、ソリューションのすべてのマネージド プロジェクトに "*Microsoft 最小推奨規則*" コード分析ルール セットが割り当てられます。 ソリューションの **[プロパティ]** ダイアログ ボックスで、ソリューションのプロジェクトに割り当てられるルール セットを変更できます。

1. Visual Studio でソリューションを開きます。

2. **[分析]** メニューの **[ソリューションのコード分析を構成する]** を選択します。

3. 必要に応じて、 **[共通プロパティ]** を展開し、 **[コード分析設定]** を選択します。

4. 1 つ以上のプロジェクトに対してルール セットを指定できます。

    - 個々のプロジェクトのルール セットを指定するには、プロジェクト名を選択します。

    - 複数のプロジェクトのルール セットを指定するには、**Ctrl** キーを押しながらプロジェクト名を選択します。

    - ソリューション内のすべてのプロジェクトを指定するには、**Shift** キーを押しながらプロジェクトの一覧を選択します。

5. プロジェクトの **[ルール セット]** フィールドを選択し、適用するルール セットの名前を選択します。

## <a name="see-also"></a>関連項目

- [コード分析規則セットの参照](../code-quality/rule-set-reference.md)
