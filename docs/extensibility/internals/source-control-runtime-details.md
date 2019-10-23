---
title: ソース管理のランタイムの詳細 |Microsoft Docs
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
ms.openlocfilehash: 1d2469bc25fabd9659e09d6ca841ebc44a743cca
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72723409"
---
# <a name="source-control-runtime-details"></a>ソース管理ランタイムの詳細
プロジェクトは、ユーザーがプロジェクト内のファイルをソース管理に追加するとき、またはウィザードなどのオートメーションコントローラーを介して追加されるときに、ソース管理に追加されます。 プロジェクトは、それ自体がソース管理下にあることを指定していません。ソース管理はサポートされていますが、手動で追加する必要があります。

## <a name="registering-with-a-source-control-package"></a>ソース管理パッケージへの登録
 プロジェクト内のファイルがソース管理に追加されると、環境は <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A> を呼び出して、ソース管理システムによって cookie として使用される4つの不透明な文字列を提供します。 これらの文字列をプロジェクトファイルに格納します。 これらの文字列は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A> を呼び出すことによって、プロジェクトの種類のスタートアップ時にソース管理スタブ (ソース管理パッケージを管理する Visual Studio コンポーネント) に渡す必要があります。 次に、適切なソース管理パッケージを読み込み、`IVsSccManager2::RegisterSccProject` の実装に呼び出しを転送します。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A>
- [ソース管理のサポート](../../extensibility/internals/supporting-source-control.md)