---
title: TextTransform ユーティリティを使用したファイルの生成
description: TextTransform ユーティリティが、テキスト テンプレートの変換に使用できるコマンド ラインツールであることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 07/26/2019
ms.topic: conceptual
helpviewer_keywords:
- text templates, TextTransform utility
- TextTransform.exe
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 741e7625d301e250daa28a93f18a82193675e068
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99902699"
---
# <a name="generate-files-with-the-texttransform-utility"></a>TextTransform ユーティリティを使用してファイルを生成する

TextTransform.exe は、テキスト テンプレートの変換に使用できるコマンド ラインツールです。 TextTransform.exe を呼び出す場合は、テキスト テンプレート ファイルの名前を引数として指定します。 TextTransform.exe によりテキスト変換エンジンが呼び出され、テキスト テンプレートが処理されます。 TextTransform.exe は通常、スクリプトから呼び出されます。 ただし、通常は必要ありません。これは、Visual Studio またはビルド処理でテキスト変換を実行できるためです。

> [!NOTE]
> ビルド処理の一部としてテキスト変換を実行する場合は、MSBuild テキスト変換タスクの使用を検討してください。 詳細については、[ビルド処理でのコード生成](../modeling/code-generation-in-a-build-process.md)に関するページを参照してください。 Visual Studio がインストールされているマシンでは、テキスト テンプレートを変換できるアプリケーションまたは Visual Studio 拡張機能を作成することもできます。 詳細については、「[カスタム ホストを使用したテキスト テンプレートの処理](../modeling/processing-text-templates-by-using-a-custom-host.md)」を参照してください。

TextTransform.exe は、次のディレクトリに格納されます。

::: moniker range=">=vs-2019"

**\Program Files (x86)\Microsoft Visual Studio\2019\Professional\Common7\IDE**

Professional edition 向け、または

**\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE**

Enterprise Edition 向け。

::: moniker-end

::: moniker range="vs-2017"

**\Program Files (x86)\Microsoft Visual Studio\2017\Professional\Common7\IDE**

Professional edition 向け、または

**\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE**

Enterprise Edition 向け。

以前のバージョンの Visual Studio では、ファイルは次の場所にあります。

**\Program Files (x86)\Common Files\Microsoft Shared\TextTemplating\{version}**

ここで、{version} は、インストールされている以前のバージョンに依存します。

::: moniker-end

## <a name="syntax"></a>構文

```
TextTransform [<options>] <templateName>
```

### <a name="parameters"></a>パラメーター

|**Argument**|**説明**|
|-|-|
|`templateName`|変換するテンプレート ファイルの名前を識別します。|

|**オプション**|**説明**|
|-|-|
|**-out** \<filename>|変換の出力の書き込み先のファイル。|
|**-r** \<assembly>|テキスト テンプレートをコンパイルして実行するために使用されるアセンブリ。|
|**-u** \<namespace>|テンプレートをコンパイルするために使用される名前空間。|
|**-I** \<includedirectory>|指定したテキスト テンプレートに含まれるテキスト テンプレートを格納しているディレクトリ。|
|**-P** \<referencepath>|テキスト テンプレート内で指定されたアセンブリを検索する、または **-r** オプションを使用する場合の対象ディレクトリ。<br /><br /> たとえば、Visual Studio API に使用するアセンブリを含めるには、次を使用します。<br /><br /> `-P "%VSSHELLFOLDER%\Common7\IDE\PublicAssemblies"`|
|**-dp** \<processorName>!\<className>!\<assemblyName&#124;codeBase>|テキスト テンプレート内のカスタム ディレクティブの処理に使用できるディレクティブ プロセッサの名前、完全な型名、およびアセンブリ。|
|**-a** [processorName]![directiveName]!\<parameterName>!\<parameterValue>|ディレクティブ プロセッサのパラメーター値を指定します。 パラメーターの名前と値だけを指定した場合、パラメーターはすべてのディレクティブ プロセッサで使用できるようになります。 ディレクティブ プロセッサを指定した場合、パラメーターは、指定されたプロセッサでのみ使用できます。 ディレクティブ名を指定した場合、パラメーターは、指定されたディレクティブが処理されている場合のみ使用できます。<br /><br /> ディレクティブ プロセッサまたはテキスト テンプレートからパラメーター値にアクセスするには、[ITextTemplatingEngineHost.ResolveParameterValue](/previous-versions/visualstudio/visual-studio-2012/bb126369\(v\=vs.110\)) を使用します。 テキスト テンプレートで、テンプレート ディレクティブに `hostspecific` を含め、`this.Host` でメッセージを呼び出します。 次に例を示します。<br /><br /> `<#@template language="c#" hostspecific="true"#> [<#= this.Host.ResolveParameterValue("", "", "parameterName") #>]`.<br /><br /> オプションのプロセッサ名とディレクティブ名を省略した場合でも、必ず '!' マークを入力してください。 次に例を示します。<br /><br /> `-a !!param!value`|
|**-h**|ヘルプを提供します。|

## <a name="related-topics"></a>関連トピック

|タスク|トピック|
|-|-|
|Visual Studio ソリューション内にファイルを生成します。|[T4 テキスト テンプレートを使用したデザイン時コード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)|
|独自のデータ ソースを変換するためのディレクティブ プロセッサを作成する。|[T4 テキスト変換のカスタマイズ](../modeling/customizing-t4-text-transformation.md)|
|独自のアプリケーションからテキスト テンプレートを呼び出すことができるテキスト テンプレート ホストを記述します。|[カスタム ホストを使用したテキスト テンプレートの処理](../modeling/processing-text-templates-by-using-a-custom-host.md)|
