---
title: DslTextTransform コマンド
description: TextTransform.exe を呼び出し、共通のオプションを使用して実行するスクリプトである DslTextTransform.cmd について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, commands
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 65d1e1d02c5b7d13c2e86343c6307306542d00e2
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388647"
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
