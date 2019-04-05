---
title: Visual Studio の複数のバージョンのサポート |Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Visual Studio, supporting multiple versions
- VSPackages, side-by-side compatibility
ms.assetid: 0047aa90-1ed4-40d3-8772-622b2719a4b1
caps.latest.revision: 21
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: c7a1a19cf512d39bce44cfeb1376fdde422f037f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51759850"
---
# <a name="supporting-multiple-versions-of-visual-studio"></a>複数バージョンの Visual Studio をサポートする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

用語*サイド バイ サイドで*をインストールして同じコンピューター上の製品の複数のバージョンを維持することを意味します。 つまり、Vspackage の場合、ユーザーが同じコンピューターにインストールされているいくつかの Visual Studio のバージョンを持つことができます。 ただし、1 つのバージョンの Visual Studio に読み込まれる Vspackage のサイド バイ サイドのバージョンを含めることはできません。  
  
 VSPackage でサイド バイ サイドのバージョンの Visual Studio に読み込まれることを行う前に、次を検討してください。  
  
-   サイド バイ サイドでの実装戦略に従うを決定する必要があります。  
  
     詳細については、[共有間で選択するとバージョン管理 Vspackage](../extensibility/choosing-between-shared-and-versioned-vspackages.md)を参照してください。  
  
-   ソリューションとプロジェクトのファイル形式は、実装戦略に収める必要があります。  
  
     詳細については、[カスタム プロジェクトのアップグレード](../misc/upgrading-custom-projects.md)と[サイド バイ サイドで配置のファイル名拡張子を登録する](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)を参照してください。  
  
-   バージョン管理されたコンポーネントは、またすべてのバージョン間で共有されるコンポーネントを正しくインストールおよび登録できるように、インストーラーは、実装戦略を処理する必要があります。  
  
     詳細については、[Windows インストーラーで Vspackage をインストールする](../extensibility/internals/installing-vspackages-with-windows-installer.md)また[コンポーネント管理](../extensibility/internals/component-management.md)を参照してください。  
  
    > [!NOTE]
    >  Visual Studio のバージョンをインストールするの対応するバージョンをインストールしても、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]します。 たとえば、バージョン 4.0 と 4.5 の Visual Studio 2010 および Visual Studio 2012 を同じコンピューターにインストールするインストールも、 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]、それぞれします。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [共有 VSPackage と バージョン管理 VSPackage の選択](../extensibility/choosing-between-shared-and-versioned-vspackages.md)  
 VSPackage でのサイド バイ サイドで問題を解決する方法について説明します。  
  
 [side-by-side 配置に対してファイル名拡張子を登録する](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)  
 サイド バイ サイドのシナリオでは、VSPackage がファイルの関連付けを登録する方法について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [VSPackage のインストール](../misc/installing-vspackages.md)  
 VSPackage をビルドしてインストールする方法や、複数のバージョンの Visual Studio を同時に実行しているユーザーをサポートする方法について説明します。

