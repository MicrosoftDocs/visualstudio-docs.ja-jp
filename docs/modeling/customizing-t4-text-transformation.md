---
title: T4 テキスト変換のカスタマイズ
description: テキスト テンプレートのディレクティブ プロセッサまたはテキスト テンプレート ホストをカスタマイズすることで、既定のテンプレート変換プロセスを拡張する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, API
- text templates, custom hosts
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4565e710d1b3172507cb3f966cd2a920d3b3aaa8
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99935405"
---
# <a name="customize-t4-text-transformation"></a>T4 テキスト変換をカスタマイズする

テキスト テンプレートは、変換プロセスを使用してプログラム コードやその他のテキスト ファイルを生成できるようにする Visual Studio の機能です。 [!INCLUDE[vssdk_current_short](../modeling/includes/vssdk_current_short_md.md)] を使用して、テキスト テンプレートのディレクティブ プロセッサまたはテキスト テンプレート ホストをカスタマイズすることで、既定のテンプレート変換プロセスを拡張できます。

## <a name="in-this-section"></a>このセクションの内容

 [テキスト テンプレート変換プロセス](../modeling/the-text-template-transformation-process.md) - テキスト変換のしくみと、テンプレート ホストとディレクティブ プロセッサの役割について説明します。

 [カスタム T4 テキスト テンプレート ディレクティブ プロセッサの作成](../modeling/creating-custom-t4-text-template-directive-processors.md) - ディレクティブ プロセッサは、`<#@template#>.` などのテンプレート内のディレクティブを処理します。それはテンプレートのコンパイル中に実行され、アセンブリやその他のリソースを読み込むことができます。 実行時にリソースを読み込むコードを挿入することもできます。 独自のディレクティブ プロセッサを定義することで、テンプレートの複雑さを軽減できます。

 [VS 拡張機能でのテキスト変換の呼び出し](../modeling/invoking-text-transformation-in-a-vs-extension.md) - メニュー コマンドやイベント ハンドラーなどの Visual Studio 拡張機能を記述する場合、拡張機能でテキスト テンプレート サービスを使用してテキスト テンプレートを変換できます。 パラメーター データは、Session オブジェクトを使用してテンプレートに渡すことができ、`<#@parameter#>` ディレクティブを使用してテンプレート内から値を取得できます。

 [カスタム ホストを使用したテキスト テンプレートの処理](../modeling/processing-text-templates-by-using-a-custom-host.md) - テキスト テンプレートのコードが実行されると、ホストによって外部ファイルとアプリケーションの状態へのアクセスが提供されます。 たとえば、Visual Studio でテキスト変換を実行するホストで、**ソリューション エクスプローラー** へのアクセスを提供できます。 エラー メッセージ ウィンドウへのエラーの表示も行います。 テキスト変換を別のコンテキストで実行する場合は、そのコンテキストで利用可能なサービスへのアクセスを提供する独自のホストを定義できます。

 Visual Studio 拡張機能を記述する場合は、独自のホストを記述する代わりに、既存のテキスト変換サービスを使用することを検討してください。 詳細については、「[VS 拡張機能でのテキスト変換の呼び出し](../modeling/invoking-text-transformation-in-a-vs-extension.md)」を参照してください。

## <a name="reference"></a>関連項目

- [T4 テキスト テンプレートの記述](../modeling/writing-a-t4-text-template.md) - テキスト テンプレートのディレクティブとコントロール ブロックの構文を示します。
