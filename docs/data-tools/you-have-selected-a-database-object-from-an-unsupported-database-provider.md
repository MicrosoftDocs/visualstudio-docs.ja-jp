---
title: サポートされていないデータベース プロバイダーのデータベース オブジェクトが選択されています
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: c0f1298e-31aa-471e-ae19-1bafffd2ae40
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 13e6dd42ed372fb28d850a566ea1900447ad220c
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55909516"
---
# <a name="you-have-selected-a-database-object-from-an-unsupported-database-provider"></a>サポートされていないデータベース プロバイダーのデータベース オブジェクトが選択されています

**O/R デザイナー** for SQL Server、.NET Framework Data Provider のみをサポートしています (<xref:System.Data.SqlClient>)。 **[OK]** をクリックし、サポートされないデータベース プロバイダーからオブジェクトの処理を続けることもできますが、実行時に予期しない動作が発生することがあります。

> [!NOTE]
> .NET Framework Data Provider for SQL Server を使用するデータ接続のみがサポートされます。

## <a name="options"></a>オプション

- **[OK]** をクリックして、サポートされないデータベース プロバイダーを使用する接続にマップされるエンティティ クラスのデザインを続行します。 サポートされないデータベース プロバイダーを使用すると、予期しない動作が発生することがあります。

- クリックして**キャンセル**アクションを停止します。 作成または SQL Server 用 .NET Framework Provider を使用する別のデータ接続を使用します。

## <a name="see-also"></a>関連項目

- [O/R デザイナーのメッセージ](../data-tools/o-r-designer-messages.md)
- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)