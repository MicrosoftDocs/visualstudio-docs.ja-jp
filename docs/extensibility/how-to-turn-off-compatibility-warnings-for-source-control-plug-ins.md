---
title: ソース管理プラグインの警告をオフにする
description: Visual Studio でソース管理を採用している場合、ユーザーにいくつかの互換性に関する警告が表示されることがあります。 これらの警告を無効にする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, turning off compatibility warnings
- compatibility warnings, turning off
ms.assetid: ba318e12-921b-4b7a-a8c2-12c712be1dbf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e7bbf2f01b2fb82e3bbb640eba5c44f99f2b7a53
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074900"
---
# <a name="how-to-turn-off-compatibility-warnings-for-source-control-plug-ins"></a>方法: ソース管理プラグインの互換性に関する警告をオフにする

[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] でソース管理を採用している場合、ユーザーにいくつかの互換性に関する警告が表示されることがあります。 表示される警告は、ソース管理プラグインの機能によって異なり、ここで詳しく説明しているように、無効にすることができます。

### <a name="to-disable-the-warning-to-ensure-optimal-source-control-integration-with-visual-studio"></a>警告: "Visual Studio と統合されたソース管理の機能を最大限に活用するためには" を無効にするには

- 次のレジストリ エントリを設定します (必要に応じて値を追加します)。

   **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl\DontDisplayCheckDotNETCompatible = dword:00000001**

   この警告は、[!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)] 以外のすべてのプラグインに対して表示されます。

### <a name="to-disable-the-warning-the-installed-source-control-provider-does-not-support-all-the-capabilities"></a>警告: "インストールされたソース管理プロバイダーは、すべての機能をサポートしていません" を無効にするには

- 次の 2 つのレジストリ値を設定します (必要に応じて値を追加します)。

     **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl\WarnedOldMSSCCIProvider = dword:00000000**

    **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl\UseOldSCC = dword:00000001**

     この警告は、ソース管理プラグインで複数のプロジェクトの再入を明示的にサポートしていない場合 (つまり、一度に 1 つのファイルとプロジェクトしかチェックインできない場合) に表示されます。

     再入 (`SCC_CAP_REENTRANT` 機能) をサポートすることが推奨されます。そうすると、この警告は削除されます。 ただし、このサポートが不可能な場合は、これらのレジストリ エントリを設定できます。

## <a name="see-also"></a>関連項目

- [機能フラグ](../extensibility/capability-flags.md)
