---
title: 例外の後に実行を継続 |Microsoft Docs
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a966709ed4b3fbb773d9f91726f4f79289af5504
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53864470"
---
# <a name="continuing-execution-after-an-exception"></a>例外後の実行の継続
デバッガーは、例外のための実行を中断と、表示されます、**例外ヘルパー**、既定では。 無効にした場合、**例外ヘルパー**で、**オプション** ダイアログ ボックスが表示されます、**例外処理アシスタント**(c# または Visual Basic) または**例外**  ダイアログ ボックス (C++)。  
  
 ときに、**例外ヘルパー**が表示されたら、例外の原因となった問題を解決しようとすることができます。
  
## <a name="managed-and-native-code"></a>マネージ コードとネイティブ コード  
 マネージ コードとネイティブ コードでハンドルされない例外の後に同じスレッドで実行を続行することができます。 **例外ヘルパー**例外がスローされたポイントにコール スタックをアンワインドします。
  
## <a name="mixed-code"></a>混合コード  
 ネイティブ コードとマネージド コードが混在するコードをデバッグしているときに、ハンドルされていない例外が発生した場合、オペレーティング システムの制約により、呼び出し履歴のアンワインドが抑制されます。 ショートカット メニューを使用して呼び出し履歴をさかのぼろうとすると、混合コードのデバッグ中は、ハンドルされていない例外からアンワインドすることはできないという内容のエラー メッセージが表示されます。  
  
## <a name="see-also"></a>「  
 [デバッガーでの例外の管理](../debugger/managing-exceptions-with-the-debugger.md)