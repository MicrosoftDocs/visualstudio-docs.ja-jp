---
title: .ofs ファイルの 1 つ以上のプロパティが、選択されたメッセージ クラスに対して有効ではありません
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VSTO.NewFormRegionWizard.OFSPropertyError
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d58ad6ff89d8cf41ec60135cfbfe3deac1382f1e
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60095270"
---
# <a name="one-or-more-properties-in-the-ofs-file-are-not-valid-for-the-message-class-selected"></a>.ofs ファイルの 1 つ以上のプロパティが、選択されたメッセージ クラスに対して有効ではありません
  Outlook でデザインしたフォーム領域をインポートするときに、このエラーが表示されますが、フォーム領域上の 1 つまたは複数のフィールドはの最後のページで選択したメッセージ クラスと互換性のない、**新しいフォーム領域**ウィザード。

たとえば、 **新しいフォーム領域** ウィザードの最後のページで **[仕事 (IPM.Task)]** を選択したとします。 フォーム領域がある場合、**ビジネス アドレス**フィールドでは、タスクは会社住所があるないために、このエラーを受け取ります。 そのため、**ビジネス アドレス**フィールドと互換性がない、 `IPM.Task` message クラス。

 選択した**タスク (IPM します。タスク)** の最後のページで、**新しいフォーム領域**ウィザード。 フォーム領域がある場合、**ビジネス アドレス**フィールドでは、タスクは会社住所があるないために、このエラーを受け取ります。 そのため、**ビジネス アドレス**フィールドと互換性がない、 `IPM.Task` message クラス。

## <a name="to-correct-this-error"></a>このエラーを解決するには

- **新しいフォーム領域** ウィザードの最後のページで、フォーム領域のフィールドと互換性のあるメッセージ クラスを選択します。

- Outlook でフォーム デザイナーでのメッセージ クラスと互換性のないフィールドを削除します。 最後のページで選択するフィールドを削除、**新しいフォーム領域**ウィザード。

## <a name="see-also"></a>関連項目
- [チュートリアル: Outlook でデザインしたフォーム領域をインポートします。](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
