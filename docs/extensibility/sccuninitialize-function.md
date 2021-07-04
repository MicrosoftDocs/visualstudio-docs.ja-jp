---
description: この関数では、ソース管理プラグインをシャットダウンする準備として、SccInitialize の以前の呼び出しによって作成された割り当てや開いている接続をすべてクリーンアップします。
title: SccUninitialize 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccUninitialize
helpviewer_keywords:
- SccUninitialize function
ms.assetid: 17cf5337-d251-4422-bc96-93fe7d48f2ae
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0d46aedd3e962d0684689ff29a34061b777fe08e
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904075"
---
# <a name="sccuninitialize-function"></a>SccUninitialize 関数
この関数では、ソース管理プラグインをシャットダウンする準備として、[SccInitialize](../extensibility/sccinitialize-function.md) の以前の呼び出しによって作成された割り当てや開いている接続をすべてクリーンアップします。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccUninitialize (
   LPVOID pvContext
);
```

#### <a name="parameters"></a>パラメーター
 pvContext

[入力] [SccInitialize](../extensibility/sccinitialize-function.md) で作成されたソース管理プラグインのコンテキスト構造体へのポインター。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|クリーンアップが正常に完了しました。|

## <a name="remarks"></a>解説
 ソース管理プラグインは、シャットダウンに対して準備し、そのプラグインがコンテキスト構造体のために割り当てたメモリを解放することに責任を負っています。 この関数は、プラグインの特定のインスタンスごとに 1 回呼び出されます。 この呼び出しの前に [SccInitialize](../extensibility/sccinitialize-function.md) の呼び出しが行われます。 `SccUninitialize` の呼び出しの時点では、どのプロジェクトも開いたままでいることはできません。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
