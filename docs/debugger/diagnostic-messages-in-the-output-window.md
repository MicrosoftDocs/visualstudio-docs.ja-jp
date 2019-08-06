---
title: 出力ウィンドウにメッセージを送信する |Microsoft Docs
ms.date: 11/08/2018
ms.topic: conceptual
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
ms.openlocfilehash: 47b563f58d08a732ec224bb8bbf47ad807c4e81d
ms.sourcegitcommit: ce1ab8a25c66a83e60eab80ed8e1596fe66dd85c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2019
ms.locfileid: "68605381"
---
# <a name="send-messages-to-the-output-window"></a>出力ウィンドウにメッセージを送信する

クラスライブラリの<xref:System.Diagnostics.Debug> <xref:System.Diagnostics.Trace>  一部であるクラスまたはクラスを使用して、実行時メッセージを出力ウィンドウに書き込むことができ<xref:System.Diagnostics>ます。 プログラムの<xref:System.Diagnostics.Debug> *デバッグ*バージョンでの出力のみが必要な場合は、クラスを使用します。 デバッグバージョン<xref:System.Diagnostics.Trace>と*リリース*バージョンの両方で出力する場合は、クラスを使用します。

## <a name="output-methods"></a>出力メソッド
 <xref:System.Diagnostics.Trace> クラスと <xref:System.Diagnostics.Debug> クラスが提供する出力方法は次のとおりです。

- 各種の `Write` メソッド。実行を中断せずに情報を出力します。 これらのメソッドは、Visual Basic の以前のバージョンで使用されていた `Debug.Print` メソッドに代わるものです。

- <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName>メソッド<xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName>とメソッド。指定された条件が失敗した場合に、実行および出力情報を中断します。 既定では、`Assert` メソッドはダイアログ ボックスに情報を出力します。 詳細については、「[マネージド コードのアサーション](../debugger/assertions-in-managed-code.md)」を参照してください。

- メソッド<xref:System.Diagnostics.Debug.Fail%2A?displayProperty=fullName> と<xref:System.Diagnostics.Trace.Fail%2A?displayProperty=fullName>メソッド。常に実行および出力情報を中断します。 既定では、`Fail` メソッドはダイアログ ボックスに情報を出力します。

**[出力]** ウィンドウには、次の情報も表示されます。

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
