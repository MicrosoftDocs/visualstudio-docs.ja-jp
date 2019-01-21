---
title: -Build (devenv.exe)
ms.date: 12/10/2018
ms.prod: visual-studio-dev15
ms.topic: reference
helpviewer_keywords:
- builds, command-line
- /build Devenv switch
- Devenv, /build switch
- build Devenv switch
- command-line builds
ms.assetid: ced21627-7653-455b-8821-3e31c6a448cf
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 30637a797d8c0845bae9548bb6a48e877d44727b
ms.sourcegitcommit: 38db86369af19e174b0aba59ba1918a5c4fe4a61
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2019
ms.locfileid: "54269476"
---
# <a name="build-devenvexe"></a>/Build (devenv.exe)

指定したソリューションの構成ファイルを使用してソリューションまたはプロジェクトをビルドします。

## <a name="syntax"></a>構文

```shell
devenv SolutionName /Build [SolnConfigName [/Project ProjName [/ProjectConfig ProjConfigName]] [/Out OutputFilename]]
```

## <a name="arguments"></a>引数

- *SolutionName*

  必須です。 ソリューション ファイルの完全パスと名前。

- *SolnConfigName*

  任意。 *SolutionName* で指定されたソリューションのビルドに使用されるソリューション構成の名前 (`Debug`、`Release` など)。 複数のソリューション プラットフォームが利用できる場合、プラットフォームも指定する必要があります (`Debug|Win32` など)。 この引数が指定されていないか空の文字列 (`""`) の場合、ソリューションのアクティブな構成が使用されます。

- `/Project` *ProjName*

  任意。 ソリューション内のプロジェクト ファイルのパスと名前です。 *SolutionName* フォルダーからプロジェクト ファイルへの相対パス、プロジェクトの表示名、プロジェクト ファイルの完全なパスと名前を入力できます。

- `/ProjectConfig` *ProjConfigName*

  任意。 指定したプロジェクトのビルド時に使用されるプロジェクトのビルド構成の名前 (`Debug`、`Release` など)。 複数のソリューション プラットフォームが利用できる場合、プラットフォームも指定する必要があります (`Debug|Win32` など)。 このスイッチを指定すると、*SolnConfigName* 引数はオーバーライドされます。

- `/Out` *OutputFilename*

  任意。 ツールの出力を送信する先のファイル名。 このファイルが既に存在する場合、ファイルの末尾に出力が追加されます。

## <a name="remarks"></a>コメント

- `/Build` スイッチを指定すると、統合開発環境 (IDE) 内の **[ソリューションのビルド]** メニュー コマンドと同じ機能が実行されます。

- 空白を含む文字列を二重引用符で囲みます。

- エラーなどのビルドの概要情報は、[コマンド] ウィンドウ、または `/Out` スイッチで指定された任意のログ ファイルに表示できます。

- `/Build` スイッチを指定すると、最後のビルド以降に変更されたプロジェクトのみがビルドされます。 ソリューション内のすべてのプロジェクトをビルドするには、代わりに [/rebuild](../../ide/reference/rebuild-devenv-exe.md) を使用します。

- "**無効なプロジェクト構成**" というエラー メッセージが表示された場合は、ソリューション プラットフォームまたはプロジェクト プラットフォーム (`Debug|Win32` など) を指定していることを確認してください。

## <a name="example"></a>例

次のコマンドでは、`MySolution` 内の `Debug` プロジェクト ビルド構成を使用して、プロジェクト `CSharpWinApp` をビルドします。

```shell
devenv "%USERPROFILE%\source\repos\MySolution.sln" /build Debug /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig Debug
```

## <a name="see-also"></a>関連項目

- [プロジェクトとソリューションをビルドおよびクリーンする](../../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)
- [Devenv コマンドライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
- [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)
- [/Clean (devenv.exe)](../../ide/reference/clean-devenv-exe.md)
- [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)