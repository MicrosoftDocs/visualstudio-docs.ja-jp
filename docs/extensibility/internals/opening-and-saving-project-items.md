---
title: プロジェクト項目のオープンと保存 | Microsoft Docs
description: Visual Studio IDE で、新しいプロジェクト タイプのファイルを開いたり保存したりするためのさまざまな方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], file persistence
- files [Visual Studio], opening and saving
- editors [Visual Studio SDK], file persistence
ms.assetid: f71898ad-335f-4c43-a177-4da87078afd1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6ff3c76294ce99fa5eeb7bf311307e54f5d0e6cc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063072"
---
# <a name="opening-and-saving-project-items"></a>プロジェクト項目のオープンと保存
新しいプロジェクト タイプを追加する場合は、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) でのプロジェクト ファイルのオープンと保存を管理する必要があります。 次のトピックでは、ファイルを開いたり保存したりするためのさまざまな方法について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [ファイルを開くコマンドを使用したファイルの表示](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)

 IDE で **[ファイルを開く]** コマンドを処理する方法と、このコマンドに応答するプロジェクトのロールについて、順を追って説明します。

- [プログラムから開くコマンドを使用したファイルの表示](../../extensibility/internals/displaying-files-by-using-the-open-with-command.md)

 標準エディターのいくつか選択肢を提示しつつファイルを開くように求める **[プログラムから開く]** コマンドを IDE で処理する方法について順を追って説明します。

- [方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)

 プロジェクト固有のエディターを使用して開く必要があるプロジェクトで、特定の種類のファイルを指定する手順について順を追って説明します。

- [方法: 標準のエディターを開く](../../extensibility/how-to-open-standard-editors.md)

 使用するプロジェクト タイプのファイルに対して、IDE が標準エディターを開けるように指定する手順について順を追って説明します。

- [方法: 開いているドキュメントのエディターを開く](../../extensibility/how-to-open-editors-for-open-documents.md)

 開くファイルに対して、プロジェクト固有のエディターを開く手順について順を追って説明します。

- [標準ドキュメントの保存](../../extensibility/internals/saving-a-standard-document.md)

 標準エディターで開かれたドキュメントに対して、 **[保存]** 、 **[名前を付けて保存]** 、および **[すべて保存]** コマンドを IDE で処理する方法について詳しく説明します。

- [カスタム ドキュメントの保存](../../extensibility/internals/saving-a-custom-document.md)

 カスタム エディターで開かれたドキュメントに対して、 **[保存]** 、 **[名前を付けて保存]** 、および **[すべて保存]** コマンドを IDE で処理する方法について、図を交えながら詳しく説明します。

- [プロジェクトでのファイルを開くエディターの決定](../../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)

 ファイルに適切なエディターまたはデザイナーを選択するために IDE が従うプロセスについて説明します。

## <a name="related-sections"></a>関連項目
- [カスタム エディターとデザイナーの作成](../../extensibility/creating-custom-editors-and-designers.md)

 IDE がホストできる 4 種類のエディターを一覧表示し、各エディターの説明を示します。

- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 コードのコンパイルとビルド方法、エディターのオープン方法、およびプロジェクト項目の書式設定方法をプロジェクトがどのように制御するかについて説明します。
