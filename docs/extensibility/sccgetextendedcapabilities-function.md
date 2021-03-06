---
description: この関数では、ソース管理プラグインによってサポートされている追加の機能を返します。
title: SccGetExtendedCapabilities 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccGetExtendedCapabilities
helpviewer_keywords:
- SccGetExtendedCapabilities function
ms.assetid: 588c6a92-2147-4d8b-a357-96ca7da0a092
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cc047fee2c92f47c181aef455b8175a4e7998176
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905593"
---
# <a name="sccgetextendedcapabilities-function"></a>SccGetExtendedCapabilities 関数
この関数では、ソース管理プラグインによってサポートされている追加の機能を返します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccGetExtendedCapabilities(
   LPVOID pContext,
   LONG lSccExCaps,
   LPBOOL pbSupported
);
```

### <a name="parameters"></a>パラメーター
 pContext

[入力] ソース管理プラグインのコンテキスト ポインター。

 lSccExCaps

[入力] テストする拡張機能を指定するフラグ (使用可能なフラグについては、拡張機能コード テーブルの[機能フラグ](../extensibility/capability-flags.md)を参照してください)。

 pbSupported

[出力] 指定した機能がサポートされている場合は 0 以外 (`TRUE`) を返します。それ以外の場合は 0 (`FALSE`) を返します。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|機能の取得操作が正常に完了しました。|
|SCC_E_UNKNOWNERROR<br /><br /> SCC_E_NONSPECIFICERROR|不明または未指定のエラーが発生しました。|

## <a name="remarks"></a>解説
 このメソッドは、オンデマンドで呼び出されます。つまり、機能をテストする必要がある場合は、このメソッドを呼び出して、その機能がサポートされているかどうかを判断します。 一度に 1 つのフラグのみが指定されます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [エラー コード](../extensibility/error-codes.md)
- [機能フラグ](../extensibility/capability-flags.md)
