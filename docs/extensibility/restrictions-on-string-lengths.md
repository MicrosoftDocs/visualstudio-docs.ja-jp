---
title: 文字列長の制限 | Microsoft Docs
description: ソース管理プラグイン API によって課せられるさまざまな関数で使用される文字列の長さの制限について学習します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, restrictions on string lengths
ms.assetid: 877173d2-ca27-43b3-b1f4-8379f7c5e268
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b7526494f5d64f7e02e63e5ec3012297af730e87
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068415"
---
# <a name="restrictions-on-string-lengths"></a>文字列長の制限
ソース管理プラグイン API では、さまざまな関数で使用される文字列の長さを制限します。

## <a name="string-length-values"></a>文字列長の値

|定数|値|
|--------------|-----------|
|`SCC_NAME_LEN`|31|
|`SCC_AUXLABEL_LEN`|31|
|`SCC_USER_LEN`|31|
|`SCC_PRJPATH_LEN`|300|

> [!NOTE]
> 長さには、終端の `null` は含まれません。 "_LEN" ではなく "_SIZE" サフィックスを持つその他の定数には、終端の `null` のスペースが含まれます。

|定数|値|
|--------------|-----------|
|SCC_NAME_SIZE|32|
|SCC_AUXLABEL_SIZE|32|
|SCC_USER_SIZE|32|
|SCC_PRJPATH_SIZE|301|

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
