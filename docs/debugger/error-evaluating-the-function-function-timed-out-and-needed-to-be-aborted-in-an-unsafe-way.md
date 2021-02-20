---
title: 関数 &apos;function&apos; の評価がタイムアウトし、安全でない方法で中止される必要がありました | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.unsafe_func_eval_abort
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1f6cae3ffb692161deb0b162a6432efe90f12bf3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99871651"
---
# <a name="error-evaluating-the-function-39function39-timed-out-and-needed-to-be-aborted-in-an-unsafe-way"></a>エラー :関数 &#39;function&#39; の評価がタイムアウトし、安全でない方法で中止される必要がありました

メッセージ テキスト全文:関数 'function' の評価がタイムアウトし、安全でない方法で中止される必要がありました。 これにより、ターゲット プロセスが破損された可能性があります。

デバッガーは、.NET オブジェクトの状態を簡単に検査できるよう、デバッグ対象のプロセスで追加のコード (通常はプロパティの getter メソッドと ToString 関数) の実行を自動強制します。 ほとんどのシナリオでは、これらの関数はすばやく完了し、デバッグが格段に簡単になります。 ただし、デバッガーではサンドボックスでアプリケーションが実行されません。 その結果、応答しないネイティブ関数を呼び出すプロパティ getter または ToString メソッドで、タイムアウトが長くなってしまう可能性があります。これは、復旧できない場合があります。 このエラー メッセージが表示された場合は、これが発生しています。

この問題の一般的な理由の 1 つは、デバッガーがプロパティを評価するときに、実行が許可されるのは検査中のスレッドのみであるためです。 そのため、デバッグ対象のアプリケーション内で実行されるよう、プロパティが別のスレッドで待機しており、それが .NET ランタイムが中断できないような方法で待機している場合、この問題が発生します。

## <a name="to-correct-this-error"></a>このエラーを解決するには

この問題にはいくつかの対応策があります。

### <a name="solution-1-prevent-the-debugger-from-calling-the-getter-property-or-tostring-method"></a>対応策 #1:デバッガーで getter プロパティまたは ToString メソッドが呼び出されないようにする

エラー メッセージには、デバッガーが呼び出そうとした関数名が表示されます。 この関数を変更できると、デバッガーがプロパティ getter または ToString メソッドを呼び出さないようにできます。 次のいずれかの操作を試してください。

* このメソッドを、プロパティ getter または ToString メソッドではない他の種類のコードに変更すると、この問題を解消できます。
    \- または -
* (ToString の場合) 型に DebuggerDisplay 属性を定義し、デバッガーで ToString 以外のものを評価するようにします。
    \- または -
* (プロパティ getter の場合) `[System.Diagnostics.DebuggerBrowsable(DebuggerBrowsableState.Never)]` 属性をプロパティに配置します。 これは、API の互換性のために、実際はメソッドである、プロパティとして残す必要があるメソッドがある場合に便利です。

### <a name="solution-2-have-the-target-code-ask-the-debugger-to-abort-the-evaluation"></a>対応策 #2:ターゲット コードで、評価を中止するようにデバッガーに求める

エラー メッセージには、デバッガーが呼び出そうとした関数名が表示されます。 プロパティ getter または ToString メソッドがときどき正常に実行されない場合、特に、コードの実行にコードが別のスレッドを必要とすることが問題である場合は、実装関数で `System.Diagnostics.Debugger.NotifyOfCrossThreadDependency` を呼び出して、関数の評価を中止するようにデバッガーに求めることができます。 この対応策では、これらの関数を明示的に評価することができますが、NotifyOfCrossThreadDependency の呼び出し時の実行の停止がこれの既定の動作です。

### <a name="solution-3-disable-all-implicit-evaluation"></a>対応策 #3:暗黙的な評価をすべて無効にする

前の対応策で問題が解決しない場合は、 **[ツール]**  >  **[オプション]** に移動し、 **[デバッグ]**  >  **[全般]**  >  **[プロパティの評価とその他の暗黙的な関数の呼び出しを有効にする]** の設定をオフにします。 これにより、暗黙的な関数のほとんどが評価されなくなり、問題が解決されるはずです。

### <a name="solution-4-enable-managed-compatibility-mode"></a>対応策 4:マネージド互換モードを有効にする

このエラーは、レガシ デバッグ エンジンに切り替えると、回避できる場合があります。 **[ツール]**  >  **[オプション]** に移動し、 **[デバッグ]**  >  **[全般]**  >  **[マネージド互換モードの使用]** の設定をオンにします。 詳細については、[全般デバッグ オプション](../debugger/general-debugging-options-dialog-box.md)に関するページを参照してください。
