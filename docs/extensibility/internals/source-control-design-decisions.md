---
title: ソース管理のデザインの方針 | Microsoft Docs
description: ソース管理を実装するときに、プロジェクトに対して考慮する必要がある重要なデザインの方針について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], design decisions
ms.assetid: 5f60ec1a-5a74-4362-8293-817a4dd73872
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 82afa3bfee446ab5bd214fd5ac58dbfac9523467
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069323"
---
# <a name="source-control-design-decisions"></a>ソース管理のデザインの方針
ソース管理を実装するときは、次に示すデザインの方針をプロジェクトに対して考慮する必要があります。

## <a name="will-information-be-shared-or-private"></a>情報は共有されるか、それとも非公開か
 判断できる最も重要なデザインの方針は、どの情報が共有可能であり、どの情報が非公開であるかです。 たとえば、プロジェクトのファイルの一覧を共有する一方で、一部のユーザーが非公開にしたいと考えるファイルがこの一覧に含まれている場合があります。 コンパイラ設定は共有されますが、スタートアップ プロジェクトは通常、非公開です。 設定は、完全に共有されるか、オーバーライド付きで共有されるか、完全に非公開にするかのいずれかです。 設計上、ソリューション ユーザー オプション (.suo) ファイルなどのプライベート項目は [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] にチェックインされません。 プライベートな情報は必ず、.suo ファイルなどのプライベート ファイル、または作成する特定のプライベート ファイル (たとえば、Visual C# の場合は .csproj.user ファイル、Visual Basic の場合は .vbproj.user ファイル) に保存してください。

 この決定は、すべてを網羅するものではなく、アイテムごとに行うことができます。

## <a name="will-the-project-include-special-files"></a>プロジェクトに特殊なファイルが含まれるか
 もう 1 つの重要なデザインの方針は、プロジェクト構造で特殊なファイルを使用するかどうかです。 特殊なファイルとは、ソリューション エクスプローラーや、チェックインおよびチェックアウトのダイアログ ボックスに表示されるファイル以外の隠しファイルのことです。 特殊なファイルを使用する場合は、以下のガイドラインに従ってください。

1. 特殊なファイルは、プロジェクトのルート ノード、つまりプロジェクト ファイルそのものには関連付けないでください。 プロジェクト ファイルは単一のファイルである必要があります。

2. プロジェクトで特別なファイルが追加、削除、または名前変更されたときに、ファイルが特別なファイルであることを示すフラグが設定されたうえで、適切な <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> イベントが発生する必要があります。 これらのイベントは、適切な <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> メソッドを呼び出すプロジェクトに応答する形で、環境によって呼び出されます。

3. プロジェクトまたはエディターでファイルに対して <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> を呼び出したとき、そのファイルに関連付けられている特別なファイルは自動的にチェックアウトされません。親のファイルと一緒に特別なファイルを渡してください。 環境によって、渡されたすべてのファイル間の関係が検出され、チェックアウト UI で特殊なファイルが適切に非表示になります。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- [ソース管理のサポート](../../extensibility/internals/supporting-source-control.md)
