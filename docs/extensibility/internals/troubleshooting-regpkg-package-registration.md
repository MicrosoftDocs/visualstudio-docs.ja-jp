---
title: RegPkg パッケージ登録のトラブルシューティング |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- RegPkg
ms.assetid: f33f822f-697a-4bad-9c10-554b4c8f6246
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 386a1a17c036207d122e4b3c7cb142a628dcfe38
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72722278"
---
# <a name="troubleshooting-regpkg-package-registration"></a>RegPkg パッケージ登録のトラブルシューティング
> [!NOTE]
> Visual Studio でパッケージを登録するには、pkgdef ファイルを使用することをお勧めします。 これにより、システムレジストリにアクセスしなくても拡張機能を展開できます。 Pkgdef ファイルは、 [Createpkgdef ユーティリティ](../../extensibility/internals/createpkgdef-utility.md)を使用して作成されます。

 @No__t_0 で RegPkg を使用してパッケージを登録するには、パッケージに適したバージョンの RegPkg を使用する必要があります。

## <a name="regpkg-versions-related-to-package-versions"></a>パッケージのバージョンに関連する RegPkg のバージョン
 RegPkg には2つのバージョンがあります。 1つのバージョンが [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に含まれています。 このバージョンを使用して、次のいずれかのアセンブリを使用して作成されたパッケージを登録します。

1. VisualStudioShell. .dll

2. VisualStudioShell (.dll)

3. VisualStudioShell. 11.0. .dll

   以前の VisualStudio アセンブリを使用してビルドされたパッケージを登録することはできません。

   以前のバージョンの RegPkg では、VisualStudio アセンブリを使用してビルドされたパッケージを登録できます。 ただし、新しいバージョンのアセンブリを使用してビルドされたパッケージを登録することはできません。

## <a name="see-also"></a>関連項目
- [VSPackage](../../extensibility/internals/vspackages.md)