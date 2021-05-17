---
title: プロジェクトのコンテキスト | Microsoft Docs
description: Visual Studio IDE でプロジェクトのコンテキストを使用して、ユーザーがプロジェクトおよびプロジェクト項目を追加または操作するときの操作の実行方法を決定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], opening items
ms.assetid: d1803f4a-24eb-44b0-b5d2-cb40c15534be
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 38571b51c31b20bd38e50dd32644be4c262e0702
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062864"
---
# <a name="project-context"></a>プロジェクトのコンテキスト
ユーザーがプロジェクトおよびプロジェクト項目を追加または操作すると、IDE ではプロジェクトのコンテキストの概念を使用して、さまざまな操作を実行する方法を決定します。

 通常、ファイルは、ユーザーが **[新しいプロジェクト]** コマンドを選択して明示的に作成するか、 **[ファイル]** メニューの **[プロジェクトを開く]** コマンドを選択して使用できるようにする標準プロジェクト オブジェクトです。 このような場合、ファイルが作成されてプロジェクトのコンテキストで開かれます。また、プロジェクト タイプで、ドキュメントを編集するためのコンテキストが定義されます。

 一部のプロジェクトは、非常に豊富なコンテキストを提供します。 たとえば、プロジェクトでは、プログラムによるプロジェクト スコープ名前空間、またはデータ バインディング用のプロジェクト スコープ データベース接続を管理します。 ユーザーは、ソリューション エクスプローラーに表示されるプロジェクト項目などの特定のプロジェクト オブジェクトを使用して、ファイルまたはデータベース接続を直接何度も開くことができます。

 それ以外の場合は、項目のプロジェクト コンテキストは明示的に指定されません。 たとえば、ユーザーが、 **[ファイル]** メニューの **[既存のファイルを開く]** コマンドを選択してファイルを開くとき、デバッガーでファイルを操作するとき、またはユーザーが **[検索と置換]** ダイアログ ボックスで **[フォルダーを指定して検索]** コマンドをクリックするときには、項目のコンテキストを使用することはできません。 このような状況に対処するために、IDE では <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument> を呼び出して、ドキュメントを開くための最適なプロジェクトを検索するプロセスを管理します。

## <a name="see-also"></a>関連項目
- [プロジェクトの優先順位](../../extensibility/internals/project-priority.md)
- [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
