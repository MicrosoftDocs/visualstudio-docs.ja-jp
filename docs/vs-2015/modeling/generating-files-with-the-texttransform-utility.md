---
title: TextTransform ユーティリティを使用したファイルの生成 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, TextTransform utility
- TextTransform.exe
ms.assetid: 06a48235-fe02-403e-a1cf-2ae70b4db62f
caps.latest.revision: 43
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 18776795fdf693c855edd3f629d674089daaaebd
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72666096"
---
# <a name="generating-files-with-the-texttransform-utility"></a>TextTransform ユーティリティを使用したファイルの生成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

TextTransform は、テキストテンプレートを変換するために使用できるコマンドラインツールです。 TextTransform を呼び出す場合は、テキストテンプレートファイルの名前を引数として指定します。 TextTransform はテキスト変換エンジンを呼び出し、テキストテンプレートを処理します。 通常、TextTransform はスクリプトから呼び出されます。 ただし、通常は必要ありません。これは、Visual Studio またはビルド処理でテキスト変換を実行できるためです。

> [!NOTE]
> ビルド処理の一部としてテキスト変換を実行する場合は、MSBuild テキスト変換タスクの使用を検討してください。 詳細については、「[ビルドプロセスでのコード生成](../modeling/code-generation-in-a-build-process.md)」を参照してください。 @No__t_0 がインストールされているコンピューターでは、テキストテンプレートを変換できるアプリケーションまたは [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の拡張機能を作成することもできます。 詳細については、「[カスタムホストを使用したテキストテンプレートの処理](../modeling/processing-text-templates-by-using-a-custom-host.md)」を参照してください。

 TextTransform .exe は、次のディレクトリにあります。

 **Files\Common の Shared\TextTemplating\11.0**

## <a name="syntax"></a>構文

```
TextTransform [<options>] <templateName>
```

#### <a name="parameters"></a>パラメーター

|**引数**|**説明**|
|------------------|---------------------|
|`templateName`|変換するテンプレートファイルの名前を指定します。|

|**オプション**|**説明**|
|----------------|---------------------|
|**out** \<filename >|変換の出力の書き込み先のファイル。|
|**-r** \<assembly >|テキストテンプレートをコンパイルして実行するために使用されるアセンブリ。|
|**-u** \<namespace >|テンプレートをコンパイルするために使用される名前空間。|
|**-I** \<includedirectory >|指定したテキストテンプレートに含まれるテキストテンプレートを格納しているディレクトリ。|
|**-P** \<referencepath >|テキストテンプレート内で指定されたアセンブリを検索するディレクトリ。または、 **-r**オプションを使用する場合は。<br /><br /> たとえば、Visual Studio API に使用するアセンブリを含めるには、を使用します。<br /><br /> `-P "%VSSHELLFOLDER%\Common7\IDE\PublicAssemblies"`|
|**-dp** \<processorName >!\<className >!\<assemblyName&#124;コードベース >|テキストテンプレート内のカスタムディレクティブの処理に使用できるディレクティブプロセッサの名前、完全な型名、およびアセンブリ。|
|**-a** [processorname]![直接の Ename]\<parameterName >!\<parameterValue >|ディレクティブプロセッサのパラメーター値を指定します。 パラメーターの名前と値だけを指定した場合、パラメーターはすべてのディレクティブプロセッサで使用できるようになります。 ディレクティブプロセッサを指定する場合、パラメーターは、指定されたプロセッサでのみ使用できます。 ディレクティブ名を指定した場合、パラメーターは、指定されたディレクティブが処理されている場合にのみ使用できます。<br /><br />  テキストテンプレートで、テンプレートディレクティブに `hostspecific` を含め、`this.Host` でメッセージを呼び出します。 (例:<br /><br /> `<#@template language="c#" hostspecific="true"#> [<#= this.Host.ResolveParameterValue("", "", "parameterName") #>]`.<br /><br /> オプションのプロセッサ名とディレクティブ名を省略した場合でも、必ず '! ' マークを入力してください。 (例:<br /><br /> `-a !!param!value`|
|**-h**|ヘルプを提供します。|

## <a name="related-topics"></a>関連トピック

|タスク|トピック|
|----------|-----------|
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューション内にファイルを生成する。|[T4 テキスト テンプレートを使用したデザイン時コード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)|
|独自のデータ ソースを変換するためのディレクティブ プロセッサを作成する。|[T4 テキスト変換のカスタマイズ](../modeling/customizing-t4-text-transformation.md)|
|独自のアプリケーションからテキストテンプレートを呼び出すことができるテキストテンプレートホストを作成します。|[カスタム ホストを使用したテキスト テンプレートの処理](../modeling/processing-text-templates-by-using-a-custom-host.md)|
