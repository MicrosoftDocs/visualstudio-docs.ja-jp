---
title: TextTransform ユーティリティを使用したファイルの生成 |Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- text templates, TextTransform utility
- TextTransform.exe
ms.assetid: 06a48235-fe02-403e-a1cf-2ae70b4db62f
caps.latest.revision: 43
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: e7dbe189c9b46c10dc7bac5da4b87457d7c6ecbf
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2018
ms.locfileid: "49227449"
---
# <a name="generating-files-with-the-texttransform-utility"></a>TextTransform ユーティリティを使用したファイルの生成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

TextTransform.exe は、テキスト テンプレートを変換するために使用できるコマンド ライン ツールです。 TextTransform.exe を呼び出すときに、引数として、テキスト テンプレート ファイルの名前を指定します。 TextTransform.exe では、テキスト変換エンジンを呼び出し、テキスト テンプレートを処理します。 TextTransform.exe は通常、スクリプトから呼び出されます。 ただし、必要でない、通常は、Visual Studio で、またはビルド プロセスでは、テキスト変換を実行するためです。  
  
> [!NOTE]
>  ビルド プロセスの一部としてテキスト変換を実行する場合は、MSBuild のテキスト変換タスクを使用して検討してください。 詳細については、[ビルド プロセスでのコード生成](../modeling/code-generation-in-a-build-process.md)を参照してください。 コンピューターでの[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]がインストールされているアプリケーションを記述することもできます。 または[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]テキスト テンプレートを変換できる拡張機能。 詳細については、[カスタム ホストを使用してテキスト テンプレートの処理](../modeling/processing-text-templates-by-using-a-custom-host.md)を参照してください。  
  
 TextTransform.exe については、次のディレクトリにあります。  
  
 **\Program Files\Common \microsoft Shared\TextTemplating\11.0**  
  
## <a name="syntax"></a>構文  
  
```  
TextTransform [<options>] <templateName>  
```  
  
#### <a name="parameters"></a>パラメーター  
  
|**引数**|**説明**|  
|------------------|---------------------|  
|`templateName`|変換するテンプレート ファイルの名前を示します。|  
  
|**オプション**|**説明**|  
|----------------|---------------------|  
|**-out** \<filename>|変換の出力を書き込むファイル。|  
|**-r** \<assembly>|アセンブリをコンパイルすると、テキスト テンプレートを実行するために使用します。|  
|**-u** \<namespace>|テンプレートのコンパイルに使用される名前空間。|  
|**-I** \<includedirectory>|指定したテキスト テンプレートに含まれるテキスト テンプレートを格納するディレクトリ。|  
|**-P** \<referencepath>|またはを使用して、テキスト テンプレート内で指定されたアセンブリを検索するディレクトリを **-r**オプション。<br /><br /> たとえば、Visual Studio API を使用するアセンブリは、次のように使用します。<br /><br /> `-P "%VSSHELLFOLDER%\Common7\IDE\PublicAssemblies"`|  
|**-dp** \<processorName>!\<className>!\<assemblyName&#124;codeBase>|名前、完全な型の名前とテキスト テンプレート内のカスタム ディレクティブの処理に使用できるディレクティブ プロセッサのアセンブリ。|  
|**-** [processorName] [。directiveName]。\<parameterName >!\<parameterValue >|ディレクティブ プロセッサのパラメーター値を指定します。 パラメーター名と値のみを指定するパラメーターはすべてのディレクティブ プロセッサにできます。 ディレクティブ プロセッサを指定する場合、パラメーターが指定したプロセッサでのみ使用できます。 ディレクティブの名前を指定する場合、パラメーターの値は、指定されたディレクティブが処理されている場合にのみ使用です。<br /><br />  テキスト テンプレートでは、 `hostspecific` template ディレクティブでのメッセージを呼び出すと`this.Host`。 例えば:<br /><br /> `<#@template language="c#" hostspecific="true"#> [<#= this.Host.ResolveParameterValue("", "", "parameterName") #>]`。<br /><br /> 入力を常に、'!' の省略可能なプロセッサとディレクティブの名前を省略した場合でも、マークします。 例えば:<br /><br /> `-a !!param!value`|  
|**-h**|ヘルプを提供します。|  
  
## <a name="related-topics"></a>関連トピック  
  
|タスク|トピック|  
|----------|-----------|  
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューション内にファイルを生成する。|[T4 テキスト テンプレートを使用したデザイン時コード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)|  
|独自のデータ ソースを変換するためのディレクティブ プロセッサを作成する。|[T4 テキスト変換のカスタマイズ](../modeling/customizing-t4-text-transformation.md)|  
|独自のアプリケーションからのテキスト テンプレートを呼び出すことができるテキスト テンプレート ホストを記述します。|[カスタム ホストを使用したテキスト テンプレートの処理](../modeling/processing-text-templates-by-using-a-custom-host.md)|



