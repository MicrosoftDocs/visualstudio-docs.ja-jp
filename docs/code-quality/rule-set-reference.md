---
title: コード分析規則セットの参照
ms.date: 04/04/2018
description: Visual Studio レガシ コード分析の組み込みのルール セットについて説明します。 ルール セットのリソースを示します。 カスタマイズされたルール セットでこれらのセットを使用する方法を確認します。
ms.custom: SEO-VS-2020
ms.topic: reference
helpviewer_keywords:
- code analysis, rule sets reference
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: cead2d51a13ce4ec137edcd55c7db91d84b04f7f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99867777"
---
# <a name="code-analysis-rule-set-reference"></a>コード分析規則セットの参照

Visual Studio でマネージド コード プロジェクトのレガシ分析を構成する場合、組み込みの "*ルール セット*" の一覧から選択できます。 一部のルールは、複数の組み込みのルール セットに含まれています。たとえば、"基本正確性規則" ルール セットには、"マネージド推奨規則" ルール セットのルールが含まれています。

> [!NOTE]
> このセクションのルール セットは、レガシ分析に関連しています。 コード アナライザー パッケージで使用できるルール セットについては、[コード アナライザーでのルール セットの使用](/dotnet/fundamentals/code-analysis/code-quality-rule-options)に関する記事をご覧ください。

これらの組み込みのルール セットのいずれかを使用することも、プロジェクトの要件に合わせて[ルール セットをカスタマイズする](../code-quality/how-to-create-a-custom-rule-set.md)こともできます。 同じルールが含まれた複数のルール セットをカスタム ルール セットに含めた場合、そのルールはカスタム ルール セットに 1 回だけ表示されます。

このセクションのトピックでは、組み込みのルール セットとそれらに含まれるルール (または警告) について説明します。

| [ルール セット] | 含まれるルール |
| - | - |
| [すべての規則](all-rules-rule-set.md) | 使用可能なすべてのマネージド ルールと C++ ルールが含まれています |
| [基本正確性規則](basic-correctness-rules-rule-set-for-managed-code.md) | マネージド推奨規則に加えて、ロジック エラーとフレームワークの使用に関するルールが含まれています |
| [拡張正確性規則](extended-correctness-rules-rule-set-for-managed-code.md) | 基本正確性規則 (マネージド推奨規則を含む) に加えて、ロジック エラーとフレームワークの使用に関するその他のルールが含まれています |
| [基本デザイン ガイドライン規則](basic-design-guideline-rules-rule-set-for-managed-code.md) | マネージド推奨規則に加えて、コードを読みやすく、わかりやすくし、簡単にメンテナンスできるようにするためのルールが含まれています |
| [拡張デザイン ガイドライン規則](extended-design-guidelines-rules-rule-set-for-managed-code.md) | 基本デザイン ガイドライン規則 (マネージド推奨規則を含む) に加えて、名前付けに重点を置いた保守容易性のルールが含まれています |
| [グローバリゼーション規則](globalization-rules-rule-set-for-managed-code.md) | グローバリゼーションの問題に関するルールが含まれています |
| [マネージド最小規則](managed-minimum-rules-rule-set-for-managed-code.md) | マネージド コードの重大な問題に関する 4 つのルールが含まれています |
| [マネージド推奨規則](managed-recommended-rules-rule-set-for-managed-code.md) | マネージド最小規則に加えて、マネージド コードの重大な問題に関するその他のルールが含まれています |
| [混合最小規則](mixed-minimum-rules-rule-set.md) | CLR の C++ コードの重大な問題に関するルールが含まれています |
| [混合推奨規則](mixed-recommended-rules-rule-set.md) | 混合最小規則に加えて、CLR の C++ コードの重大な問題に関するその他のルールが含まれています |
| [ネイティブ最小規則](native-minimum-rules-rule-set.md) | ネイティブ コードの重大な問題に関するルールが含まれています |
| [ネイティブ推奨規則](native-recommended-rules-rule-set.md) | ネイティブ最小規則に加えて、ネイティブ コードの重大な問題に関するその他のルールが含まれています |
| [セキュリティ規則](security-rules-rule-set-for-managed-code.md) | セキュリティの脆弱性を検出するためのルールが含まれています |