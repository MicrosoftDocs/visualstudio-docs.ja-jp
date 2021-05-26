---
title: ソリューションの概要
description: Visual Studio 拡張機能でソリューションを扱う拡張機能の開発者向けに、ソリューションの内部について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions, about solutions
ms.assetid: 3b21e3a1-170a-4485-941e-6b04b7b27886
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 914f1744accc10eb55cfb0b321a04560c27bca05
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069375"
---
# <a name="solutions-overview"></a>ソリューションの概要

ソリューションは、アプリケーションを作成するために連携する 1 つ以上のプロジェクトのグループです。 ソリューションに関連するプロジェクトおよびステータス情報は、2 つの異なるソリューション ファイルに保存されます。 [ソリューション (.sln) ファイル](solution-dot-sln-file.md)はテキストベースであり、ソース コード管理下に置いてユーザー間で共有できます。 [ソリューション ユーザー オプション (.suo) ファイル](solution-user-options-dot-suo-file.md)はバイナリです。 そのため、.suo ファイルはソース コード管理下に置くことはできず、ユーザー固有の情報が含まれています。

どの VSPackage も、どちらかの種類のソリューション ファイルに書き込むことができます。 ファイルの性質上、ファイルに書き込むために 2 つの異なるインターフェイスが実装されています。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps> インターフェイスはテキスト情報を .sln ファイルに書き込み、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> インターフェイスはバイナリ ストリームを .suo ファイルに書き込みます。

> [!NOTE]
> プロジェクトでは、それ自体のエントリをソリューション ファイルに明示的に書き込む必要はありません。これは、プロジェクトの代わりに環境によって処理されます。 そのため、特にソリューション ファイルにコンテンツを追加する必要がない場合は、この方法で VSPackage を登録する必要はありません。

ソリューションの永続化をサポートしているそれぞれの VSPackage では、3 つのインターフェイスを使用します。<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> インターフェイスは、環境によって実装され、VSPackage によって呼び出されます。`IVsPersistSolutionProps` と `IVsPersistSolutionOpts` は、どちらも VSPackage によって実装されます。 `IVsPersistSolutionOpts` インターフェイスを実装する必要があるのは、プライベートな情報が VSPackage によって .suo ファイルに書き込まれる場合だけです。

ソリューションが開かれると、次の処理が行われます。

1. 環境によってソリューションが読み取られます。

2. 環境で `CLSID` が検出された場合、対応する VSPackage が読み込まれます。

3. VSPackage が読み込まれる場合、VSPackage が必要とするインターフェイスのために、環境によって <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> インターフェイスの `QueryInterface` が呼び出されます。

   - .sln ファイルから読み取るときは、環境は `IVsPersistSolutionProps` の `QueryInterface` を呼び出します。

   - .suo ファイルから読み取るときは、環境は `IVsPersistSolutionOpts` の `QueryInterface` を呼び出します。

   これらのファイルの使用に関する具体的な情報については、「[ソリューション (.Sln) ファイル](../../extensibility/internals/solution-dot-sln-file.md)」および「[ソリューション ユーザー オプション (.Suo) ファイル](../../extensibility/internals/solution-user-options-dot-suo-file.md)」を参照してください。

> [!NOTE]
> 2 つのプロジェクトの構成で成り立ち、3 番目をビルドから除外する新しいソリューション構成を作成する場合は、プロパティページの UI またはオートメーションを使用する必要があります。 ソリューション ビルド マネージャーの構成とそのプロパティを直接変更することはできませんが、オートメーション モデルの DTE の `SolutionBuild` クラスを使用してソリューション ビルド マネージャーを操作できます。 ソリューションの構成の詳細については、「[ソリューション構成](../../extensibility/internals/solution-configuration.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>
