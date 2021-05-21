---
title: マネージド コードの "グローバリゼーション規則" 規則セット
ms.date: 11/04/2016
description: Visual Studio の "グローバリゼーション規則" 規則セットについて説明します。これは言語、ロケール、およびカルチャに関連する問題に焦点を当てています。 規則の説明を示します。
ms.custom: SEO-VS-2020
ms.topic: reference
ms.assetid: 3c4032ee-0805-4581-8c48-b1827cd6b213
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: fdf816b978aac5d22b1750eeabe3737f1eb64085
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99867933"
---
# <a name="globalization-rules-rule-set-for-managed-code"></a>マネージド コードの "グローバリゼーション規則" 規則セット

Microsoft の "グローバリゼーション規則" 規則セットを使用して、アプリケーションのデータが異なる言語、ロケール、およびカルチャで正しく表示されない可能性のある問題に焦点を当てます。 アプリケーションのローカライズまたはグローバル化 (またはその両方) を行う場合には、この規則セットを含める必要があります。

|ルール|説明|
|----------|-----------------|
|[CA1303](/dotnet/fundamentals/code-analysis/quality-rules/ca1303)|ローカライズされるパラメーターとしてリテラルを渡さない|
|[CA1304](/dotnet/fundamentals/code-analysis/quality-rules/ca1304)|CultureInfo を指定します|
|[CA1305](/dotnet/fundamentals/code-analysis/quality-rules/ca1305)|IFormatProvider を指定します|
|[CA1307](/dotnet/fundamentals/code-analysis/quality-rules/ca1307)|意味を明確にするための StringComparison の指定|
|[CA1308](/dotnet/fundamentals/code-analysis/quality-rules/ca1308)|文字列を大文字に標準化します|
|[CA1309](/dotnet/fundamentals/code-analysis/quality-rules/ca1309)|順序を示す StringComparison を使用します|
|[CA1310](/dotnet/fundamentals/code-analysis/quality-rules/ca1310)|正確な StringComparison の指定|
|[CA2101](/dotnet/fundamentals/code-analysis/quality-rules/ca2101)|P/Invoke 文字列引数に対してマーシャリングを指定します|
