---
title: レガシ コード分析を無効にする
ms.date: 10/04/2019
description: Visual Studio でバイナリ コード分析をオンまたはオフにする方法について説明します。 マネージド コード プロジェクトでこの機能を構成する方法を示します。
ms.custom: SEO-VS-2020
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.openlocfilehash: c10aa602c2c9af3c51812073d62d5bd9bff06664
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860075"
---
# <a name="how-to-enable-and-disable-binary-code-analysis-for-managed-code"></a>方法: マネージド コードのバイナリ コード分析を有効または無効にする

マネージド コード プロジェクトの各ビルドの後で実行されるように、レガシ コード分析 (バイナリ分析) を構成できます。 また、デバッグやリリースなど、ビルド構成ごとに異なる設定を使用することもできます。

> [!NOTE]
> .NET Core アプリや .NET Standard アプリなど、新しいプロジェクトの種類にはレガシ分析を使用できません。 これらのプロジェクトのコードを分析するには、ライブ時とビルド時のどちらについても、[.NET Compiler Platform ベースのコード アナライザー](roslyn-analyzers-overview.md)を使用します。 これらのプロジェクトでソース コード分析を無効にする方法については、[ソース コード分析を無効にする方法](disable-code-analysis.md)に関する記事を参照してください。

レガシ コード分析を有効または無効にするには

1. **ソリューション エクスプローラー** でプロジェクトを長押しし (または右クリックし)、 **[プロパティ]** を選択します。

2. プロジェクトのプロパティ ダイアログ ボックスで、 **[コード分析]** タブに移動します。

3. **[構成]** でビルドの種類を指定し、 **[プラットフォーム]** でターゲット プラットフォームを指定します。 (.NET Core または .NET Standard 以外のプロジェクトのみ。)

::: moniker range="vs-2017"

4. 自動コード分析を有効または無効にするには、 **[ビルド時のコード分析の有効化]** チェック ボックスをオンまたはオフにします。

::: moniker-end

::: moniker range=">=vs-2019"

4. 自動コード分析を有効または無効にするには、 **[バイナリ アナライザー]** セクションの **[ビルド時に実行]** チェック ボックスをオンまたはオフにします。

   ![Visual Studio のビルド オプションでバイナリ コード分析を実行する](media/run-on-build-binary-analyzers.png)

::: moniker-end

> [!NOTE]
> ビルド時のバイナリ コード分析を無効にしても、[.NET Compiler Platform ベースのコード アナライザー](roslyn-analyzers-overview.md)には影響しません。それらを NuGet パッケージとしてインストールした場合は、ビルド時に常に実行されます。 これらのアナライザーから分析を無効にする方法については、[ソース コード分析を無効にする方法](disable-code-analysis.md)に関する記事を参照してください。
