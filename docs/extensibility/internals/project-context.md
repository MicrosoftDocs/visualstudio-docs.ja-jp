---
title: プロジェクトのコンテキスト |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], opening items
ms.assetid: d1803f4a-24eb-44b0-b5d2-cb40c15534be
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 800a28d9829600821014aab17b36ca8506fd044a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62859625"
---
# <a name="project-context"></a>プロジェクトのコンテキスト
ユーザーを追加またはプロジェクトとプロジェクト項目では、ときに、IDE、プロジェクトのコンテキストの概念を使用して、さまざまな操作を実行する必要がありますを決定します。

 通常、ファイルは、標準的なプロジェクト オブジェクトを選択して、ユーザーが明示的に作成します、**新しいプロジェクト**コマンドまたは選択して使用できるように、**プロジェクトを開く**コマンドを**ファイル**メニュー。 このような場合は、ファイルが作成され、プロジェクトのコンテキストで開かれているし、プロジェクトの種類のドキュメントの編集コンテキストを定義します。

 いくつかのプロジェクトでは、非常に豊富なコンテキストを提供します。 たとえば、プロジェクトは、プロジェクト スコープ、プログラムの名前空間またはデータ バインディングのプロジェクトを対象のデータベース接続を管理します。 ユーザーは、ソリューション エクスプ ローラーに表示されるプロジェクト項目などの特定のプロジェクト オブジェクトを使用して直接、ファイルまたはデータベース接続を開くことが頻繁に。

 他の時間は、アイテムのプロジェクトのコンテキストが明示的に指定されていません。 項目のコンテキストが利用できないなど、ユーザーが選択してファイルを開くときに、**既存ファイルを開く**コマンドを**ファイル**メニューで、ファイル、またはユーザーがクリックすると、デバッガーが動作するときに、**ファイル内の検索**コマンド、**検索し、置換** ダイアログ ボックス。 こうした状況では、IDE の呼び出しを処理するために<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument>検索ドキュメントを開くに最適なプロジェクトのプロセスを管理します。

## <a name="see-also"></a>関連項目
- [プロジェクトの優先順位](../../extensibility/internals/project-priority.md)
- [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)