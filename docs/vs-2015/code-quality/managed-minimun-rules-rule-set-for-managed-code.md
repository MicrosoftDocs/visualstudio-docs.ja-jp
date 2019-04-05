---
title: マネージ コードの"マネージ最小規則"規則の設定 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
ms.assetid: 44a50c54-8dd3-42b2-8387-532a150e5a6c
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: fbbbdf8a1ece9a57d0216a6c9b59ac9d2a8ea474
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58963655"
---
# <a name="managed-minimun-rules-rule-set-for-managed-code"></a>マネージド コードの "マネージ最小規則" 規則セット
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

最小の管理規則は、潜在的なセキュリティ ホール、アプリケーションのクラッシュ、およびその他の重要なロジックとデザイン エラーなど、コードの最も重大な問題に集中します。 プロジェクトにカスタムの規則セットを作成する場合は、必ずこの規則セットを含める必要があります。  
  
|ルール|説明|  
|----------|-----------------|  
|[CA1001](../code-quality/ca1001-types-that-own-disposable-fields-should-be-disposable.md)|破棄可能なフィールドを所有する型は、破棄可能でなければなりません|  
|[CA1821](../code-quality/ca1821-remove-empty-finalizers.md)|空のファイナライザーを削除します|  
|[CA2213](../code-quality/ca2213-disposable-fields-should-be-disposed.md)|破棄可能なフィールドは破棄されなければなりません|  
|[CA2231](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)|ValueType.Equals のオーバーライドで、演算子 equals をオーバーロードします|
