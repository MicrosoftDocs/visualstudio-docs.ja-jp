---
title: プロパティを削除できません
description: プロパティを削除できません。 この Visual Studio オブジェクト リレーショナル デザイナー (O/R デザイナー) メッセージに関する情報を表示してください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 55873f74-7834-4ec1-8815-eeeb65618d87
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 03d9fa4368251ec36dad8f791f033fdce1f71adb
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99858333"
---
# <a name="the-property-property-name-cannot-be-deleted"></a>プロパティ \<property name> を削除できません

プロパティ \<property name> は、\<class name> と \<class name> との間の継承に対する **識別子のプロパティ** として設定されているため、削除できません。

選択されたプロパティは、エラー メッセージに示されているクラス間の継承に対する **識別子のプロパティ** として設定されています。 プロパティがデータ クラス間の継承構成に関与している場合、そのプロパティを削除することはできません。

**識別子のプロパティ** をデータ クラスの別のプロパティに設定して、目的のプロパティが正常に削除されるようにしてください。

## <a name="to-correct-this-error"></a>このエラーを解決するには

1. **O/R デザイナー** で、エラー メッセージに示されているデータ クラスを接続する継承線を選択します。

2. **識別子** プロパティを別のプロパティに設定します。

3. プロパティの削除を再試行します。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)