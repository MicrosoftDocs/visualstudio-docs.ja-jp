---
title: '方法: ASP.NET Exceptions をデバッグする |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], ASP.NET exceptions
- ASP.NET, exceptions
- exceptions, ASP.NET
ms.assetid: 1810096e-de8c-435e-be3d-f365d0cd0a6a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
ms.openlocfilehash: 9f8391d355b2f540db4e38486b8992d940336464
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72733798"
---
# <a name="how-to-debug-aspnet-exceptions"></a>方法 : ASP.NET の例外をデバッグする
例外のデバッグは、堅牢な [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] アプリケーションの開発において重要な部分です。 例外をデバッグする方法に関する一般的な情報は[、「デバッガーでの例外の管理](../debugger/managing-exceptions-with-the-debugger.md)」を参照してください。

 ハンドルされない [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 例外をデバッグする場合、その例外でデバッガーが停止していることを確認する必要があります。 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ランタイムにはトップレベルの例外ハンドラーがあります。 そのため、デバッガーは既定では、ハンドルされない例外で実行を中断することはありません。 例外がスローされたときにデバッガーに割り込むには、 **[例外]** ダイアログ ボックスで、その特定の例外に対して **[例外が次の場合に中断する: スローされるとき]** の設定を選択する必要があります。

 マイコードのみを有効にした場合、**例外がスローされたときに中断します**。 .net メソッドまたはその他のシステムコードで例外がスローされた場合、デバッガーは直ちに中断されません。 デバッガーがシステム コード以外のコードをヒットするまで実行は継続され、ヒットした時点でデバッガーは中断されます。 つまり、例外が発生したときにシステム コードをステップ実行する必要はありません。

 [マイ コードのみ] では、さらに便利な **[例外が次の場合に中断する: ユーザーにハンドルされていないとき]** を選択することもできます。 例外にこの設定を選択すると、ユーザー コードで例外が取得され、処理された場合にのみ、デバッガーによってユーザー コードの実行が中断されます。 この設定では、トップレベルの [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 例外ハンドラーの効果が無視されます。この例外ハンドラーがユーザー コードではないためです。

### <a name="to-enable-debugging-of-aspnet-exceptions-with-just-my-code"></a>[マイ コードのみ] で ASP.NET 例外を有効にするには

1. **[デバッグ]** メニューの **[例外]** をクリックします。

     **[例外]** ダイアログ ボックスが表示されます。

2. **[Common Language Runtime Exceptions]** 行の **[スローされるとき]** または **[ユーザーにハンドルされていないとき]** チェック ボックスをオンにします。

     **[ユーザーにハンドルされていないとき]** 設定を使用するには、 **[マイ コードのみ]** を有効にする必要があります。

### <a name="to-use-best-practices-for-aspnet-exception-handling"></a>ASP.NET の例外処理で推奨される手順を使用するには

- 予測でき、処理方法がわかる例外をスローできるコードを、`try ... catch` ブロックで囲みます。 たとえば、アプリケーションから XML Web サービスを呼び出したり、SQL Server を直接呼び出したりする場合、そのコードは、**try … catch** ブロックで囲みます。この場合、数多くの例外が発生すると予想できるためです。

## <a name="see-also"></a>関連項目
- [ASP.NET アプリケーションをデバッグする](../debugger/how-to-enable-debugging-for-aspnet-applications.md)