---
title: T4 テキスト変換のカスタマイズ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, API
- text templates, custom hosts
ms.assetid: 62cd9a3c-a6e1-4b29-93f5-f2a0cf47dc92
caps.latest.revision: 30
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 71cec79acfcc934f9ddd910006f32f5207b26c84
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72654965"
---
# <a name="customizing-t4-text-transformation"></a>T4 テキスト変換のカスタマイズ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テキストテンプレートは [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の機能の1つであり、変換プロセスを使用してプログラムコードやその他のテキストファイルを生成できます。 @No__t_0 を使用すると、テキストテンプレートディレクティブプロセッサまたはテキストテンプレートホストをカスタマイズすることによって、既定のテンプレート変換プロセスを拡張できます。

## <a name="in-this-section"></a>このセクションの内容
 [テキストテンプレート変換プロセス](../modeling/the-text-template-transformation-process.md)テキスト変換のしくみについて説明し、テンプレートホストとディレクティブプロセッサの役割について説明します。

 [カスタム T4 テキストテンプレートディレクティブプロセッサの作成](../modeling/creating-custom-t4-text-template-directive-processors.md)ディレクティブプロセッサは、テンプレートのコンパイル中に実行される `<#@template#>.` など、テンプレート内のディレクティブを処理し、アセンブリやその他のリソースを読み込むことができます。 また、実行時にリソースを読み込むコードを挿入することもできます。 独自のディレクティブプロセッサを定義することで、テンプレートの複雑さを軽減できます。

 [VS 拡張機能でのテキスト変換の呼び出し](../modeling/invoking-text-transformation-in-a-vs-extension.md)メニューコマンドやイベントハンドラーなどの [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 拡張機能を記述している場合、拡張機能はテキストテンプレートサービスを使用してテキストテンプレートを変換できます。 セッションオブジェクトを使用してテンプレートにパラメーターデータを渡すことができます。また、`<#@parameter#>` ディレクティブを使用して、テンプレート内から値を取得することもできます。

 [カスタムホストを使用したテキストテンプレートの処理](../modeling/processing-text-templates-by-using-a-custom-host.md)テキストテンプレートのコードが実行されると、ホストは外部ファイルおよびアプリケーションの状態へのアクセスを提供します。 たとえば、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] でテキスト変換を実行するホストは、ソリューションエクスプローラーへのアクセスを提供できます。 また、エラーメッセージウィンドウにエラーが表示されます。 テキスト変換を別のコンテキストで実行する場合は、そのコンテキストで利用可能なサービスへのアクセスを提供する独自のホストを定義できます。

 @No__t_0 拡張機能を作成する場合は、独自のホストを作成するのではなく、既存のテキスト変換サービスを使用することを検討してください。 詳細については、「 [VS 拡張機能でのテキスト変換の呼び出し](../modeling/invoking-text-transformation-in-a-vs-extension.md)」を参照してください。

## <a name="reference"></a>参照
 [T4 テキスト テンプレートの作成](../modeling/writing-a-t4-text-template.md)

 テキストテンプレートディレクティブとコントロールブロックの構文を提供します。
