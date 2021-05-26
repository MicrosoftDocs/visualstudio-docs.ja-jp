---
title: 複数バージョンの Visual Studio をサポートする | Microsoft Docs
description: 複数バージョンの Visual Studio をサポートし、お使いの VSPackage をさまざまなバージョンに読み込めるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, supporting multiple versions
- VSPackages, side-by-side compatibility
ms.assetid: 0047aa90-1ed4-40d3-8772-622b2719a4b1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3d455ebf18ee8817e2adac2fa266592594ca7e6c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056104"
---
# <a name="supporting-multiple-versions-of-visual-studio"></a>複数バージョンの Visual Studio をサポートする
*side-by-side* という用語は、製品の複数のバージョンを同じコンピューターにインストールして維持できることを意味します。 VSPackage では、それはユーザーが複数の Visual Studio バージョンを同じコンピューターにインストールできることを意味します。 ただし、お使いの VSPackage の side-by-side 実行バージョンを 1 つの Visual Studio バージョンに読み込むことはできません。

 VSPackage を Visual Studio の side-by-side 実行バージョンに読み込む前に、次の点を考慮してください。

- 実行する side-by-side 実装方法を決める必要があります。

   詳細については、「[共有 VSPackage とバージョン管理 VSPackage の選択](../extensibility/choosing-between-shared-and-versioned-vspackages.md)」をご覧ください。

- ソリューションとプロジェクト ファイルの形式が実装方法に適合している必要があります。

   詳細については、「[カスタム プロジェクトのアップグレード](../extensibility/internals/upgrading-projects.md#upgrading-custom-projects)」および [side-by-side 配置に対するファイル名拡張子の登録](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)に関するページをご覧ください。

- インストーラーで、バージョン管理されたコンポーネントと、すべてのバージョン間で共有されるコンポーネントが正しくインストールおよび登録されるように、実装方法を処理する必要があります。

   詳細については、「[Windows インストーラーによる VSPackage のインストール](../extensibility/internals/installing-vspackages-with-windows-installer.md)」および「[コンポーネント管理](../extensibility/internals/component-management.md)」をご覧ください。

  > [!NOTE]
  > あるバージョンの Visual Studio をインストールすると、対応する .NET Framework のバージョンもインストールされます。 たとえば、Visual Studio 2010 と Visual Studio 2012 を同じコンピューターにインストールすると、.NET Framework のバージョン 4.0 と 4.5 もそれぞれインストールされます。

## <a name="in-this-section"></a>このセクションの内容
- 「[共有 VSPackage と バージョン管理 VSPackage の選択](../extensibility/choosing-between-shared-and-versioned-vspackages.md)」では、VSPackage で発生する side-by-side の問題を解決する方法について説明します。

- [side-by-side 配置に対するファイル名拡張子の登録](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)に関する記事では、side-by-side のシナリオにおいて VSPackage でファイルの関連付けを登録する方法について説明します。

## <a name="related-sections"></a>関連項目
- [Windows インストーラーによる VSPackage のインストール](../extensibility/internals/installing-vspackages-with-windows-installer.md)
