---
title: プロジェクト フォルダーをソース管理ストアと比較する | Microsoft Docs
description: ソース管理プラグイン API では、ローカルのプロジェクト フォルダーとソース管理の比較は、SccDirQueryInfo と SccDirDiff を使用して行われます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, comparing versions
- source control plug-ins, local project folders
ms.assetid: 65217e8b-15a6-4446-92b0-4cff1c6220f5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f7b334bb6e1b73dd31060020378e91b74e5af102
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063046"
---
# <a name="optional-comparison-of-local-project-folder-to-source-control-store"></a>ソース管理ストアとローカルのプロジェクト フォルダーとの比較 (オプション)
ソース管理プラグイン API 1.2 では、ローカルのプロジェクト フォルダーとソース管理の比較は、[SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md) と [SccDirDiff](../../extensibility/sccdirdiff-function.md) を使用して行われます。

 **ソリューション エクスプローラー** 内で、個々のファイルではなくフォルダーを選択すると、 **[バージョンの比較]** ショートカット メニューによって、ソース管理プラグインの新しい [SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md) と [SccDirDiff](../../extensibility/sccdirdiff-function.md) が呼び出されます。

## <a name="new-capability-flags"></a>新しい機能フラグ
 `SCC_CAP_DIRECTORYDIFF`

 `SCC_CAP_DIRECTORYCHECKOUT`

## <a name="new-functions"></a>新しい関数
- [SccDirDiff](../../extensibility/sccdirdiff-function.md)

- [SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)

 `SccDirQueryInfo` 関数は `SccDirDiff` の前に呼び出され、作業ディレクトリがソース管理されているかどうかが判別されます。 `SccDirDiff` 関数では、現在のローカル ディレクトリとそれに対応するソース管理フォルダーとの違いが表示されます。 このコマンドにより、ソース管理プラグインは、ディレクトリに対する変更内容の一覧を表示するように要求されます。 ソース管理プラグインには、違いを表示するための独自の UI が備えられています。

> [!NOTE]
> この関数では、[SccDiff](../../extensibility/sccdiff-function.md) と同じコマンド フラグを使用します。 ソース管理プラグイン プロバイダーは、ディレクトリの "クイック diff" 操作をサポートしないことを選択できます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
