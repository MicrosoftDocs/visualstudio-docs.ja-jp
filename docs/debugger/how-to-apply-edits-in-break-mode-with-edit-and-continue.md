---
title: エディットコンティニュを使用して中断モードで編集を適用する |Microsoft Docs
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
ms.openlocfilehash: 05340b4922262eb134aca8fef4bf215342e5a997
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72734032"
---
# <a name="how-to-apply-edits-in-break-mode-with-edit-and-continue-visual-basic"></a>方法: エディットコンティニュを使用して中断モードで編集を適用する (Visual Basic)
エディット コンティニュを使用すると、中断モードでコードを編集した後、コードを停止したり再起動したりせずにデバッグを継続できます。

デバッグ中にエディットコンティニュを使用する場合の制限については、「[サポートされてC#いるコード変更 (および Visual Basic)](../debugger/supported-code-changes-csharp.md)」を参照してください。

### <a name="to-edit-code-in-break-mode"></a>中断モードでコードを編集するには

1. 以下のいずれかの操作を行って中断モードに入ります。

    - コードにブレークポイントを設定した後、 **[デバッグ]** メニューの **[デバッグ開始]** をクリックし、アプリケーションがブレークポイントにヒットするのを待ちます。

         -または-

    - デバッグを開始し、 **[デバッグ]** メニューの **[すべて中断]** をクリックします。

         -または-

    - 例外が発生した場合は、例外処理**アシスタント**で **[編集を有効にする]** を選択します。

2. 必要なコードとサポートされているコードを変更します。

     詳細については、「[サポートさC#れているコード変更 (および Visual Basic)](../debugger/supported-code-changes-csharp.md)」を参照してください。

    > [!NOTE]
    > エディット コンティニュで許可されないコード変更を行おうとすると、編集部分の下に紫の波線が表示され、タスク一覧にタスクが表示されます。 この場合、無効なコード変更を元に戻さない限り、コードの実行を続行できません。

3. **[デバッグ]** メニューの **[続行]** をクリックして、コードの実行を再開します。

     適用した編集がプロジェクトに取り込まれた状態でコードが実行されます。

## <a name="see-also"></a>関連項目
- [サポートされてC#いるコード変更 (および Visual Basic)](../debugger/supported-code-changes-csharp.md)
- [エディット コンティニュ (Visual Basic)](../debugger/edit-and-continue-visual-basic.md)
