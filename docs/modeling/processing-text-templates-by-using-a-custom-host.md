---
title: カスタム ホストを使用したテキスト テンプレートの処理
description: テキスト テンプレート変換プロセスでは、テキスト テンプレート ファイルを入力として受け取り、テキスト ファイルを出力として生成することを学習します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, in application or VS extension
- text templates, custom directive hosts
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a301df6edaf8558ade5c8a297f233b58de6d8f4e
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390933"
---
# <a name="process-text-templates-by-using-a-custom-host"></a>カスタム ホストを使用してテキスト テンプレートを処理する

"*テキスト テンプレート変換*" プロセスでは、テキスト "*テンプレート ファイル*" を入力として受け取り、テキスト ファイルを出力として生成します。 テキスト変換エンジンは、Visual Studio 拡張機能か、Visual Studio がインストールされているコンピューターで実行中のスタンドアロン アプリケーションから呼び出すことができます。 ただし、"*テキスト テンプレート ホスト*" を提供する必要があります。 このクラスは、テンプレートを環境に接続し、アセンブリやインクルード ファイルなどのリソースの検索と、出力およびエラー メッセージの処理を行います。

> [!TIP]
> Visual Studio 内で実行されるパッケージまたは拡張機能を作成する場合は、独自のホストを作成するのではなく、テキスト テンプレート サービスを使用することを検討します。 詳細については、「[VS 拡張機能でのテキスト変換の呼び出し](../modeling/invoking-text-transformation-in-a-vs-extension.md)」を参照してください。

> [!NOTE]
> サーバー アプリケーションでテキスト テンプレート変換を使用することはお勧めしません。 また、シングル スレッド以外でテキスト テンプレート変換を使用することはお勧めしません。 テキスト テンプレート エンジンでは、単一の AppDomain を再利用して、テンプレートを変換、コンパイル、および実行するためです。 変換されたコードは、スレッド セーフになるように設計されているわけではありません。 デザイン時にはファイルは Visual Studio プロジェクトに含まれているので、このエンジンはファイルを連続的に処理するように設計されています。
>
> 実行時アプリケーションでは、前処理されたテキスト テンプレートを使用することを検討します。「[T4 テキスト テンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)」を参照してください。

コンパイル時に決定されるテンプレートのセットをアプリケーションで使用する場合は、前処理されたテキスト テンプレートを使用する方が簡単です。 この方法は、Visual Studio がインストールされていないコンピューターでアプリケーションを実行する場合にも使用できます。 詳細については、「[T4 テキスト テンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)」を参照してください。

## <a name="execute-a-text-template-in-your-application"></a>アプリケーションでのテキスト テンプレートの実行

テキスト テンプレートを実行するには、<xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName> の ProcessTemplate メソッドを呼び出します。

```csharp
using Microsoft.VisualStudio.TextTemplating;
...
Engine engine = new Engine();
string output = engine.ProcessTemplate(templateString, host);
```

 アプリケーションでは、テンプレートを見つけて提供すると共に、出力を処理する必要があります。

 `host` パラメーターでは、 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))を実装するクラスを指定する必要があります。 これはエンジンによってコールバックされます。

 ホストは、エラーのログ記録、アセンブリとインクルード ファイルへの参照の解決、テンプレートを実行できるアプリケーション ドメインの指定、各ディレクティブの適切なプロセッサの呼び出しを実行できる必要があります。

 <xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName> は **Microsoft.VisualStudio.TextTemplating.\*.0.dll** で定義されており、[ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110)) は **Microsoft.VisualStudio.TextTemplating.Interfaces.\*.0.dll** で定義されています。

## <a name="in-this-section"></a>このセクションの内容
 「[チュートリアル: カスタム テキスト テンプレート ホストの作成](../modeling/walkthrough-creating-a-custom-text-template-host.md)」では、Visual Studio の外部でテキスト テンプレート機能を使用できるようにするカスタム テキスト テンプレート ホストを作成する方法について説明します。

## <a name="reference"></a>関連項目
 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))

## <a name="related-sections"></a>関連項目

- 「[テキスト テンプレート変換プロセス](../modeling/the-text-template-transformation-process.md)」では、テキスト変換のしくみと、カスタマイズできるパーツについて説明します。
- 「[カスタム T4 テキスト テンプレート ディレクティブ プロセッサの作成](../modeling/creating-custom-t4-text-template-directive-processors.md)」では、テキスト テンプレート ディレクティブ プロセッサの概要について説明します。
