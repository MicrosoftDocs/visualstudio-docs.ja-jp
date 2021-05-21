---
title: マネージド コードの "マネージ最小規則" 規則セット
ms.date: 11/04/2016
description: Visual Studio の "マネージド最小規則" 規則セットについて説明します。これはセキュリティ、堅牢性、およびその他の重要な問題に重点を置いています。 規則の説明を示します。
ms.custom: SEO-VS-2020
ms.topic: reference
ms.assetid: 44a50c54-8dd3-42b2-8387-532a150e5a6c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 8711fd0a265618a5aaf4f84edcf7dd2b081b16a3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99859815"
---
# <a name="managed-minimum-rules-rule-set-for-managed-code"></a>マネージド コードの "マネージ最小規則" 規則セット

"マネージド最小規則" は、セキュリティ ホール、アプリケーション クラッシュ、その他の重要な論理エラーやデザイン エラーなど、コードに含まれる最も重要な問題に関するものです。 プロジェクトにカスタムの規則セットを作成する場合は、この規則セットを含めます。

|ルール|説明|
|----------|-----------------|
|[CA1001](/dotnet/fundamentals/code-analysis/quality-rules/ca1001)|破棄可能なフィールドを所有する型は、破棄可能でなければなりません|
|[CA1821](/dotnet/fundamentals/code-analysis/quality-rules/ca1821)|空のファイナライザーを削除します|
|[CA2213](/dotnet/fundamentals/code-analysis/quality-rules/ca2213)|破棄可能なフィールドは破棄されなければなりません|
|[CA2231](/dotnet/fundamentals/code-analysis/quality-rules/ca2231)|`ValueType.Equals` のオーバーライドで、演算子 equals をオーバーロードします|
