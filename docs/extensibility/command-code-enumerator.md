---
title: コマンド コード列挙子 | Microsoft Docs
description: コマンド コード列挙子は、オプションが指定されているコマンドを示すために SccGetCommandOptions および SccPopulateListto のオプションで使用されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- command code enumerator
- source control plug-ins, command code enumeration
ms.assetid: 5d2c360c-59e4-4da8-bcb4-dd07c7441e40
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b97d5083c4f262ae2d86aeef5ee2627fdc854bcb
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901384"
---
# <a name="command-code-enumerator"></a>コマンド コード列挙子
この列挙子は、オプションが指定されているコマンドを示すために [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) および [SccPopulateList](../extensibility/sccpopulatelist-function.md) のオプションで使用されます。

## <a name="syntax"></a>構文

```
enum SCCCOMMAND {
   SCC_COMMAND_GET,
   SCC_COMMAND_CHECKOUT,
   SCC_COMMAND_CHECKIN,
   SCC_COMMAND_UNCHECKOUT,
   SCC_COMMAND_ADD,
   SCC_COMMAND_REMOVE,
   SCC_COMMAND_DIFF,
   SCC_COMMAND_HISTORY,
   SCC_COMMAND_RENAME,
   SCC_COMMAND_PROPERTIES,
   SCC_COMMAND_OPTIONS
};
```

## <a name="members"></a>メンバー
SCC_COMMAND_GET は [SccGet](../extensibility/sccget-function.md) に対応します。

SCC_COMMAND_CHECKOUT は [SccCheckout](../extensibility/scccheckout-function.md) に対応します。

SCC_COMMAND_CHECKIN は [SccCheckin](../extensibility/scccheckin-function.md) に対応します。

SCC_COMMAND_UNCHECKOUT は [SccUncheckout](../extensibility/sccuncheckout-function.md) に対応します。

SCC_COMMAND_ADD は [SccAdd](../extensibility/sccadd-function.md) に対応します。

SCC_COMMAND_REMOVE は [SccRemove](../extensibility/sccremove-function.md) に対応します。

SCC_COMMAND_DIFF は [SccDiff](../extensibility/sccdiff-function.md) に対応します。

SCC_COMMAND_HISTORY は [SccHistory](../extensibility/scchistory-function.md) に対応します。

SCC_COMMAND_RENAME は [SccRename](../extensibility/sccrename-function.md) に対応します。

SCC_COMMAND_PROPERTIES は [SccProperties](../extensibility/sccproperties-function.md) に対応します。

SCC_COMMAND_OPTIONS は [SccSetOption](../extensibility/sccsetoption-function.md) に対応します。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)
- [SccPopulateList](../extensibility/sccpopulatelist-function.md)
