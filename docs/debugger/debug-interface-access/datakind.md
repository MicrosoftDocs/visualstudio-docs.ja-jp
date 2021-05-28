---
description: データ値の特定のスコープを示します。
title: DataKind | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- DataKind enumeration
ms.assetid: b64be708-22d6-4360-99e7-8f4e6b196de7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 24f13fc1157dd7f3de723474091a1f80e3717504
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634550"
---
# <a name="datakind"></a>DataKind
データ値の特定のスコープを示します。

## <a name="syntax"></a>構文

```C++
enum DataKind {
    DataIsUnknown,
    DataIsLocal,
    DataIsStaticLocal,
    DataIsParam,
    DataIsObjectPtr,
    DataIsFileStatic,
    DataIsGlobal,
    DataIsMember,
    DataIsStaticMember,
    DataIsConstant
};
```

## <a name="elements"></a>要素
DataIsUnknown データ シンボルを特定できません。

DataIsLocal データ項目は、ローカル変数です。

DataIsStaticLocal データ項目は、静的なローカル変数です。

DataIsParam データ項目は、仮パラメーターです。

DataIsObjectPtr データ項目は、オブジェクト ポインター (`this`) です。

DataIsFileStatic データ項目は、ファイルスコープの変数です。

DataIsGlobal データ項目は、グローバル変数です。

DataIsMember データ項目は、オブジェクト メンバー変数です。

DataIsStaticMember データ項目は、クラスの静的変数です。

DataIsConstant データ項目は、定数値です。

## <a name="remarks"></a>解説
この列挙型の値は、[IDiaSymbol::get_dataKind](../../debugger/debug-interface-access/idiasymbol-get-datakind.md) メソッドによって返されます。

## <a name="requirements"></a>必要条件
ヘッダー: cvconst.h

## <a name="see-also"></a>関連項目
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_dataKind](../../debugger/debug-interface-access/idiasymbol-get-datakind.md)
