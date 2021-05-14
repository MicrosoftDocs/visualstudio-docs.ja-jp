---
title: デバッグ中はデザイナーを変更できません
description: デバッグ中はデザイナーを変更できません。 この Visual Studio オブジェクト リレーショナル デザイナー (O/R デザイナー) メッセージに関する情報を表示してください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 487dafe4-d57c-4be1-9e3a-bb0a8699b2fa
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 244fbcc21c062c50b2f61940a1b43cf17c22761f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866438"
---
# <a name="the-designer-cannot-be-modified-while-debugging"></a>デバッグ中はデザイナーを変更できません

このメッセージは、アプリケーションがデバッグ モードで実行されているときに、**O/R デザイナー** で項目を変更しようとした場合に表示されます。 アプリケーションがデバッグ モードで実行されている場合、**O/R デザイナー** は読み取り専用です。

このエラーを修正するには、 **[デバッグ]** メニューで **[デバッグの停止]** を選択します。 アプリケーションのデバッグが停止し、**O/R デザイナー** の項目を変更できるようになります。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
