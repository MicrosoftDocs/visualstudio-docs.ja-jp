---
description: この関数では、ソース管理プラグインでファイル上の複数のチェックアウトが許可されているかどうかをチェックします。
title: SccIsMultiCheckoutEnabled 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccIsMultiCheckoutEnabled
helpviewer_keywords:
- SccIsMultiCheckoutEnabled function
ms.assetid: 6721639d-e475-4766-81b5-ee40a280fc70
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7b9fc81a20e3a8078a2d4cebbc6a8db10c2e2e49
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902515"
---
# <a name="sccismulticheckoutenabled-function"></a>SccIsMultiCheckoutEnabled 関数
この関数では、ソース管理プラグインでファイル上の複数のチェックアウトが許可されているかどうかをチェックします。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccIsMultiCheckoutEnabled(
   LPVOID pContext,
   LPBOOL pbMultiCheckout
);
```

#### <a name="parameters"></a>パラメーター
 pContext

[入力] ソース管理プラグインのコンテキスト構造体。

 pbMultiCheckout

[出力] このプロジェクトで複数のチェックアウトが有効になっているかどうかを指定します (0 以外は複数のチェックアウトがサポートされていることを示します)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|チェックに成功しました。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|不特定のエラーです。|

## <a name="remarks"></a>解説
 IDE では、ファイルを複数のユーザーが同時にチェックアウトできるかどうかを判定するために 2 つのチェックを行います。 最初に、ソース管理システムが複数のチェックアウトをサポートしている必要があります。 ソース管理プラグインでは、`SCC_CAP_MULTICHECKOUT` を指定することによって、初期化中にこの機能を指定できます。 その後、2 番目のチェックとして、IDE でこの関数を呼び出して、現在のプロジェクトが複数のチェックアウトをサポートしているかどうかを判定します。 選択されたプロジェクトで複数のチェックアウトがサポートされている場合、プラグインは成功コードを返し、`pbMultiCheckout` を 0 以外 (`TRUE`) または `FALSE` に設定します。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
