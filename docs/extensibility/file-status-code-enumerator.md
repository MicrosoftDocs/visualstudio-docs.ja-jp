---
title: ファイル状態コード列挙子 | Microsoft Docs
description: SccStatus 列挙子には、ソース管理システム内のファイルの状態を指定する定数値が含まれ、SccQueryInfo および POPLISTFUNC によって使用されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- named constants, SccStatus enumerator
- source control plug-ins, file status enumeration
- SccStatus enumerator
- file status code enumerator
ms.assetid: 5c37876b-c83c-4ca1-837b-57cd465a879a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 95de8a29efcd56880cdaf452c9f21b90bba1c5c9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900968"
---
# <a name="file-status-code-enumerator"></a>ファイル状態コード列挙子
`SccStatus` 列挙子には、ソース管理システム内のファイルの状態を指定する名前付き定数値が含まれます。 この列挙は、[SccQueryInfo](../extensibility/sccqueryinfo-function.md) および `POPLISTFUNC` コールバック関数によって使用されます (詳細については、[POPLISTFUNC](../extensibility/poplistfunc.md) を参照してください)。

## <a name="syntax"></a>構文

```
enum SccStatus {
   SCC_STATUS_INVALID          = -1L,
   SCC_STATUS_NOTCONTROLLED    = 0x0000L,
   SCC_STATUS_CONTROLLED       = 0x0001L,
   SCC_STATUS_CHECKEDOUT       = 0x0002L,
   SCC_STATUS_OUTOTHER         = 0x0004L,
   SCC_STATUS_OUTEXCLUSIVE     = 0x0008L,
   SCC_STATUS_OUTMULTIPLE      = 0x0010L,
   SCC_STATUS_OUTOFDATE        = 0x0020L,
   SCC_STATUS_DELETED          = 0x0040L,
   SCC_STATUS_LOCKED           = 0x0080L,
   SCC_STATUS_MERGED           = 0x0100L,
   SCC_STATUS_SHARED           = 0x0200L,
   SCC_STATUS_PINNED           = 0x0400L,
   SCC_STATUS_MODIFIED         = 0x0800L,
   SCC_STATUS_OUTBYUSER        = 0x1000L
   SCC_STATUS_NOMERGE          = 0x2000L
   SCC_STATUS_RESERVED_1       = 0x4000L
   SCC_STATUS_RESERVED_2       = 0x8000L
};
```

## <a name="members"></a>メンバー
 SCC_STATUS_INVALID 状態を取得できませんでした。それに依存しないでください。

 SCC_STATUS_NOTCONTROLLED ファイルはソース管理下にありません。

 SCC_STATUS_CONTROLLED ファイルはソース管理下にあります。

 SCC_STATUS_CHECKEDOUT ローカル ディスクの現在のユーザーによってチェックアウトされています。

 SCC_STATUS_OUTOTHER ファイルは別のユーザーによってチェックアウトされています。

 SCC_STATUS_OUTEXCLUSIVE ファイルは排他的にチェックアウトされています。

 SCC_STATUS_OUTMULTIPLE ファイルは複数のユーザーによってチェックアウトされています。

 SCC_STATUS_OUTOFDATE ファイルは最新ではありません。

 SCC_STATUS_DELETED ファイルはプロジェクトから削除されています。

 SCC_STATUS_LOCKED ファイルはロックされています。これ以上のバージョンは使用できません。

 SCC_STATUS_MERGED ファイルはマージされましたが、まだ修正または検証されていません。

 SCC_STATUS_SHARED ファイルはプロジェクト間で共有されます。

 SCC_STATUS_PINNED ファイルは明示的なバージョンに共有されます。

 SCC_STATUS_MODIFIED ファイルは変更されているか、壊れているか、違反にされています。

 SCC_STATUS_OUTBYUSER ファイルは現在のユーザーによってチェックアウトされています。

 SCC_STATUS_NOMERGE ファイルをマージすることはできず、GET の前に保存する必要はありません。

 SCC_STATUS_RESERVED_1 内部使用用として予約されています。

 SCC_STATUS_RESERVED_2 内部使用用として予約されています。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [SccQueryInfo](../extensibility/sccqueryinfo-function.md)
- [POPLISTFUNC](../extensibility/poplistfunc.md)
