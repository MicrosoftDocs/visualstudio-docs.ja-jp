---
title: メッセージ クラスに対する、.ofs ファイルの無効なプロパティ
description: .ofs ファイルの 1 つ以上のプロパティが、選択されたメッセージ クラスに対して有効でない場合に発生するエラーを修正する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VSTO.NewFormRegionWizard.OFSPropertyError
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b22870cdb038adee84adc0fd7a56c269cb048626
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99841917"
---
# <a name="invalid-properties-in-the-ofs-file-for-the-message-class"></a>メッセージ クラスに対する、.ofs ファイルの無効なプロパティ

  エラー ".ofs ファイルの 1 つ以上のプロパティが、選択されたメッセージ クラスに対して有効ではありません" は、Outlook でデザインしたフォーム領域をインポートする場合に、フォーム領域の 1 つ以上のフィールドが、**新しいフォーム領域** ウィザードの最後のページで選択するメッセージ クラスと互換性がないときに発生します。

たとえば、 **新しいフォーム領域** ウィザードの最後のページで **[仕事 (IPM.Task)]** を選択したとします。 フォーム領域に **[会社住所]** フィールドが含まれている場合、タスクには会社住所がないため、このエラーが表示されます。 つまり、 **[会社住所]** フィールドは、`IPM.Task` メッセージ クラスとの互換性がないということです。

 **新しいフォーム領域** ウィザードの最後のページで **[仕事 (IPM.Task)]** を選択したとします。 フォーム領域に **[会社住所]** フィールドが含まれている場合、タスクには会社住所がないため、このエラーが表示されます。 つまり、 **[会社住所]** フィールドは、`IPM.Task` メッセージ クラスとの互換性がないということです。

## <a name="to-correct-this-error"></a>このエラーを解決するには

- **新しいフォーム領域** ウィザードの最後のページで、フォーム領域のフィールドと互換性のあるメッセージ クラスを選択します。

- Outlook のフォーム デザイナーで、メッセージ クラスと互換性のないフィールドを削除します。 **新しいフォーム領域** ウィザードの最後のページで選択するフィールドを削除します。

## <a name="see-also"></a>関連項目
- [チュートリアル : Outlook でデザインしたフォーム領域のインポート](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
