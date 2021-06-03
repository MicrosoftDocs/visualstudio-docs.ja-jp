---
title: OPTNAMECHANGEPFN | Microsoft Docs
description: ソース管理プラグインから Visual Studio IDE に名前の変更を伝える OPTNAMECHANGEPFN コールバック関数について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- OPTNAMECHANGEPFN
helpviewer_keywords:
- OPTNAMECHANGEPFN callback function
ms.assetid: 147303f3-c7f1-438a-81b7-db891ea3d076
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4e6cb58aebbe76eff5c66dc29ecfad8c77c8717c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090370"
---
# <a name="optnamechangepfn"></a>OPTNAMECHANGEPFN
これは、[SccSetOption](../extensibility/sccsetoption-function.md) の呼び出し (オプション `SCC_OPT_NAMECHANGEPFN` を使用) で指定され、ソース管理プラグインによって行われた名前の変更を IDE に戻すために使用されるコールバック関数です。

## <a name="signature"></a>署名

```cpp
typedef void (*OPTNAMECHANGEPFN)(
   LPVOID pvCallerData,
   LPCSTR pszOldName,
   LPCSTR pszNewName
);
```

## <a name="parameters"></a>パラメーター
 pvCallerData

[入力] [SccSetOption](../extensibility/sccsetoption-function.md) の以前の呼び出し (オプション `SCC_OPT_USERDATA` を使用) で指定されたユーザー値。

 pszOldName

[入力] ファイルの元の名前。

 pszNewName

[入力] 変更された後のファイル名。

## <a name="return-value"></a>戻り値
 [なし] :

## <a name="remarks"></a>解説
 ファイルの名前がソース管理操作中に変更された場合、ソース管理プラグインでは、このコールバックを使用して名前の変更を IDE に通知できます。

 IDE では、このコールバックをサポートしていない場合、[SccSetOption](../extensibility/sccsetoption-function.md) を呼び出してそれを指定することはありません。 プラグインでは、このコールバックをサポートしていない場合、IDE がこのコールバックを設定しようとしたときに `SccSetOption` 関数からの `SCC_E_OPNOTSUPPORTED` を返します。

## <a name="see-also"></a>関連項目
- [IDE によって実装されたコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccSetOption](../extensibility/sccsetoption-function.md)
