---
title: 概念モデルの使用 (WCF Data Services)
description: WCF Data Services で概念モデルを使用する データベース スキーマとオブジェクト モデルを双方向変換する代わりにオブジェクトを使用してデータを照会します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- data [Visual Studio], querying a service
- data [Visual Studio], LINQ to Entities
- data [Visual Studio], querying an EDM
ms.assetid: 2cd873cf-b010-49f2-a278-bb1277aaa934
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: ef5745f974848da75b4dcc0c42b59b38aa61cd0b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866113"
---
# <a name="work-with-a-conceptual-model-wcf-data-services"></a>概念モデルを使用する (WCF Data Services)

概念モデルを使用してデータベースのデータを記述すると、データベース スキーマとオブジェクト モデル間で双方向の変換を行うのではなく、オブジェクトを使用してデータを照会できます。

概念モデルは、WCF Data Services アプリケーションで使用できます。 以下のトピックでは、概念モデルを使用してデータを照会する方法について説明します。

| トピック | 説明 |
| - | - |
| [方法: データ サービス クエリを実行する](/dotnet/framework/data/wcf/how-to-execute-data-service-queries-wcf-data-services) | .NET アプリケーションからデータ サービスを照会する方法について説明します。 |
| [方法: クエリ結果を射影する](/dotnet/framework/data/wcf/how-to-project-query-results-wcf-data-services) | データ サービス クエリによって返されるデータの量を削減する方法について説明します。 |

概念モデルを使用すると、ドメインに対応する言語で有効なデータの種類を定義できます。 モデルの有効なデータを定義したり、エンティティまたはデータ サービスで実行する操作に検証を追加したりできます。

以下のトピックでは、WCF Data Services アプリケーションに検証を追加する方法について説明します。

|トピック|説明|
|-----------|-----------------|
|[方法: データ サービス メッセージを先に取得する](/dotnet/framework/data/wcf/how-to-intercept-data-service-messages-wcf-data-services)|データ サービスの操作に検証を追加する方法について説明します。|

 以下のトピックでは、エンティティに対して操作を実行して、データを作成、更新、および削除する方法について説明します。

|トピック|説明|
|-----------|-----------------|
|[方法: エンティティを追加、変更、および削除する](/dotnet/framework/data/wcf/how-to-add-modify-and-delete-entities-wcf-data-services)|データ サービスでエンティティ データを作成、更新、および削除する方法について説明します。|
|[方法: エンティティ リレーションシップを定義する](/dotnet/framework/data/wcf/how-to-define-entity-relationships-wcf-data-services)|データ サービスでリレーションシップを作成または変更する方法について説明します。|

## <a name="see-also"></a>関連項目

- [Visual Studio での Windows Communication Foundation サービスと WCF データ サービス](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
- [データ サービスに対するクエリ](/dotnet/framework/data/wcf/querying-the-data-service-wcf-data-services)
