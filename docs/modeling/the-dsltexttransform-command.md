---
title: DslTextTransform コマンド
description: TextTransform.exe を呼び出し、共通のオプションを使用して実行するスクリプトである DslTextTransform.cmd について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, commands
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f51d1a5cbefc3c2cf60559075a9c9a299664ed07
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99924511"
---
# <a name="the-dsltexttransform-command"></a>DslTextTransform コマンド
DslTextTransform.cmd は、TextTransform.exe を呼び出し、共通のオプションを使用して実行するスクリプトです。 DslTextTransformation.cmd を使用すると、[!INCLUDE[dsl](../modeling/includes/dsl_md.md)] プロジェクトの夜間ビルドを自動化できます。 詳細については、「[TextTransform ユーティリティを使用したファイルの生成](../modeling/generating-files-with-the-texttransform-utility.md)」を参照してください。

 DslTextTransform.cmd は、次のディレクトリに格納されます。

 **\<Visual Studio SDK Installation Path>\VisualStudioIntegration\Tools\Bin**

 DslTextTransform.cmd への入力として、次の引数を指定できます。

- ドメイン モデル プロジェクトの出力ディレクトリ。

- デザイナー定義プロジェクトの出力ディレクトリ。

- テキスト テンプレート ファイルの場所。

  DslTextTransform.cmd では、既定のディレクティブ プロセッサとアセンブリを使用して、指定されたテキスト テンプレート ファイルを処理します。 カスタム ディレクティブ プロセッサを作成する場合は、TextTransform.exe を呼び出す独自のバッチ ファイルを作成できます。 このバッチ ファイルでは、アセンブリおよび関連付けられているカスタム ディレクティブ プロセッサを指定できます。
