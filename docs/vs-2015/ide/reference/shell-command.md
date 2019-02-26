﻿---
title: Shell コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- tools.shell
helpviewer_keywords:
- exe files
- Shell command
- Tools.Shell command
- executables, running from Visual Studio
- .exe files
- Shell, launching exe files
- Visual Studio, executables from
ms.assetid: 737fda23-b852-45c4-a9fe-41cbce6ba70f
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 62b4a3e83b368a015cee30284acee0dbab39ca36
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2019
ms.locfileid: "54779309"
---
# <a name="shell-command"></a>Shell コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 内から実行可能プログラムを起動します。  
  
## <a name="syntax"></a>構文  
  
```  
Tools.Shell [/command] [/output] [/dir:folder] path [args]  
```  
  
## <a name="arguments"></a>引数  
 `path`  
 必須です。 実行するファイルまたは開くドキュメントのパスとファイル名。 指定したファイルが、PATH 環境変数のディレクトリのいずれにもない場合は、完全パスが必要です。  
  
 `args`  
 任意。 呼び出されるプログラムに渡す引数。  
  
## <a name="switches"></a>スイッチ  
 /commandwindow、/command、/c または /cmd  
 任意。 実行可能ファイルの出力が **[コマンド]** ウィンドウに表示されるように指定します。  
  
 /dir:`folder` または /d: `folder`  
 任意。 プログラムの実行時に作業ディレクトリが設定されるように指定します。  
  
 /outputwindow、/output、/out、または /o  
 任意。 実行可能ファイルの出力が **[出力]** ウィンドウに表示されるように指定します。  
  
## <a name="remarks"></a>解説  
 /dir、/o、/c の各スイッチは、`Tools.Shell` の直後に指定する必要があります。 実行可能ファイルの名前の後に指定した内容は、その実行可能ファイルにコマンド ライン引数として渡されます。  
  
 定義済みの `Shell` エイリアスは、`Tools.Shell` の代わりに使用できます。  
  
> [!CAUTION]
>  `path` 引数でディレクトリ パスとファイル名を指定する場合は、次のように、リテラル二重引用符 (""") でパス名全体を囲む必要があります。  
  
```  
Tools.Shell """C:\Program Files\SomeFile.exe"""  
```  
  
 3 つの二重引用符 (""") の各セットは、`Shell` プロセッサによって、1 つの二重引用符として解釈されます。 そのため、上の例では実際には次のパス文字列を `Shell` コマンドに渡します。  
  
```  
"C:\Program Files\SomeFile.exe"  
```  
  
> [!CAUTION]
>  パス文字列をリテラル二重引用符 (""") で囲まなかった場合、Windows では、文字列のうち最初の空白までの部分のみが使用されます。 たとえば、上記のパス文字列を引用符で適切に囲まなかった場合、Windows では、C:\ ルート ディレクトリにある "Program" というファイルが検索されます。 C:\Program.exe という実行可能ファイルが実際は使用可能な場合、不正改ざんによってインストールされたファイルであっても、Windows では目的の "c:\Program Files\SomeFile.exe" プログラムではなく、そのプログラムの実行が試行されます。  
  
## <a name="example"></a>例  
 次のコマンドでは xcopy.exe を使用して、ファイル `MyText.txt` を `Text` フォルダーにコピーします。 xcopy.exe からの出力は、**コマンド ウィンドウ**と **[出力]** ウィンドウの両方に表示されます。  
  
```  
>Tools.Shell /o /c xcopy.exe c:\MyText.txt c:\Text\MyText.txt  
```  
  
## <a name="see-also"></a>関連項目
 [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)   
 [コマンド ウィンドウ](../../ide/reference/command-window.md)   
 [[出力] ウィンドウ](../../ide/reference/output-window.md)   
 [[検索/コマンド] ボックス](../../ide/find-command-box.md)   
 [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
