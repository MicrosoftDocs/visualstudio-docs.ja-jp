---
title: Roslyn アナライザーの概要 | Microsoft Docs
description: これらのリソースを使用して、Visual Studio で Roslyn アナライザーを使い始めることができます。チュートリアルといくつかの例が含まれています。
ms.custom: SEO-VS-2020
ms.date: 04/02/2018
ms.topic: conceptual
ms.assetid: 367c2ec8-3059-46a5-9d1c-57bead0419e7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4579f148d2e27961fe1c579ffe3583e0e6be806c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057599"
---
# <a name="get-started-with-roslyn-analyzers"></a>Roslyn アナライザーの概要

Visual Studio のプロジェクト ベースのコード アナライザーを使用すると、API の作成者は、NuGet パッケージの一部としてドメイン固有のコード分析を配布することができます。 これらのアナライザーは .NET コンパイラ プラットフォーム (コードネーム "Roslyn") により駆動されるので、行を完了する前に入力したコードに対する警告を生成することができます (問題を検出するためにコードのビルドを待つ必要はありません)。 また、アナライザーでは、Visual Studio 電球のプロンプトを使用してコードを自動的に修正することもできます。これにより、コードをすぐにクリーンアップできます。

## <a name="get-started"></a>はじめに

[Roslyn アナライザーの概要](../code-quality/roslyn-analyzers-overview.md)

[チュートリアル: 最初のアナライザーとコード修正を作成する](/dotnet/csharp/roslyn-sdk/tutorials/how-to-write-csharp-analyzer-code-fix)

[コード修正の追加のチュートリアル: アナライザーの問題についてユーザーに修正プログラムを提供する](/archive/msdn-magazine/2015/february/csharp-adding-a-code-fix-to-your-roslyn-analyzer)

[説明](https://channel9.msdn.com/events/Build/2015/3-725)を視聴することもできる[現実に使える Roslyn アナライザー](../extensibility/roslyn-analyzers-and-code-aware-library-for-immutablearrays.md)

[3 種類のアナライザーにグループ化された GitHub のいくつかの例](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)

## <a name="see-also"></a>関連項目

- [.NET コンパイラ プラットフォーム パッケージ バージョン リファレンス](roslyn-version-support.md)
- [GitHub OSS サイトに関するその他のドキュメント](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)
- [Roslyn アナライザーで実装された FxCop 規則](../code-quality/fxcop-rule-port-status.md)
