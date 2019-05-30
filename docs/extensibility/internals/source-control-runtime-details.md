---
title: ソース管理ランタイムの詳細 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], runtime details
ms.assetid: 1acd30e0-f98c-4bde-b9cd-4076845887df
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1e84fd82c5da5deea2d718baf67799e5bf877131
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322562"
---
# <a name="source-control-runtime-details"></a>ソース管理ランタイムの詳細
プロジェクトは、ユーザーは、ウィザードなどのオートメーション コント ローラーまたはソース管理にプロジェクトのファイルを追加するとき、ソース管理に追加されます。 ソース管理されているある自体のプロジェクトが指定はしません。ソース管理をサポートしていますが、これを手動で追加する必要があります。

## <a name="registering-with-a-source-control-package"></a>ソース管理のパッケージへの登録
 ソース管理に、プロジェクト内のファイルが追加されると、環境を呼び出す<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A>cookie としてソース管理システムで使用される 4 つの不透明な文字列を提供します。 プロジェクト ファイル内には、これらの文字列を格納します。 これらの文字列渡す必要があります (ソース管理パッケージを管理する Visual Studio コンポーネント) のソース コントロール スタブをプロジェクトの種類の起動時に呼び出すことによって<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A>します。 これでさらに適切なソース管理パッケージを読み込みますありの実装への呼び出しを転送`IVsSccManager2::RegisterSccProject`します。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A>
- [ソース管理のサポート](../../extensibility/internals/supporting-source-control.md)