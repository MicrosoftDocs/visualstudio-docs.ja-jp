---
title: ディレクトリ状態コード列挙子 | Microsoft Docs
description: SccDirStatus 列挙子には、ソース管理システム内のディレクトリファイルの状態を指定する名前付き定数値が含まれ、SccDirQueryInfo によって使用されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- directory status code enumerator
- source control plug-ins, directory status enumeration
ms.assetid: 616026b5-f529-40ef-90c1-1836e116d797
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a504c6c080c34b4506cf4078b64465a3bd6c7d97
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904231"
---
# <a name="directory-status-code-enumerator"></a>ディレクトリの状態コードの列挙子
`SccDirStatus` 列挙子には、ソース管理システム内のディレクトリの状態を指定する名前付き定数値が含まれます。 この列挙子は、[SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md) で使用されます。 これは、ソース管理プラグイン API のバージョン 1.2 で導入されました。

## <a name="syntax"></a>構文

```
enum SccDirStatus {
   SCC_DIRSTATUS_INVALID       = -1L,
   SCC_DIRSTATUS_NOTCONTROLLED = 0x0000L,
   SCC_DIRSTATUS_CONTROLLED    = 0x0001L,
   SCC_DIRSTATUS_EMPTYPROJ     = 0x0002L
};
```

## <a name="members"></a>メンバー
 SCC_DIRSTATUS_INVALID 状態を取得できませんでした。これに依存しないでください。

 SCC_DIRSTATUS_NOTCONTROLLED ディレクトリがソース管理下にありません。

 SCC_DIRSTATUS_CONTROLLED ディレクトリがソース管理下にあります。

 このディレクトリに対応した SCC_DIRSTATUS_EMPTYPROJ プロジェクトが空です。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)
