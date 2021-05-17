---
title: ソース管理ランタイムの詳細 | Microsoft Docs
description: ユーザーがソース管理でプロジェクトにファイルを追加したときに、またはオートメーション コントローラーによって、プロジェクトがソース管理に追加されるしくみについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], runtime details
ms.assetid: 1acd30e0-f98c-4bde-b9cd-4076845887df
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4a25a9c29c828e1d5e70d143ccd3582dc4ec6f48
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064216"
---
# <a name="source-control-runtime-details"></a>ソース管理ランタイムの詳細
プロジェクトは、ユーザーがプロジェクト内のファイルをソース管理に追加したときに、またはウィザードなどのオートメーション コントローラーによって、ソース管理に追加されます。 ソース管理下に置かれることをプロジェクト自体で指定するのではありません。プロジェクトはソース管理をサポートしていますが、手動でソース管理に追加する必要があります。

## <a name="registering-with-a-source-control-package"></a>ソース管理パッケージへの登録
 プロジェクト内のファイルがソース管理に追加されると、環境によって <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A> が呼び出され、ソース管理システムで Cookie として使用される 4 つのあいまいな文字列が生成されます。 これらの文字列をプロジェクト ファイルに格納します。 プロジェクト タイプの起動時に、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A> を呼び出して、これらの文字列をソース管理スタブ (ソース管理パッケージを管理する Visual Studio コンポーネント) に渡す必要があります。 これにより、適切なソース管理パッケージが読み込まれ、そのパッケージでの `IVsSccManager2::RegisterSccProject` の実装に呼び出しが転送されます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A>
- [ソース管理のサポート](../../extensibility/internals/supporting-source-control.md)
