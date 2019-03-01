---
title: Microsoft Visual Studio デバッガー (例外がスローされます) ダイアログ ボックス |Microsoft Docs
titleSuffix: ''
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.exceptions.thrown
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Microsoft Visual Studio Debugger (Exception Thrown) dialog box
- exception handling, during debugging
- debugger, exceptions
- throwing exceptions, during debugging
ms.assetid: 1fe98d10-c8f9-4b39-a920-99169bfd542e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e1111bc7f3fbb0f515bfeb5247f70925c1ab304d
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56681284"
---
# <a name="microsoft-visual-studio-debugger-exception-thrown-dialog-box"></a>[Microsoft Visual Studio デバッガー (例外がスローされました)] ダイアログ ボックス
プログラムに例外が発生しました。 このダイアログ ボックスには、スローされた例外の種類が報告されます。 コードでは、この例外を処理する必要があります。 この例外を処理するには、次のオプションから選択できます。

 **Break**デバッガーを中断する操作を実行できます。 中断するまで、例外ハンドラーは起動されません。 中断した位置から継続すると、例外ハンドラーが起動されます。

 **引き続き**により、実行を継続するには、例外ハンドラーに例外を処理する機会を提供します。 このオプションは、特定の種類の例外に対しては使用できません。 **[継続]** によってアプリケーションは実行を継続できます。 ネイティブ アプリケーションでは、例外が再スローされます。 マネージド アプリケーションでは、プログラムが終了するか、または例外がホスト アプリケーションによって処理されます。

> [!NOTE]
>  未処理の例外がマネージド コードで発生した後には実行を継続できません。 マネージド コードで未処理の例外が発生した後に **[継続]** をクリックすると、デバッグが停止します。

 **無視**例外ハンドラーは起動せずに続行する操作を実行できます。 例外ハンドラーが起動されないため、例外やエラーなどが続けて発生することがあります。 このオプションは、特定の種類の例外に対しては使用できません。

## <a name="see-also"></a>関連項目
- [デバッガーでの例外の管理](../debugger/managing-exceptions-with-the-debugger.md)
- [例外の推奨事項](/dotnet/standard/exceptions/best-practices-for-exceptions)
- [例外処理](/cpp/windows/exception-handling-cpp-component-extensions)