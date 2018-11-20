---
title: ビルド アクション
description: この記事では、C# プロジェクトで使用できるさまざまなビルド アクションについて説明します。
author: conceptdev
ms.author: crdun
ms.date: 05/06/2018
ms.assetid: 5399BCB1-E317-4C7B-87B1-C531E985DE6E
ms.openlocfilehash: a5b1175caf0ac7f6654fbe20b5300327679eccbc
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2018
ms.locfileid: "51294293"
---
# <a name="build-actions"></a>ビルド アクション

Visual Studio for Mac プロジェクト内のすべてのファイルに、ビルド アクションがあります。 これで、ビルド時にファイルに発生する内容を制御します。 下の画像のように、任意のファイルを右クリックして **[ビルド アクション]** に移動することで、この動作を設定できます。

![ソリューション エクスプローラーで [コンパイル] ビルド アクションを選択する](media/projects-and-solutions-image1.png)

C# プロジェクトの一般的ビルド アクションには次のようなものがあります。

* **なし** - このファイルはいかなる形でもビルドに含まれません。IDE から簡単にアクセスできるようにプロジェクトに含まれています。
* **コンパイル** - このファイルはソース ファイルとして C# コンパイラに渡されます。
* **EmbeddedResource** - このファイルはアセンブリに埋め込むリソースとして C# コンパイラに渡されます。 `System.Reflection` 名前空間の [Assembly.GetManifestResourceStream](https://docs.microsoft.com/dotnet/api/system.reflection.assembly.getmanifestresourcestream) を使用すると、アセンブリからファイルを読み取ることができます。
* **コンテンツ** - ASP.NET プロジェクトの場合、展開時、このファイルはサイトの一部として追加されます。 Xamarin.iOS プロジェクトと Xamarin.Mac プロジェクトの場合、アプリ バンドルに含まれます。

ソリューション エクスプローラーでは複数のファイルを選択でき、ビルド アクションを一度に複数のファイルに設定できます。

また、特定のプロジェクトのビルド アクションがあります。 Xamarin.iOS プロジェクトには、**BundleResource** ビルド アクションがあります。このアクションでは、アプリ バンドルの一環としてファイルを追加します。 Xamarin.Android 固有のビルド アクションに関する詳細は、[ビルド プロセス](/xamarin/android/deploy-test/building-apps/build-process#Build_Actions) ガイドでご覧いただけます。