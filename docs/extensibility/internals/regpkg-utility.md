---
title: RegPkg ユーティリティ | Microsoft Docs
description: RegPkg.exe ユーティリティで VSPackage を Visual Studio に登録し、それを配置のために準備する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- regpkg, registration utility
- registration, regpkg utility
ms.assetid: 1683ee18-59d1-4bab-a674-dd00dd960de3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f5160608379549abbd469bd6cf1c17e4357eac15
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060758"
---
# <a name="regpkg-utility"></a>RegPkg ユーティリティ
> [!NOTE]
> Visual Studio でパッケージを登録するために推奨される方法は、.pkgdef ファイルの使用です。 これにより、システム レジストリにアクセスしなくても拡張機能を配置できるようになります。これは VSIX 配置の要件です。 pkgdef ファイルは、[CreatePkgDef ユーティリティ](../../extensibility/internals/createpkgdef-utility.md)を使用して作成されます。 Visual Studio パッケージの配置の詳細については、「[Visual Studio 拡張機能の配布](../../extensibility/shipping-visual-studio-extensions.md)」を参照してください。

 RegPkg.exe ユーティリティでは VSPackage を [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に登録し、それを配置のために準備します。 このユーティリティは、VSPackage の開発中にバックグラウンドで使用されます。 ユーザーが実験用ハイブで VSPackage をビルドして実行できるように、これはビルド プロセスの一部として実行されます。

 RegPkg では、いくつかの形式のシステム レジストリ スクリプトを生成できます。 これらのスクリプトは、.msi プロジェクトや Windows インストーラー XML ツールセット ファイルなどの配置プロジェクトに組み込むことができます。

 RegPkg.exe は通常、\<*Visual Studio SDK installation path*>\VisualStudioIntegration\Tools\Bin\RegPkg.exe にあります。 RegPkg は、次の構文に従います。

```
RegPkg [/root:<root>] [/regfile:<regfile>] [/rgsfile:<rgsfile> [/rgm]] [/vrgfile:<vrgfile>] [/codebase | /assembly] [/unregister] AssemblyPath
```

 /root:root 指定された Visual Studio ルートで登録を実行します。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ルート。

 /regfile:FileName レジストリを更新するのではなく、.reg ファイルを作成します。  /vrgfile、/rgsfile、または /wixfile と共に使用することはできません。

 /rgsfile:FileName レジストリを更新するのではなく、.rgs ファイルを作成します。  /vrgfile、/regfile、または /wixfile と共に使用することはできません。

 /vrgfile:FileName レジストリを更新するのではなく、.vrg ファイルを作成します。  /regfile、/rgsfile、または /wixfile と共に使用することはできません。

 /rgm rgs ファイルに加えて、.rgm ファイルを作成します。  /rgsfile と組み合わせる必要があります。

 /wixfile:FileName レジストリを更新するのではなく、Windows インストーラー XML ツールセットと互換性のあるファイルを作成します。  /regfile、/rgsfile、または /vrgfile と共に使用することはできません。

 /codebase アセンブリではなく、強制的にコードベースで登録します。

 /assembly コードベースではなく、強制的にアセンブリで登録します。

 /unregister このパッケージの登録を解除します。  /regfile、/vrgfile、/rgsfile、または /wixfile

 と共に使用することはできません。

## <a name="see-also"></a>関連項目
- [VSPackages](../../extensibility/internals/vspackages.md)
- [RegPkg パッケージ登録のトラブルシューティング](../../extensibility/internals/troubleshooting-regpkg-package-registration.md)
