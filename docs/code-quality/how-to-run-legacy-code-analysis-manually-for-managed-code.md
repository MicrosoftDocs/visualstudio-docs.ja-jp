---
title: レガシ コード分析を手動で実行する (.NET)
description: ソース コードに存在する可能性がある欠陥を検出する方法について説明します。 Visual Studio でマネージド コードについて手動でレガシ コード分析を実行する方法に関するページを参照してください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- code analysis, running
ms.assetid: 5086d228-f92e-4515-9708-c5b89b9e9a03
author: Mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: f214ac47ad3d831432b91652c5bbe3249ce5f1c5
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102223486"
---
# <a name="how-to-run-legacy-code-analysis-manually-for-managed-code"></a>方法: マネージド コードについて手動でレガシ コード分析を実行する

コード分析ツールでは、ソース コードに存在する可能性がある欠陥に関する情報を提供します。 コード プロジェクトの各ビルドでコード分析を自動的に実行することも、コード分析を手動で実行することもできます。 コード分析の実行時にチェックされる規則は、プロジェクトのプロパティ ページの [コード分析] ページで指定します。 詳細については、「[方法: マネージド コード プロジェクトのコード分析を構成する](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)」を参照してください。

## <a name="to-run-code-analysis-manually"></a>手動でコード分析を実行するには

1. Visual Studio 2019 バージョン 16.5 以降を使用している場合は、Visual Studio を起動する前に、コマンド プロンプトで次のコマンドを実行します。

```
setx EnableLegacyCodeAnalysis true
```

2. **ソリューション エクスプローラー** でプロジェクトをクリックします。

3. **[分析]** メニューの **[<*プロジェクト名*> に対してコード分析を実行]** をクリックします。
