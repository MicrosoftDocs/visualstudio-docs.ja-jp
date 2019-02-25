---
title: どのような&#39;ソース新プラグイン API バージョン 1.3 の制御 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, what's new in API v1.3
- what's new [Visual Studio SDK], source control plug-ins
ms.assetid: 7dfb2227-6e1d-4028-bce9-f8967456a993
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8b61e56fcef8bbbe8e9f36a39580eae14ad582d5
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56645980"
---
# <a name="what39s-new-in-the-source-control-plug-in-api-version-13"></a>どのような&#39;ソース新プラグイン API バージョン 1.3 を制御します。
ソース管理プラグイン API バージョン 1.3 より高度な制御を提供する次の関数について説明します。

## <a name="changes"></a>変更内容
 次の関数は、新しいソース管理プラグイン API バージョン 1.3 には。

|関数|概要|
|--------------|--------------|
|[SccGetExtendedCapabilities](../../extensibility/sccgetextendedcapabilities-function.md)|により、報告する追加機能ビット|
|[SccEnumChangedFiles](../../extensibility/sccenumchangedfiles-function.md)|ローカル ディスク上のよりもバージョン管理データベースに新しいバージョンがファイルを調べることができます。|
|[SccQueryChanges](../../extensibility/sccquerychanges-function.md)|指定したファイルの 名前の変更 (名前変更、追加、および削除) の状態を調べることができます。|
|[SccPopulateDirList](../../extensibility/sccpopulatedirlist-function.md)|ディレクトリおよびファイルのバージョン管理データベースでの調べることができます。|
|[SccAddFilesFromSCC](../../extensibility/sccaddfilesfromscc-function.md)|バージョン管理データベースからファイルの指定された一覧を現在のプロジェクトに追加します。|
|[SccBackgroundGet](../../extensibility/sccbackgroundget-function.md)|サイレント"Get"(ユーザー インターフェイスは表示されません)、指定されたファイルの実行します。|
|[SccGetUserOption](../../extensibility/sccgetuseroption-function.md)|ユーザー固有のオプションにアクセスをできます。|

## <a name="see-also"></a>関連項目
- [はじめに](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)
- [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)