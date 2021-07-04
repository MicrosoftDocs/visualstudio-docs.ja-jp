---
title: コンソール プロジェクトのデバッグを準備する | Microsoft Docs
description: Visual Studio でコンソール プロジェクト (C#、C++、Visual Basic、F#) をデバッグするための準備に関する情報をお届けします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], console applications
- debugging console applications
- console applications, debugging
ms.assetid: 9641f1d9-2d5a-48b1-8731-6525e8f67892
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4d1610919667fdaf1a752ca56aef5358c0bd34f3
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387815"
---
# <a name="debugging-preparation-console-projects-c-c-visual-basic-f"></a>デバッグの準備:コンソール プロジェクト (C#、C++、Visual Basic、F#)

コンソール プロジェクトのデバッグの準備は Windows プロジェクトのデバッグの準備に似ていますが、コマンド ライン引数の設定や、デバッグ用にアプリを一時停止する方法など、追加の考慮事項がいくつかあります。 詳細については、[Windows フォーム アプリのデバッグの準備](../debugger/debugging-preparation-windows-forms-applications.md)に関する記事を参照してください。 コンソール アプリケーションはどれも類似しているため、このトピックでは次のプロジェクトの種類について説明します。

- C#、Visual Basic、F# コンソール アプリケーション

- C++ コンソール アプリケーション (.NET)

- C++ コンソール アプリケーション (Win32)

  コンソール アプリケーションは、 **[コンソール]** ウィンドウを使用して、入力を受け付けたり出力メッセージを表示したりします。 **[コンソール]** ウィンドウに書き込むには、アプリケーションで Debug オブジェクトではなく **Console** オブジェクトを使用する必要があります。 ただし、**Visual Studio の出力** ウィンドウに書き込むには、通常どおりに Debug オブジェクトを使用します。 アプリケーションの書き込み先を理解し、間違った場所でメッセージを探すことのないようにしてください。 詳細については、「[Console クラス](/dotnet/api/system.console)」、「[Debug クラス](/dotnet/api/system.diagnostics.debug)」、「[[出力] ウィンドウ](../ide/reference/output-window.md)」を参照してください。

## <a name="set-command-line-arguments"></a>コマンド ライン引数を設定する

コンソール アプリケーションのコマンド ライン引数を指定する必要がある場合があります。 詳細については、次を参照してください[C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)、 [Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)、または[c# デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)。

すべてのプロジェクト プロパティと同様に、これらの引数はデバッグ セッション間および Visual Studio セッション間で保持されます。 このため、コンソール アプリケーションを以前にデバッグしたことがある場合は、前回のセッションで **[\<Project> プロパティ ページ]** ダイアログ ボックスに入力した引数が存在する場合があります。

## <a name="start-the-application"></a>アプリケーションの起動

 いくつかのコンソール アプリケーションが起動すると、それらのアプリケーションは最後まで実行されてから終了します。 この動作のため、実行を中断してデバッグする時間が十分ない場合があります。 アプリケーションをデバッグできるようにするには、次のいずれかの手順に従ってアプリケーションを起動します。

- コードにブレークポイントを設定し、アプリケーションを開始します。

- **F10** キー ( **[デバッグ]**  >  **[ステップ オーバー]** ) または **F11** キー ( **[デバッグ]**  >  **[ステップ イン]** ) を使用してアプリケーションを起動し、 **[Run to click]\(クリックして実行\)** などの他のオプションを使用して、コード内を移動します。

- コード エディターで行を右クリックして、 **[カーソル行の前まで実行]** を選択します。

  コンソール アプリケーションをデバッグする場合、Visual Studio からではなく、コマンド プロンプトからアプリケーションを起動することもできます。 その場合は、コマンド プロンプトからアプリケーションを起動し、Visual Studio デバッガーをアプリケーションにアタッチします。 詳細については、[実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)に関するページを参照してください。

  Visual Studio からコンソール アプリケーションを起動すると、 **[コンソール]** ウィンドウが Visual Studio ウィンドウの背後に表示される場合があります。 Visual Studio からコンソール アプリケーションを起動しようとしても、何も起こらない場合は、Visual Studio ウィンドウを移動してみてください。

## <a name="see-also"></a>関連項目
- [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)
- [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
- [C++ プロジェクトのデバッグの準備](../debugger/debugging-preparation-visual-cpp-project-types.md)
- [C#、F#、および Visual Basic のプロジェクト](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)
- [C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)
- [デバッガーのセキュリティ](../debugger/debugger-security.md)