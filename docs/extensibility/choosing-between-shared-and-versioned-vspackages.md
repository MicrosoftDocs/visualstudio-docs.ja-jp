---
title: 共有 VSPackage と バージョン管理 VSPackage の選択 | Microsoft Docs
description: 共有またはバージョン管理された戦略を通して、複数のバージョンの Visual Studio と .NET Framework を含む Vspackage をサイドバイサイドでインストールする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- SxS
- side-by-side installation
- installation [Visual Studio SDK], side-by-side
ms.assetid: e3128ac3-2e92-48e9-87ab-3b6c9d80e8c9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 257158ec3c8d4364e1aa52133c457e24fd98cff3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078241"
---
# <a name="choose-between-shared-and-versioned-vspackages"></a>共有 VSPackage と バージョン管理 VSPackage の選択
異なるバージョンの Visual Studio を同じコンピューター上で共存させることができます。 Vspackage では、任意のバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を組み合わせることができます。

 Vspackage のサイドバイサイドインストールは、2 つの戦略 (共有戦略またはバージョン管理された戦略) のいずれかを使用して有効にすることができます。 どちらを使用しても、複数のバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] と .NET Framework の関連バージョンを共存させることができます。

 共有戦略では、1 つの VSPackage が複数のバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 用に登録されます。 バージョン管理された戦略では、複数の VSPackage DLL がインストールされ、それぞれがサポートする [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の各バージョンに対応します。

## <a name="shared-vspackages"></a>共有 Vspackage
 共有 VSPackage は、複数のバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] で同じ VSPackage を使用する場合に適しています。 共有 VSPackage を実装するには、次の手順を実行する必要があります。

- VSPackage と複数のバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] との互換性を確保します。 これを行うには、次の 2 つの方法があります。

  - サポートする最も古いバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の機能のみを使用するように、VSPackage を制限します。

  - VSPackage が実行されている [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のバージョンに合わせて、それをプログラムします。 これで、新しいサービスのクエリが失敗した場合に、VSPackage では、以前のバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] でサポートされている他のサービスを提供できます。

- VSPackage を適切に登録します。 詳細については、「[VSPackage の登録](../extensibility/internals/vspackage-registration.md)」および[マネージド VSPackage の登録](/previous-versions/bb166783(v=vs.100))に関するページを参照してください。

- ファイル拡張子を適切に登録します。 詳細については、[side-by-side 配置に対してファイル名拡張子を登録する方法](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)に関するページを参照してください。

- 適切なバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 用の VSPackage を展開するインストーラーを作成します。 詳細については、「[Windows インストーラーによる VSPackage のインストール](../extensibility/internals/installing-vspackages-with-windows-installer.md)」および「[コンポーネント管理](../extensibility/internals/component-management.md)」を参照してください。

- 登録の競合に関する問題に対処します。 詳細については、「[VSPackage の登録](../extensibility/internals/vspackage-registration.md)」を参照してください。

- 共有およびバージョン付きファイルの両方で、複数のバージョンを安全にインストールおよび削除できるように、参照カウントが考慮されていることを確認します。 詳細については、「[コンポーネント管理](../extensibility/internals/component-management.md)」を参照してください。

## <a name="versioned-vspackages"></a>バージョン管理された Vspackage
 バージョン管理された VSPackage 戦略では、サポートする [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のバージョンごとに 1 つの VSPackage を作成します。 各 VSPackage を他に影響を与えずに拡張できるため、この方法は、以降のバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] で提供されるサービスを利用することが予想される場合に適しています。 ただし、バージョン管理された戦略では、1 つのコード ベースまたは複数の独立したコード ベースから複数のバイナリを作成するので、共有戦略に比べて多くの初期開発が必要になる場合があります。 また、追加のセットアップ作業が必要になることがあります。これは、各バージョンに対して個別のセットアップを作成するか、インストールされている [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のバージョンと VSPackage でサポートされているものを検出する 1 つのセットアップを作成する必要があるためです。

## <a name="binary-compatibility"></a>バイナリの互換性
 一般に、バイナリの互換性を使用すると、以前のバージョンの Visual Studio で開発されたネイティブコードの Vspackage を、新しいバージョンの Visual Studio で実行できるようになります。 ただし、重要な例外として、次の 3 つの点があります。

- VSPackage が特定のバージョンの共通言語ランタイムに依存している場合は、それが実行されている [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のバージョンを確認する必要があります。

- VSPackage は、別の VSPackage または別の製品の特定の機能に依存している場合があります。 その結果、VSPackage は依存関係が満たされている場所でのみ実行できます。

- VSPackage は、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] Service Pack または以降のバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のセキュリティ修正プログラムの影響を受けることがあります。 このような場合、セキュリティ修正プログラムが適用されると、以前のバージョンの [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] で開発された VSPackage は、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の他のバージョンでは実行されない場合があります。 ただし、新しいバージョンでリビルドされたパッケージは、以前のバージョンでも実行することができます。

  マネージド Vspackage は、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の 1 つのバージョン と、ターゲット バージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] と一致する [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] を使用してビルドする必要があり ます。

  VSPackage バイナリのバイナリ互換性を計画するだけでなく、ソリューションとプロジェクト ファイルの形式も考慮する必要があります。 VSPackage で新しいプロジェクト タイプを作成する場合、1 つのバージョンのみ、または複数バージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のどちらで実行できるようにするかを決定する必要があります。 詳細については、「[カスタム プロジェクトのアップグレード](../extensibility/internals/upgrading-projects.md#upgrading-custom-projects)」を参照してください。

## <a name="see-also"></a>関連項目
- [Windows インストーラーによる VSPackage のインストール](../extensibility/internals/installing-vspackages-with-windows-installer.md)
- [コンポーネント管理](../extensibility/internals/component-management.md)