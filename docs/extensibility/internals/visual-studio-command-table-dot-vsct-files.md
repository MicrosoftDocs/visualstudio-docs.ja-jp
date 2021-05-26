---
title: Visual Studio コマンド テーブル (.vsct) ファイル | Microsoft Docs
description: コマンド テーブル構成ファイルについて説明します。これは、VSPackage に含まれる一連のコマンドを記述するテキスト ファイルです。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, overview
- Visual Studio command table configuration files (VSCT), overview
ms.assetid: 1313adb4-add4-4e74-90e2-f4be522f5259
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 305bf0e5463fd4e030f2ce3e9f7fa6eca99bfe20
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085742"
---
# <a name="visual-studio-command-table-vsct-files"></a>Visual Studio Command Table (.Vsct) ファイル
コマンド テーブル構成ファイルは、VSPackage に含まれる一連のコマンドを記述するテキスト ファイルです。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] コマンド テーブル (VSCT) コンパイラは、XML ベースの構成ファイル (.vsct ファイル) をバイナリ コマンド テーブル出力 (.cto) ファイルにコンパイルします。 結果として得られる .cto ファイルは、コマンド テーブル (CTC) コンパイラを使用して .ctc 構成ファイルをコンパイルすることによって作成されるファイルと同じです。 ただし、XML ベースの .vsct ファイルには、XML エディターや XML IntelliSense など、有利な点がいくつかあります。

 .vsct ファイルの構文とセマンティクスの詳細については、「[XML コマンド テーブル (.vsct) ファイルの設計](../../extensibility/internals/designing-xml-command-table-dot-vsct-files.md)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容
 [XML コマンド テーブル (.Vsct) ファイルの設計](../../extensibility/internals/designing-xml-command-table-dot-vsct-files.md)

 .vsct ファイルを設計する方法について説明します。

 [方法: .Vsct ファイルを作成する](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)

 .vsct ファイルを作成する方法を比較します。 新しい .vsct ファイルを手動で作成するプロセスについて説明します。

## <a name="related-sections"></a>関連項目
 [VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)

 コマンド テーブルの XML 構成ファイルの各セクションについて詳しく説明します。

 [コマンド テーブル構成 (.ctc) ファイル](/previous-versions/bb165153(v=vs.100)) 非推奨の .ctc ファイル形式の概要について説明します。

 [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

 コマンド テーブル形式の仕様について説明します。

 [VSPackage のリソース](../../extensibility/internals/resources-in-vspackages.md)

 マネージド VSPackage でマネージド リソースとアンマネージド リソースを使用する方法について説明します。

 [コマンド、メニュー、およびツール バー](../../extensibility/internals/commands-menus-and-toolbars.md)

 メニュー、ツール バー、およびコマンド コンボ ボックスが含まれている UI を作成する方法について説明します。