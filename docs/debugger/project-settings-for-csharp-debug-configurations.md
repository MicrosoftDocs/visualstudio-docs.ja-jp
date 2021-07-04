---
title: C# デバッグ構成のプロジェクト設定 | Microsoft Docs
description: Visual Studio でプロジェクト プロパティ ページの [デバッグ] タブと [ビルド] タブを使用し、C# デバッグ構成のプロジェクト設定を変更する方法について理解します。
ms.custom: SEO-VS-2020
ms.date: 11/21/2018
ms.topic: reference
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debug configurations, C#
- project settings [Visual Studio], debug configurations
- debug builds, project settings
- projects [Visual Studio], debug configurations
- project configurations, debug
- debugging [C#], debugger settings
ms.assetid: e30ca810-66e9-4d6e-9cf6-9f285cd0b100
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 3377187412f95e090c7403ddd6f898a18f6cec9f
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386502"
---
# <a name="project-settings-for--c-debug-configurations"></a>C# デバッグ構成のプロジェクト設定

C# プロジェクトのデバッグ設定は、プロジェクト プロパティ ページの [[デバッグ] タブ](#debug-tab)と [[ビルド] タブ](#build-tab) で変更できます。

プロパティ ページを開くには、**ソリューション エクスプローラー** でプロジェクトを選択して **[プロパティ]** アイコンを選択するか、プロジェクトを右クリックして **[プロパティ]** を選択します。

詳細については、[デバッグ構成とリリース構成](how-to-set-debug-and-release-configurations.md)に関するページを参照してください。

>[!IMPORTANT]
>これらの設定は、.NET Core、ASP.NET、UWP アプリには適用されません。 UWP アプリのデバッグ設定を構成するには、「[UWP アプリのデバッグ セッションを開始する](start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md)」を参照してください。

## <a name="debug-tab"></a>[デバッグ] タブ

|設定|説明|
|-------------------------------------| - |
| **構成** | アプリをビルドするためのモードを設定します。 ドロップダウンから、 **[アクティブ (デバッグ)]** 、 **[デバッグ]** 、 **[リリース]** 、または **[すべての構成]** を選択します。 |
| **開始動作** | デバッグ構成で **[開始]** を選択した場合のアクションを指定します。<br />既定値は -  **[プロジェクトの開始]** で、デバッグのスタートアップ プロジェクトを起動します。 詳細については、[スタートアップ プロジェクトの選択](/previous-versions/visualstudio/visual-studio-2010/0s590bew(v=vs.100))に関するページをご覧ください。<br />-  **[外部プログラムの開始]** が起動され、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロジェクトに含まれないアプリにアタッチされます。 詳細については、[デバッガーで実行中のプロセスにアタッチする](attach-to-running-processes-with-the-visual-studio-debugger.md)に関するページを参照してください。<br />-  **[ブラウザーを開始時に使用する URL]** を使用して、Web アプリをデバッグできます。 |
| **[開始オプション]**  >  **[コマンド ライン引数]** | デバッグするアプリのコマンド ライン引数を指定します。 コマンド名は、 **[外部プログラムの開始]** に指定したアプリ名です。 |
| **[開始オプション]**  >  **[作業ディレクトリ]** | デバッグするアプリの作業ディレクトリを指定します。 C# の作業ディレクトリは、既定で *\bin\debug* です。
| **[開始オプション]**  >  **[リモート コンピューターを使用する]**|リモート デバッグの場合は、このオプションを選択し、リモート デバッグ ターゲットの名前 ([Msvsmon サーバー名](../debugger/remote-debugging.md)) を入力します。 <br />リモート マシン上のアプリの場所は、 **[ビルド]** タブの **[出力パス]** プロパティで指定します。また、EXE ファイルがリモート コンピューターの共有ディレクトリにあることも必要です。
| **[デバッガー エンジン]**  >  **[アンマネージ コード デバッグを有効にする]** | マネージ アプリからネイティブ (アンマネージ) Win32 コードへの呼び出しをデバッグします。 |
| **[デバッガー エンジン]**  >  **[SQL Server デバッグを有効にする]** | SQL Server データベース オブジェクトをデバッグします。 |

## <a name="build-tab"></a>[ビルド] タブ

|設定|説明|
|-------------|-----------------|
|**[全般]**  >  **[条件付きコンパイル シンボル]**|選択されている場合は、DEBUG 定数と TRACE 定数を定義します。<br /><br /> これらの定数により、[Debug クラス](/dotnet/api/system.diagnostics.debug)と [Trace クラス](/dotnet/api/system.diagnostics.trace)の条件付きコンパイルが有効になります。 これらの定数を定義すると、Debug クラスと Trace クラスのメソッドによって[出力ウィンドウ](../ide/reference/output-window.md)に出力が生成されます。 これらの定数を定義しない場合、Debug クラスと Trace クラスのメソッドはコンパイルされず、出力も生成されません。<br /><br />通常、DEBUG はビルドのデバッグ バージョンで定義され、リリース バージョンでは定義されません。 TRACE は、デバッグ バージョンとリリース バージョンの両方で定義されます。|
|**[全般]**  >  **[コードの最適化]**|最適化されたコードでのみバグが発生する場合を除き、この設定は、デバッグ ビルドではオフのままにしておきます。 最適化されたコードは、命令がソース コードのステートメントに直接対応していないため、デバッグが難しくなります。|
|**[出力]**  >  **[出力パス]**|通常は、デバッグ用の *bin\Debug* に設定します。|
|**[詳細設定]** ボタン|詳細なデバッグ オプションについては、[[ビルドの詳細設定] ダイアログ ボックス (C#)](../ide/reference/advanced-build-settings-dialog-box-csharp.md) に関するページを参照してください。 シンボル ( *.pdb*) ファイルの移植可能な形式は、.NET Core アプリの最新のクロスプラットフォーム形式です。

## <a name="see-also"></a>関連項目
- [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)