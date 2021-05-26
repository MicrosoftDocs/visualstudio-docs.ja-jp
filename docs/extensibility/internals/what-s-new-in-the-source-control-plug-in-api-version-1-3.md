---
title: ソース管理プラグイン API バージョン 1.3 の新機能
description: ソース管理プラグイン API バージョン 1.3 の新機能について説明します。このバージョンでは、より高度な管理を提供する新しい関数が導入されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, what's new in API v1.3
- what's new [Visual Studio SDK], source control plug-ins
ms.assetid: 7dfb2227-6e1d-4028-bce9-f8967456a993
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7ab9079248931758efbcfcd792ce3c79ccffb270
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074263"
---
# <a name="what39s-new-in-the-source-control-plug-in-api-version-13"></a>ソース管理プラグイン API バージョン 1.3 の新機能
ソース管理プラグイン API バージョン 1.3 では、より高度な管理を提供するために次の新しい関数が導入されています。

## <a name="changes"></a>[変更点]
 ソース管理プラグイン API バージョン 1.3 では、次の関数が新しく追加されています。

|機能|概要|
|--------------|--------------|
|[SccGetExtendedCapabilities](../../extensibility/sccgetextendedcapabilities-function.md)|追加の機能ビットを報告できるようにします|
|[SccEnumChangedFiles](../../extensibility/sccenumchangedfiles-function.md)|バージョン管理データベース内のバージョンがローカル ディスク上のバージョンよりも新しいファイルを調べることができます|
|[SccQueryChanges](../../extensibility/sccquerychanges-function.md)|指定されたファイルの名前の変化 (名前の変更、追加、削除) の状態を調べることができます|
|[SccPopulateDirList](../../extensibility/sccpopulatedirlist-function.md)|バージョン管理データベース内のディレクトリとファイルを調べることができます|
|[SccAddFilesFromSCC](../../extensibility/sccaddfilesfromscc-function.md)|バージョン管理データベースから現在のプロジェクトに、指定したファイル一覧を追加します|
|[SccBackgroundGet](../../extensibility/sccbackgroundget-function.md)|指定されたファイルのサイレントな "Get" を実行します (ユーザー インターフェイスは表示されません)|
|[SccGetUserOption](../../extensibility/sccgetuseroption-function.md)|ユーザー固有のオプションにアクセスできます|

## <a name="see-also"></a>関連項目
- [はじめに](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)
- [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
