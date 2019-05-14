---
title: エディット コンティニュの中断モードで編集を適用 |Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.variables.failededit
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue [Visual Basic], applying edits in break mode
- break mode, applying code changes
- Edit and Continue, applying edits in break mode
- editing, break mode
- coding, editing in break mode
- code, editing in break mode
ms.assetid: 1eef7498-6a1f-4fba-8146-510adc6375c9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d6c821c63354ec1b7cc83e302a3c2682982696e2
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387689"
---
# <a name="how-to-apply-edits-in-break-mode-with-edit-and-continue-visual-basic"></a>方法: 編集と中断モードで編集を適用し、続行 (Visual Basic)
エディット コンティニュを使用すると、中断モードでコードを編集した後、コードを停止したり再起動したりせずにデバッグを継続できます。

デバッグ中にエディット コンティニュの使用に関する制限については、次を参照してください。[サポートされているコードの変更 (C#および Visual Basic)](../debugger/supported-code-changes-csharp.md)します。

### <a name="to-edit-code-in-break-mode"></a>中断モードでコードを編集するには

1. 以下のいずれかの操作を行って中断モードに入ります。

    - コードにブレークポイントを設定した後、**[デバッグ]** メニューの **[デバッグ開始]** をクリックし、アプリケーションがブレークポイントにヒットするのを待ちます。

         - または -

    - デバッグを開始し、**[デバッグ]** メニューの **[すべて中断]** をクリックします。

         - または -

    - 例外が発生したときに選択**編集を有効にする**上、**例外処理アシスタント**します。

2. 必要なサポートされているコード変更を加えます。

     詳細については、次を参照してください。 [(c# および Visual Basic) のサポートされているコード変更](../debugger/supported-code-changes-csharp.md)します。

    > [!NOTE]
    > エディット コンティニュで許可されないコード変更を行おうとすると、編集部分の下に紫の波線が表示され、タスク一覧にタスクが表示されます。 この場合、無効なコード変更を元に戻さない限り、コードの実行を続行できません。

3. **[デバッグ]** メニューの **[続行]** をクリックして、コードの実行を再開します。

     適用した編集がプロジェクトに取り込まれた状態でコードが実行されます。

## <a name="see-also"></a>関連項目
- [サポートされているコード変更 (C# および Visual Basic)](../debugger/supported-code-changes-csharp.md)
- [エディット コンティニュ (Visual Basic)](../debugger/edit-and-continue-visual-basic.md)
