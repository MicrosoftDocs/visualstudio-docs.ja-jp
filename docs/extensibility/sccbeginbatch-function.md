---
description: この関数により、ソース管理操作のバッチ シーケンスが開始されます。
title: SccBeginBatch 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccBeginBatch
helpviewer_keywords:
- SccBeginBatch function
ms.assetid: 33968183-2e15-4e0d-955b-ca12212d1c25
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5af4d8fb1d8524f16493603bb5d46ee4bdbd03ba
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060446"
---
# <a name="sccbeginbatch-function"></a>SccBeginBatch 関数
この関数により、ソース管理操作のバッチ シーケンスが開始されます。 バッチを終了するために [SccEndBatch](../extensibility/sccendbatch-function.md) が呼び出されます。 これらのバッチを入れ子にすることはできません。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccBeginBatch(void);
```

### <a name="parameters"></a>パラメーター
 [なし] :

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値を返すことが想定されます。

|値|説明|
|-----------|-----------------|
|SCC_OK|操作のバッチが正常に開始されました。|
|SCC_E_UNKNOWNERROR|不特定のエラーです。|

## <a name="remarks"></a>解説
 ソース管理バッチは、複数のプロジェクトまたは複数のコンテキストで同じ操作を実行するために使用されます。 バッチを使用すると、バッチされた操作中に、ユーザー エクスペリエンスから冗長なプロジェクトごとのダイアログ ボックスを削除できます。 `SccBeginBatch` 関数と [SccEndBatch](../extensibility/sccendbatch-function.md) は、操作の開始と終了を示すペアとして使用されます。 入れ子にすることはできません。 `SccBeginBatch` により、バッチ操作が進行中であることを示すフラグが設定されます。

 バッチ操作が有効になっている間、ソース管理プラグインでは、ユーザーに対するすべての質問に対して最大 1 つのダイアログ ボックスを表示し、後続のすべての操作にそのダイアログ ボックスから応答を適用する必要があります。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccEndBatch](../extensibility/sccendbatch-function.md)
