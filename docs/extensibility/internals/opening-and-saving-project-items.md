---
title: 開くと、プロジェクト項目の保存 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], file persistence
- files [Visual Studio], opening and saving
- editors [Visual Studio SDK], file persistence
ms.assetid: f71898ad-335f-4c43-a177-4da87078afd1
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 77a3417bc15bc9c4c6149b4e77dc4fdcebe5cd6e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66314932"
---
# <a name="opening-and-saving-project-items"></a>プロジェクト項目のオープンと保存
新しいプロジェクトの種類を追加するときに開始タグとでプロジェクト ファイルの保存を管理する必要があります、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合開発環境 (IDE) です。 次のトピックでは、オープンとファイルを保存する別の方法について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [ファイルを開くコマンドを使用したファイルの表示](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)

 詳しい手順については、IDE を処理する方法の提供、**ファイルを開く**コマンドと、このコマンドに対応するプロジェクトの役割。

- [プログラムから開くコマンドを使用したファイルの表示](../../extensibility/internals/displaying-files-by-using-the-open-with-command.md)

 IDE を処理する方法の詳細な手順を説明します、**プログラムから開く**コマンド、標準のエディターのいくつかの選択肢を含むファイルを開くを確認します。

- [方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)

 プロジェクトに固有のエディターを使用して、プロジェクト内の特定の種類のファイルが開かれることを指定するための手順について説明します。

- [方法: 標準のエディターを開く](../../extensibility/how-to-open-standard-editors.md)

 プロジェクトの種類のファイルの標準のエディターを開く IDE を有効にする方法を指定するための手順について説明します。

- [方法: 開いているドキュメントのエディターを開く](../../extensibility/how-to-open-editors-for-open-documents.md)

 開いているファイルのプロジェクトに固有のエディターを開く手順について説明します。

- [標準ドキュメントの保存](../../extensibility/internals/saving-a-standard-document.md)

 IDE を処理する方法について詳しく説明します、**保存**、**名前を付けて保存**、および**すべて保存**ドキュメント用のコマンドは、標準のエディターで開かれています。

- [カスタム ドキュメントの保存](../../extensibility/internals/saving-a-custom-document.md)

 図と、IDE を処理する方法の詳細については、**保存**、**名前を付けて保存**と**すべて保存**ドキュメント用のコマンドは、カスタム エディターで開かれています。

- [プロジェクトでのファイルを開くエディターの決定](../../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)

 IDE に適切なエディターまたはデザイナー ファイルの選択に依存するプロセスについて説明します。

## <a name="related-sections"></a>関連項目
- [カスタム エディターとデザイナーの作成](../../extensibility/creating-custom-editors-and-designers.md)

 エディター、IDE をホストし、各エディターの説明の 4 つの種類を一覧表示します。

- [プロジェクト タイプ](../../extensibility/internals/project-types.md)

 プロジェクトでコードをコンパイルおよびビルドする方法を制御する方法、エディターを開く方法、およびプロジェクト アイテムの書式設定方法について説明します。