---
title: RegPkg パッケージ登録のトラブルシューティング | Microsoft Docs
description: この情報を使用して、Visual Studio で RegPkg パッケージ登録のトラブルシューティングを行います。 パッケージに適したバージョンの RegPkg を使用します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: troubleshooting
helpviewer_keywords:
- RegPkg
ms.assetid: f33f822f-697a-4bad-9c10-554b4c8f6246
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 48e3699b095ed7b9d0e72cf7b09ad02e26ac5a51
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090760"
---
# <a name="troubleshooting-regpkg-package-registration"></a>RegPkg パッケージ登録のトラブルシューティング
> [!NOTE]
> Visual Studio でパッケージを登録するために推奨される方法は、.pkgdef ファイルの使用です。 これにより、システム レジストリにアクセスしなくても拡張機能をデプロイできます。 pkgdef ファイルは、[CreatePkgDef ユーティリティ](../../extensibility/internals/createpkgdef-utility.md)を使用して作成されます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で RegPkg を使用してパッケージを登録するには、パッケージに適したバージョンの RegPkg を使用する必要があります。

## <a name="regpkg-versions-related-to-package-versions"></a>パッケージのバージョンに関連する RegPkg バージョン
 RegPkg には 2 つのバージョンがあります。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] には 1 つのバージョンが含まれています。 このバージョンを使って、次のいずれかのアセンブリを使用してビルドされたパッケージを登録します。

1. Microsoft.VisualStudioShell.9.0.dll

2. Microsoft.VisualStudioShell.10.0.dll

3. Microsoft.VisualStudioShell.11.0.dll

   前の Microsoft.VisualStudio.Shell.dll アセンブリを使用してビルドされたパッケージを登録することはできません。

   前のバージョンの RegPkg では、Microsoft.VisualStudio.Shell.dll アセンブリを使用してビルドされたパッケージを登録できます。 ただし、以降のバージョンのそのアセンブリを使用してビルドされたパッケージを登録することはできません。

## <a name="see-also"></a>関連項目
- [VSPackages](../../extensibility/internals/vspackages.md)
- [Visual Studio トラブルシューティング](/troubleshoot/visualstudio/welcome-visual-studio/)
