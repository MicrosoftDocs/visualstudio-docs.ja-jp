---
title: サポートされていないデータ型
description: 1 つ以上の選択された項目に、デザイナーでサポートされていないデータ型が含まれています。 この Visual Studio O/R デザイナー メッセージに関する情報を表示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 71dcd4f9-2946-42c5-9ce4-99c819ea2785
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: c50d47363217a87147275a406d5370cc8736c10b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866646"
---
# <a name="one-or-more-selected-items-contain-a-data-type-that-is-not-supported-by-the-designer"></a>1 つ以上の選択された項目に、デザイナーでサポートされていないデータ型が含まれています

**サーバー エクスプローラー** または **データベース エクスプローラー** から **O/R デザイナー** にドラッグされた項目の 1 つまたは複数に、[CLR ユーザー定義型](/dotnet/framework/data/adonet/sql/clr-user-defined-types)など、**O/R デザイナー** でサポートされていないデータ型が含まれています。

## <a name="to-correct-this-error"></a>このエラーを解決するには

1. 目的のテーブルをベースにした、サポートされていないデータ型を含まないビューを作成します。

2. **サーバー エクスプローラー** または **データベース エクスプローラー** からデザイナーにビューをドラッグします。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
