---
title: SccBeginBatch 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccBeginBatch
helpviewer_keywords:
- SccBeginBatch function
ms.assetid: 33968183-2e15-4e0d-955b-ca12212d1c25
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6bb145358184117046e14b7b598ce6d4bb4586b0
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66333895"
---
# <a name="sccbeginbatch-function"></a>SccBeginBatch 関数
この関数は、ソース管理操作のバッチ シーケンスを開始します。 [SccEndBatch](../extensibility/sccendbatch-function.md)をバッチの終了が呼び出されます。 これらのバッチは、入れ子にできません。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccBeginBatch(void);
```

### <a name="parameters"></a>パラメーター
 なし。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグイン実装は、次の値のいずれかを返すが必要です。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|操作のバッチは正常に開始しました。|
|SCC_E_UNKNOWNERROR|不特定のエラーです。|

## <a name="remarks"></a>Remarks
 ソース コントロールのバッチは、複数のプロジェクトまたは複数のコンテキスト全体で同じ操作を実行に使用されます。 バッチを使用して、バッチ操作中に、ユーザー エクスペリエンスから、プロジェクトごとに冗長ダイアログ ボックスを解消できます。 `SccBeginBatch`関数と[SccEndBatch](../extensibility/sccendbatch-function.md)を先頭と末尾の操作を示すために、関数のペアとして使用されます。 入れ子にできません。 `SccBeginBatch` バッチ操作が進行中であることを示すフラグを設定します。

 バッチ操作が有効では、ソース管理プラグインはユーザーに最大ですべての質問の 1 つのダイアログ ボックスを表示し、そのダイアログ ボックスからの応答を後続のすべての操作に適用する必要があります。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccEndBatch](../extensibility/sccendbatch-function.md)