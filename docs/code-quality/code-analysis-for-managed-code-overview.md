---
title: マネージド コードのコード分析
ms.date: 08/27/2020
description: Visual Studio での .NET Compiler Platform ベースのコード分析について説明します。 これらのアナライザーがマネージド アセンブリの FxCop スタティック分析に取って代わる理由を理解します。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- managed code, code analysis
author: mikadumont
ms.author: midumont
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 542747f650888b384a9f9c4910b0d9caea93e948
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860569"
---
# <a name="overview-of-code-analysis-for-net-in-visual-studio"></a>Visual Studio での .NET のコード分析の概要

Visual Studio では、マネージド コードのコード分析を 2 とおりの方法で実行できます。[レガシ分析](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md) (マネージド アセンブリの FxCop 静的分析とも呼ばれます) を使用する方法と、最新の [.NET Compiler Platform ベースのコード アナライザー](../code-quality/roslyn-analyzers-overview.md)を使用する方法です。 入力直後にコードを分析する .NET Compiler Platform ベースのコード アナライザーが、コンパイル後のコードのみを分析するレガシ FxCop 静的コード分析に取って代わります。
