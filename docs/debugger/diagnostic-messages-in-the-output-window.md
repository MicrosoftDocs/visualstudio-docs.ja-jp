---
title: 出力ウィンドウにメッセージを送信 |Microsoft Docs
ms.date: 11/08/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- diagnostic messages [C#]
- System.Diagnostics.Debug class, Output window
- messages, diagnostic
- Debug.Print replacements
- diagnosis
- Output window, diagnostic messages
- System.Diagnostics.Trace class, Output window
- Trace class, diagnostic messages
- diagnostics
- debugger, Output window
- debugging [Visual Studio], diagnostic messages in Output window
- Debug class
ms.assetid: 386e9524-be17-4573-83fb-4f7c5cae0be0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bb4493eb55b83b9f76d1a833ba2df359ae9683e8
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56682506"
---
# <a name="send-messages-to-the-output-window"></a>出力ウィンドウにメッセージを送信する

実行時のメッセージを記述することができます、**出力**ウィンドウを使用して、<xref:System.Diagnostics.Debug>クラスまたは<xref:System.Diagnostics.Trace>に含まれるクラスの<xref:System.Diagnostics>クラス ライブラリ。 使用して、<xref:System.Diagnostics.Debug>クラスのみ出力をする場合、*デバッグ*プログラムのバージョン。 使用して、<xref:System.Diagnostics.Trace>クラスの両方で出力する場合、*デバッグ*と*リリース*バージョン。

## <a name="output-methods"></a>出力メソッド
 <xref:System.Diagnostics.Trace> クラスと <xref:System.Diagnostics.Debug> クラスが提供する出力方法は次のとおりです。

- 各種の `Write` メソッド。実行を中断せずに情報を出力します。 これらのメソッドは、Visual Basic の以前のバージョンで使用されていた `Debug.Print` メソッドに代わるものです。

- <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName>メソッドで、指定した条件が失敗した場合に実行し、出力の情報を中断します。 既定では、`Assert` メソッドはダイアログ ボックスに情報を出力します。 詳細については、「[マネージド コードのアサーション](../debugger/assertions-in-managed-code.md)」を参照してください。

- <xref:System.Diagnostics.Debug.Fail%2A?displayProperty=fullName>と<xref:System.Diagnostics.Trace.Fail%2A?displayProperty=fullName>メソッドで、実行と出力の情報を常に中断します。 既定では、`Fail` メソッドはダイアログ ボックスに情報を出力します。

**出力**ウィンドウに関する情報を表示できます。

- デバッガーが読み込んだり、アンロードしたりしたモジュール

- スローされた例外

- 終了したプロセス

- 終了したスレッド

## <a name="see-also"></a>関連項目
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [[出力] ウィンドウ](../ide/reference/output-window.md)
- [アプリケーションのトレースとインストルメント化](/dotnet/framework/debug-trace-profile/tracing-and-instrumenting-applications)
- [C#、F#、Visual Basic プロジェクト タイプ](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)
- [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
