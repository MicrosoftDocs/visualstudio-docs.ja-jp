---
title: プロジェクト システムを拡張するための IDE 定義コマンド | Microsoft Docs
description: プロジェクト システムの拡張に使用される、Visual Studio 統合開発環境 (IDE) で定義されているコマンドとコマンド グループについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, project systems
- project systems, environment-defined commands
ms.assetid: 0e33b8e9-16fa-4400-a941-e92d56120e7e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6fedca7081c531fef257e20e64426f8b35e88e87
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086002"
---
# <a name="ide-defined-commands-for-extending-project-systems"></a>プロジェクト システムを拡張するための IDE 定義コマンド
プロジェクト システムを拡張する場合は、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE によって提供されるコマンドとコマンド グループを使用できます。

 以下のセクションでは、プロジェクト システムの拡張に特に役立つコマンド項目の一覧を示します。

## <a name="command-menus"></a>コマンド メニュー
 次の表は、プロジェクト エクステンダーを呼び出す高レベルのコマンドを配置するための便利な場所であるコマンド メニューを示しています。

|コマンド メニュー|説明|
|------------------|-----------------|
|IDM_VS_MENU_PROJECT|**プロジェクト** の最上位レベルのメニュー。|
|IDM_VS_TOOL_PROJWIN|**ソリューション エクスプローラー** のツール バー。|

## <a name="shortcut-menus"></a>ショートカット メニュー
 次の表は、**ソリューション エクスプローラー** で 1 つのノードが選択されたとき、または **ソリューション エクスプローラー** に複数の同種の選択がある (選択されたすべてのノードが同じ種類である場合) ときに適用されるショートカット メニューを示しています。

|ショートカット メニュー|説明|
|-------------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE>|プロジェクト ノードが選択されたときに適用されます。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_ITEMNODE>|ファイルが選択されたときに適用されます。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_FOLDERNODE>|フォルダーが選択されたときに適用されます。|
|IDM_VS_CTXT_WEBREFFOLDER|Web 参照フォルダーが選択されたときに適用されます。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCEROOT>|"参照" と呼ばれる参照ルート ノードが選択されたときに適用されます。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCE>|参照ノードが選択されたときに適用されます。これには、アセンブリ、COM、プロジェクトの参照のみが含まれます。 Web 参照は含まれません。|

 次の表は、**ソリューション エクスプローラー** での選択が複数の階層にまたがっている場合に適用されるショートカット メニューを示しています。

|ショートカット メニュー|説明|
|-------------------|-----------------|
|IDM_VS_CTXT_XPROJ_SLNPROJ|現在の選択にソリューション ノードとルート プロジェクト ノードが含まれている場合に適用されます。|
|IDM_VS_CTXT_XPROJ_SLNITEM|現在の選択にソリューション ノードとプロジェクト項目が含まれている場合に適用されます。|
|IDM_VS_CTXT_XPROJ_MULTIPROJ|現在の選択が複数のルート プロジェクト ノードのみで構成されている場合に適用されます。|
|IDM_VS_CTXT_XPROJ_PROJITEM|現在の選択にルート プロジェクト ノードとプロジェクト項目が混在している場合に適用されます。 また、選択にソリューション ノードが含まれる場合があります。|
|IDM_VS_CTXT_XPROJ_MULTIITEM|現在の選択にソリューション内の複数のプロジェクトのプロジェクト項目が含まれている場合、または同じプロジェクトで異なる種類の項目が選択されている場合に適用されます。|

## <a name="command-groups"></a>コマンド グループ
 次の表は、プロジェクトを拡張するときに使用でき、<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE> ショートカット メニューからアクセスできるコマンド グループを示しています。

|コマンド グループ|説明|
|-------------------|-----------------|
|IDG_VS_CTXT_PROJECT_BUILD|プロジェクトをビルド、リビルド、デプロイするためのコマンド。|
|IDG_VS_CTXT_COMPILELINK|プロジェクトをコンパイルおよびリンクするためのコマンド。|
|IDG_VS_CTXT_PROJECT_CONFIG|プロジェクト構成とビルド順序を設定するコマンド。|
|IDG_VS_CTXT_PROJECT_ADD|プロジェクトに項目を追加するコマンド。|
|IDG_VS_CTXT_PROJECT_START|F5 キーに関連付けられるスタートアップ プロジェクトを設定するコマンド。|
|IDG_VS_CTXT_PROJECT_SAVE|プロジェクト項目を保存するためのコマンド。|
|IDG_VS_CTXT_PROJECT_DEBUG|デバッグするためのコマンド。|
|IDG_VS_CTXT_PROJECT_SCC|ソース管理用のコマンド。|
|IDG_VS_CTXT_PROJECT_TRANSFER|切り取り、コピー、貼り付け操作のためのコマンド。|
|IDG_VS_CTXT_PROJECT_PROPERTIES|**[プロジェクトのプロパティ]** ダイアログ ボックスへのアクセスを提供するコマンド。|

## <a name="see-also"></a>関連項目

- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [再利用可能なボタンのグループの作成](../../extensibility/creating-reusable-groups-of-buttons.md)
