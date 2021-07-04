---
title: VB デバッグ構成のプロジェクト設定 | Microsoft Docs
description: Visual Studio の [プロパティ ページ] ウィンドウで Visual Basic デバッグ構成のプロパティ設定を変更する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vbProjectPropertiesDebug
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- project settings [Visual Studio], debug configurations
- debug builds, project settings
- debugging [Visual Basic], debugger settings
- projects [Visual Studio], debug configurations
- project configurations, debug
- debug configurations, Visual Basic
ms.assetid: 72a8483a-af0b-4403-8b0d-ee9ad71ee435
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f16d0dde62a23d8272cb89aec46f2ce952f18979
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385209"
---
# <a name="project-settings-for-a-visual-basic-debug-configuration"></a>Visual Basic デバッグ構成のプロジェクト設定
「[デバッグ構成とリリース構成](../debugger/how-to-set-debug-and-release-configurations.md)」で説明されているように、[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] のデバッグ構成に対するプロジェクト設定は **[プロパティ ページ]** ウィンドウで変更できます。 次の表は、 **[プロパティ ページ]** ウィンドウのデバッガー関連の設定の場所を示しています。

> [!WARNING]
> このトピックは UWP アプリには適用されません。 「[デバッグ セッションの開始 (VB、C#、C++、および XAML)](../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md)」を参照してください。

### <a name="debug-tab"></a>[デバッグ] タブ

| 設定 | 説明 |
|------------------------------| - |
| **構成** | アプリケーションをコンパイルするためのモードを設定します。 **[Active (Debug)]\(アクティブ (デバッグ)\)** 、 **[デバッグ]** 、 **[リリース]** 、 **[すべての構成]** から選択します。 |
| **開始動作** | [デバッグ] メニューの [開始] を選択したときに発生するアクションを指定します。<br /><br /> -   既定値は **[プロジェクトの開始]** で、デバッグのスタートアップ プロジェクトを起動します。 <br />-    **[外部プログラムの開始]** では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロジェクトに含まれないプログラムを起動してアタッチできます。 詳細については、[実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)に関するページを参照してください。<br />-    **[ブラウザーを開始時に使用する URL]** は、Web アプリケーションのデバッグを有効にします。 |
| **コマンド ライン引数** | デバッグするプログラムのコマンド ライン引数を指定します。 コマンド名は、[外部プログラムの開始] に指定されたプログラム名です。 [開始動作] を [URL の開始] に設定した場合、コマンド ライン引数は無視されます。 |
| **作業ディレクトリ** | デバッグするプログラムの作業ディレクトリを指定します。 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] では、作業ディレクトリはアプリケーションが起動されるディレクトリです。 既定の作業ディレクトリは、現在の構成に応じて、\bin\Debug または \bin\Release です。 |
| **リモート コンピューターの使用** | このチェック ボックスがオンの場合、リモート デバッグは有効です。 テキスト ボックスには、デバッグ用にアプリケーションを実行するリモート コンピューターの名前または [Msvsmon サーバー名](../debugger/remote-debugging.md)を入力できます。 リモート コンピューター上の EXE ファイルの場所は、[ビルド] タブの [出力パス] プロパティで指定します。また、EXE ファイルがリモート コンピューターの共有ディレクトリにあることも必要です。 |
| **Unmanaged code debugging (アンマネージド コード デバッグ)** | マネージド アプリケーションからネイティブ (アンマネージド) Win32 コードの呼び出しをデバッグできます。 これは、[!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] プロジェクトで [デバッガーのタイプ] に [混合] を選択するのと同じ効果があります。 |
| **SQL Server デバッグ** | SQL Server データベース オブジェクトのデバッグを許可します。 |

### <a name="compile-tab-press-advanced-compile-options-button"></a>[コンパイル] タブ : [詳細コンパイル オプション] ボタンをクリックします。

| 設定 | 説明 |
|---------------------------| - |
| **最適化を有効にする** | このオプションはオフにしておくことをお勧めします。 最適化を有効にすると、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] に表示されるソース コードとは異なるコードが実行されるため、デバッグが困難になります。 コードが最適化されている場合、"マイ コードのみ" でデバッグするときに、既定でシンボルが読み込まれません。 |
| **デバッグ情報を作成** | 既定で、デバッグ バージョンとリリース バージョンの両方に定義されます。この設定 (/debug コンパイラ オプションに相当します) に基づいて、ビルド時にデバッグ情報が作成されます。 デバッガーでは、この情報を使って変数名やその他の情報を見やすい形式でデバッグ時に表示します。 この情報を設定せずにプログラムをコンパイルすると、デバッガーの機能は制限されます。 詳細については、「[/debug](/dotnet/visual-basic/reference/command-line-compiler/debug)」を参照してください。 |
| **定数 DEBUG の定義** | このシンボルを定義すると、[Debug クラス](/dotnet/api/system.diagnostics.debug)の出力関数の条件付きコンパイルが可能になります。 このシンボルを定義すると、Debug クラスのメソッドは[出力ウィンドウ](../ide/reference/output-window.md)に出力を生成します。 このシンボルを定義しない場合、Debug クラスのメソッドはコンパイルされず、出力も生成されません。 このシンボルは、デバッグ バージョンに定義します。リリース バージョンには定義しません。 リリース バージョンにこのシンボルを定義すると、不要なコードのためにプログラムの実行速度が低下します。 |
| **定数 TRACE の定義** | このシンボルを定義すると、[Trace クラス](/dotnet/api/system.diagnostics.trace)の出力関数の条件付きコンパイルが可能になります。 このシンボルを定義すると、Trace クラスのメソッドは[出力ウィンドウ](../ide/reference/output-window.md)に出力を生成します。 このシンボルを定義しない場合、Trace クラスのメソッドはコンパイルされず、出力も生成されません。 このシンボルは、既定で、デバッグ バージョンとリリース バージョンの両方に定義されます。 |

## <a name="see-also"></a>関連項目
- [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)