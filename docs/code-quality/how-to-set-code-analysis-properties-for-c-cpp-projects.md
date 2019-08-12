---
title: '方法: C/C++ プロジェクトのコード分析プロパティを設定する'
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.propertypages.native
- VC.Project.VCCLCompilerTool.EnablePrefast
- VC.Project.VCFxCopTool.EnablePREfast
- VC.Project.VCFxCopTool.IgnoreGeneratedCode
helpviewer_keywords:
- properties, C/C++ Code Analysis
- properties, Code Analysis
- code analysis properties
- C/C++ code analysis properties
ms.assetid: 7af52097-6d44-4785-9b9f-43b7a7d447d7
author: mikeblome
ms.author: mblome
manager: wpickett
ms.workload:
- cplusplus
ms.openlocfilehash: 72866618383382389ad5e5706ae2a0999c89c346
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68923985"
---
# <a name="how-to-set-code-analysis-properties-for-cc-projects"></a>方法: C/C++ プロジェクトのコード分析プロパティを設定する
コード分析ツールがプロジェクトの各構成でコードを分析するために使用する規則を構成できます。 さらに、サードパーティのツールによって生成され、プロジェクトに追加されたコードからの警告を表示しないようにコード分析を指示することもできます。

## <a name="code-analysis-property-page"></a>[コード分析] プロパティページ
[**コード分析**] プロパティページには、プロジェクトのすべてのコード分析の構成設定が含まれています。 **ソリューションエクスプローラー**のプロジェクトの [コード分析] プロパティページを開くには、プロジェクトを右クリックし、[**プロパティ**] をクリックします。 次に、[**構成プロパティ**] を展開し、[**コード分析**] タブを選択します。

## <a name="project-configuration-and-platform"></a>プロジェクトの構成とプラットフォーム
[**構成**リスト] と [**プラットフォーム**] ボックスの一覧では、さまざまなコード分析設定をプロジェクトの構成とプラットフォームの組み合わせごとに適用できます。 たとえば、デバッグビルドのプロジェクトに1つのルールセットを適用し、リリースビルド用に別のセットを適用するようにコード分析を指示することができます。

## <a name="enabling-code-analysis"></a>コード分析の有効化
**[C/C++ビルド時にコード分析を有効**にする] を選択すると、プロジェクトのコード分析を有効にするかどうかを決定できます。 たとえば、**構成**リストと組み合わせて、デバッグビルドのコード分析を無効にし、リリースビルドに対して有効にすることができます。

プロジェクトにマネージコードが含まれている場合は、[**ビルドでコード分析を有効**にする] を選択して、コード分析を有効または無効にするかどうかを決定できます。

コード分析は、コードの品質を向上させ、一般的な落とし穴を回避できるように設計されています。 そのため、コード分析を無効にするかどうかを慎重に検討してください。 通常は、プロジェクトに適用しないルールセットまたは個々のルールを無効にすることをお勧めします。

## <a name="generated-code"></a>生成されたコード
開発者は、アプリケーションの迅速な開発に役立つツールを頻繁に使用します。 これらのツールは、プロジェクトに追加されたコードを生成できます。 生成されたコードでコード分析によって検出された規則違反を確認することができます。 ただし、コードを管理したくない場合は、表示したくない場合があります。

**[全般**プロパティ] ページの [**生成されたコードの結果を**表示しない] チェックボックスをオンにすると、サードパーティツールによって生成されたマネージコードからコード分析の警告を表示するかどうかを選択できます。

## <a name="rule-sets"></a>規則セット
プロジェクトにマネージコードが含まれている場合は、[**この規則セットを実行**する] の一覧から規則セットを選択して、コード分析で適用する規則を選択できます。

## <a name="see-also"></a>関連項目

- [マネージド コードの品質の分析](../code-quality/code-analysis-for-managed-code-overview.md)
- [C/C++ コードの警告に対応するコードの分析](../code-quality/code-analysis-for-c-cpp-warnings.md)