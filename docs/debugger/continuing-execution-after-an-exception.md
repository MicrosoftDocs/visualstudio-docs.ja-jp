---
title: 例外の後の実行の継続 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- managed exceptions, continuing execution after
- exceptions, continuing execution after
- debugger, exceptions
- managed code, exception handling
- exception handling, continuing execution after
- execution, continuing after an exception
- program execution
- threading [Visual Studio], continuing execution after exceptions
- Exceptions dialog box
- programs, executing
ms.assetid: 6fe97aac-2131-4615-bd92-d3afee741558
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e7be214a950c8cc93d986f97834a848bd9ab824e
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745645"
---
# <a name="continuing-execution-after-an-exception"></a>例外後の実行の継続
例外が発生したためにデバッガーが実行を中断すると、既定では**例外ヘルパー**が表示されます。 **[オプション]** ダイアログボックスで**例外ヘルパー**を無効にしている場合は、 **[例外]** 処理C#アシスタント (または Visual Basic) またはC++ **[例外]** ダイアログボックス () が表示されます。

 **例外ヘルパー**が表示されたら、例外の原因となった問題の修正を試みることができます。

## <a name="managed-and-native-code"></a>マネージコードとネイティブコード
 マネージコードとネイティブコードでは、ハンドルされない例外が発生した後も、同じスレッドで実行を継続できます。 **例外ヘルパー**は、例外がスローされた時点まで呼び出し履歴をアンワインドします。

## <a name="mixed-code"></a>混合コード
 ネイティブ コードとマネージド コードが混在するコードをデバッグしているときに、ハンドルされていない例外が発生した場合、オペレーティング システムの制約により、呼び出し履歴のアンワインドが抑制されます。 ショートカット メニューを使用して呼び出し履歴をさかのぼろうとすると、混合コードのデバッグ中は、ハンドルされていない例外からアンワインドすることはできないという内容のエラー メッセージが表示されます。

## <a name="see-also"></a>関連項目

- [デバッガーでの例外の管理](../debugger/managing-exceptions-with-the-debugger.md)