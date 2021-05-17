---
title: シンボル型のクラス階層 | Microsoft Docs
description: Visual Studio Debug Interface Access SDK のクラス階層で、シンボル型の一覧を確認します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- symbols [DIA SDK], class hierarchies
ms.assetid: 0ccd6990-4654-44cd-a6f3-bdd82fe90f6c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c33b6852935bbe02c75b0814fd2f77095d283c15
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "108634223"
---
# <a name="class-hierarchy-of-symbol-types"></a>シンボル型のクラス階層
次の表では、クラス階層内のシンボル型について説明します。

## <a name="symbol-types"></a>シンボル型

|シンボル型|説明|
|-----------------|-----------------|
|[UDT](../../debugger/debug-interface-access/udt.md)|各クラス、構造体、共用体を表すために使用されるシンボル。|
|[Enum (Debug Interface Access SDK)](../../debugger/debug-interface-access/enum-debug-interface-access-sdk.md)|列挙型のシンボル。|
|[PointerType](../../debugger/debug-interface-access/pointertype.md)|ポインター型のシンボル。|
|[ArrayType](../../debugger/debug-interface-access/arraytype.md)|配列型のシンボル。|
|[BaseType](../../debugger/debug-interface-access/basetype.md)|基本型のシンボル。|
|[Typedef (Debug Interface Access SDK)](../../debugger/debug-interface-access/typedef-debug-interface-access-sdk.md)|他の型の名前を導入するシンボル。|
|[BaseClass](../../debugger/debug-interface-access/baseclass.md)|ユーザー定義型 (UDT) の各基底クラスに使用されるシンボル。|
|[フレンド (Debug Interface Access SDK)](../../debugger/debug-interface-access/friend-debug-interface-access-sdk.md)|フレンド クラスとフレンド関数のシンボル。|
|[FunctionType](../../debugger/debug-interface-access/functiontype.md)|一意の関数シグネチャごとのシンボル。|
|[FunctionArgType](../../debugger/debug-interface-access/functionargtype.md)|関数に対する各パラメーターのシンボル。|
|[VTableShape](../../debugger/debug-interface-access/vtableshape.md)|仮想テーブルのサイズのシンボル。|
|[VTable](../../debugger/debug-interface-access/vtable.md)|仮想テーブルのシンボル。|
|[CustomType](../../debugger/debug-interface-access/customtype.md)|ベンダー定義型のシンボル。|
|[ManagedType](../../debugger/debug-interface-access/managedtype.md)|メタデータで定義されている型のシンボル。|
|[ディメンション](../../debugger/debug-interface-access/dimension.md)|配列の次元のシンボル。|

> [!NOTE]
> 各シンボルには、シンボルに関する情報を保持するプロパティや、他のシンボルへの参照を含めることができます。 これらのプロパティの一覧については、個々のシンボルのトピックを参照してください。

## <a name="see-also"></a>関連項目
- [CV_access_e 列挙型](../../debugger/debug-interface-access/cv-access-e.md)
- [シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
- [シンボルとシンボル タグ](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)