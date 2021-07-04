---
title: テキスト テンプレートのセキュリティ
description: 任意のコードや悪意のあるディレクティブ プロセッサなどのトピックを含め、セキュリティとテキスト テンプレートについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, security
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0a740a6f7a4c532a61a5e412c94fa4321c5da707
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385761"
---
# <a name="security-of-text-templates"></a>テキスト テンプレートのセキュリティ
テキスト テンプレートには、次のようなセキュリティの問題があります。

- テキスト テンプレートは、任意のコードの挿入に対して脆弱です。

- ディレクティブ プロセッサを検索するためにホストが使用するメカニズムがセキュリティで保護されていない場合は、悪意のあるディレクティブ プロセッサを実行できます。

## <a name="arbitrary-code"></a>任意のコード
 テンプレートを記述するときに、\<# #> タグ内に任意のコードを配置できます。 これにより、テキスト テンプレート内から任意のコードを実行できます。

 信頼されたソースからテンプレートを取得していることを確認してください。 信頼できるソースからのものではないテンプレートを実行しないように、アプリケーションのエンドユーザーに警告してください。

## <a name="malicious-directive-processor"></a>悪意のあるディレクティブ プロセッサ
 テキスト テンプレート エンジンでは、変換ホストと 1 つ以上のディレクティブ プロセッサと対話し、テンプレート テキストを出力ファイルに変換します。 詳細については、「[テキスト テンプレート変換プロセス](../modeling/the-text-template-transformation-process.md)」を参照してください。

 ディレクティブ プロセッサを検索するためにホストが使用するメカニズムがセキュリティで保護されていない場合は、悪意のあるディレクティブ プロセッサの実行リスクがあります。 悪意のあるディレクティブ プロセッサから、テンプレートの実行時に `FullTrust` モードで実行されるコードが提供される可能性があります。 カスタム テキスト テンプレート変換ホストを作成した場合は、エンジンがディレクティブ プロセッサを見つけるために、レジストリなどの安全な機構を使用する必要があります。
