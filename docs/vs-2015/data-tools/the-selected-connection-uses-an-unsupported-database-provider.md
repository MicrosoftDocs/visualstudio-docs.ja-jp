---
title: 選択した接続はサポートされていないデータベースプロバイダーを使用しています |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 4d25dfa1-8fa4-4529-9b90-973bc2ec2993
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4e79d8408fba54cf192d51f9d2ead8c0ffafe1f0
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667189"
---
# <a name="the-selected-connection-uses-an-unsupported-database-provider"></a>選択した接続では、サポートされていないデータベース プロバイダーが使用されています
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このメッセージは、**サーバーエクスプローラー** SQL Server の .NET Framework Data Provider を使用しない項目を[Visual Studio の / ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)**にドラッグ**したときに表示されます。

 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]では、.NET Framework Provider for SQL Server を使用するデータ接続のみがサポートされます。 有効な接続は、Microsoft SQL Server または Microsoft SQL Server データベース ファイルへの接続だけです。

### <a name="to-correct-this-error"></a>このエラーを解決するには

- .NET Framework Data Provider for SQL Server を使用するデータ接続の項目のみを [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]に追加します。

## <a name="see-also"></a>参照
 [データプロバイダーの <xref:System.Data.SqlClient> .NET Framework](https://msdn.microsoft.com/library/03a9fc62-2d24-491a-9fe6-d6bdb6dcb131) [チュートリアル: LINQ to SQL クラスの作成 (O/R デザイナー)](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233)