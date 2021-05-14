---
title: .NET のコード分析を手動で実行する方法
ms.date: 09/02/2020
description: Visual Studio 2019 バージョン 16.5 以降のバージョンでコード分析を手動で実行する方法について説明します。 C# または Visual Basic コードで Roslyn アナライザーを実行する方法を示します。
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- code analysis, running
- run code analysis
ms.assetid: 5086d228-f92e-4515-9708-c5b89b9e9a03
author: mikadumont
ms.author: midumont
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 997fc6f6ecb8ffbd8c48e2352dcc9ae2f6092211
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860023"
---
# <a name="run-code-analysis-manually-for-net"></a>.NET のコード分析を手動で実行する
既定では、.NET Compiler Platform ("Roslyn") アナライザーは、ライブ分析時およびビルド時に、入力された C# または Visual Basic コードを分析します。 そのため、通常はコード分析を手動でトリガーする必要はありません。 ただし、コード分析を手動でトリガーする必要があるシナリオもあります。

> [!NOTE]
> コード分析を手動で実行するには、Visual Studio 2019 バージョン 16.5 以降が必要です。

- 既定では、ライブ コード分析でアナライザーの実行対象となるのは、Visual Studio で開いているファイルだけです。 しかし、特定のプロジェクトまたはソリューション内のすべてのファイルについて、コード分析の警告を表示したい場合があります。 その場合は、プロジェクトまたはソリューションに対してコード分析を 1 回トリガーできます。 または、継続的なライブ コード分析を有効にして、ソリューション全体に対して実行することもできます。 詳細については、「[方法:方法: マネージド コードのライブ コード分析スコープを構成する](./configure-live-code-analysis-scope-managed-code.md)」を参照してください。
- 継続的なライブ分析またはビルド時分析よりも、オンデマンドのコード分析実行ワークフローの方が望ましい場合もあります。 その場合は、ライブ分析時やビルド時のアナライザーの実行を無効にすることができます。 分析を無効にする方法については、[ソース コード分析を無効にする方法](disable-code-analysis.md)に関する記事をご覧ください。 その後、プロジェクトまたはソリューションに対してコード分析を手動で 1 回トリガーできます。

### <a name="run-code-analysis-manually"></a>手動でのコード分析の実行

1. **ソリューション エクスプローラー** でプロジェクトを選択します。

2. **[分析]** メニューの **[<*プロジェクト名*> に対してコード分析を実行]** を選択します。

コード分析は、バックグラウンドで実行が開始されます。 Visual Studio のステータス バーの左下隅に、 **[\<project> のコード分析を実行しています...]** というメッセージが表示されます。 コード分析が完了すると、ステータス メッセージが **[\<project> のコード分析が完了しました]** に変わります。 エラー一覧は、すべてのコード分析診断ですぐに更新されます。
