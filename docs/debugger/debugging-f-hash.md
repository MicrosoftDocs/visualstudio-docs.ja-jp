---
title: デバッグF#|Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Debugging [F#]
- F#, debugging
ms.assetid: 20bcd51c-2d06-4281-9a1e-ef2b91d1a779
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 10bcc9162d41fd07b85d7cb1bf87adc31367bda1
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "55008908"
---
# <a name="debugging-f"></a>F# のデバッグ
F# のデバッグは、他のマネージド言語のデバッグとほとんど同じですが、次の例外があります。  
  
-   **[自動変数]** ウィンドウに F# 変数は表示されません。  
  
-   F# ではエディット コンティニュはサポートされません。 デバッグ セッション中に F# コードを編集することは可能ですが、そのような操作は避けてください。 コードの変更はデバッグ セッション中は適用されないため、デバッグ中に F# コードを編集すると、ソース コードとデバッグ中のコードが一致しなくなります。  
  
-   デバッガーは F# 式を認識しません。 F# のデバッグ中にデバッガー ウィンドウまたはダイアログ ボックスに式を入力するには、式を C# の構文に変換する必要があります。 F# の式を C# に変換するときは、C# では等価を示す比較演算子として == を使用しますが、F# では単一の = を使用することに注意してください。  
  
## <a name="see-also"></a>関連項目  
 [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
